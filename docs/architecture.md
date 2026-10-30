# Softly — Arquitetura do Aplicativo

**Projeto:** Softly  
**Versão do documento:** 1.0  
**Plataforma:** Android nativo  
**Linguagem:** Kotlin  
**Interface:** Jetpack Compose  
**Padrão arquitetural:** MVVM + Clean Architecture simplificada  
**Status:** Planejamento

---

## 1. Visão geral

O Softly é um aplicativo Android nativo destinado à concentração, ao relaxamento e à produtividade.

A arquitetura será desenvolvida priorizando:

- Separação de responsabilidades.
- Facilidade de manutenção.
- Testabilidade das regras de negócio.
- Gerenciamento adequado do ciclo de vida Android.
- Reprodução eficiente de múltiplos sons.
- Persistência local.
- Evolução incremental das funcionalidades.

O projeto será inicialmente organizado em um único módulo Gradle, `:app`, utilizando pacotes para separar as responsabilidades.

A criação de módulos Gradle adicionais será considerada apenas quando houver necessidade técnica comprovada.

---

## 2. Tecnologias

| Tecnologia | Responsabilidade |
|---|---|
| Kotlin | Linguagem principal |
| Jetpack Compose | Interface declarativa |
| Material 3 | Componentes e sistema visual |
| ViewModel | Gerenciamento do estado das telas |
| StateFlow | Exposição de estados observáveis |
| Coroutines | Operações assíncronas |
| Navigation Compose | Navegação |
| Room | Persistência estruturada |
| DataStore | Preferências |
| Media3 | Reprodução de áudio e integração com serviços de mídia |
| JUnit | Testes unitários |

As versões das bibliotecas serão controladas pelo arquivo `gradle/libs.versions.toml`.

Não serão definidas versões de dependências neste documento, pois deverão ser verificadas quanto à compatibilidade durante a implementação.

---

## 3. Camadas arquiteturais

O aplicativo terá três camadas principais:

### Presentation

Responsável pela interface e interação com o usuário.

Contém:

- Composables.
- ViewModels.
- Estados de interface.
- Eventos de interação.
- Componentes visuais reutilizáveis.

A camada de apresentação não deverá acessar diretamente o banco de dados.

### Domain

Responsável pelas regras de negócio independentes da interface.

Contém:

- Modelos de domínio.
- Interfaces de repositório.
- Casos de uso quando necessários.
- Regras de validação.

Casos de uso serão criados quando representarem operações de negócio relevantes, evitando classes que apenas repassem chamadas sem acrescentar comportamento.

### Data

Responsável por recuperar e armazenar informações.

Contém:

- Implementações dos repositórios.
- Entidades Room.
- DAOs.
- Configurações DataStore.
- Mapeadores entre entidades e modelos de domínio.

---

## 4. Estrutura inicial de pacotes

Pacote principal:

`com.dannyrodrygues.softly`

Estrutura planejada:

```text
com.dannyrodrygues.softly
│
├── MainActivity.kt
│
├── presentation/
│   ├── home/
│   ├── sounds/
│   ├── focus/
│   ├── activities/
│   ├── notes/
│   ├── library/
│   ├── settings/
│   └── components/
│
├── domain/
│   ├── model/
│   ├── repository/
│   └── usecase/
│
├── data/
│   ├── local/
│   │   ├── database/
│   │   ├── dao/
│   │   └── entity/
│   │
│   ├── preferences/
│   ├── mapper/
│   └── repository/
│
├── playback/
│   ├── controller/
│   ├── service/
│   └── model/
│
├── timer/
│
├── navigation/
│
├── di/
│
└── ui/
    └── theme/
```

Essa estrutura representa o planejamento, não os arquivos que já existem.

Os pacotes serão criados progressivamente conforme as funcionalidades forem implementadas.

---

## 5. Arquitetura MVVM

O Softly utilizará o padrão Model-View-ViewModel.

### View

Representada pelas telas Jetpack Compose.

Responsabilidades:

- Exibir informações.
- Receber interações.
- Observar estados.
- Encaminhar eventos ao ViewModel.

### ViewModel

Responsável por coordenar a lógica de apresentação.

Responsabilidades:

- Expor estados com StateFlow.
- Processar eventos da interface.
- Executar operações de domínio.
- Comunicar-se com repositórios por meio de contratos.
- Tratar estados de carregamento e erro.

### Model

Representa os dados e regras utilizados pelo aplicativo.

Será distribuído entre as camadas Domain e Data, conforme a responsabilidade.

### Fluxo de comunicação

```text
Usuário
   │
   ▼
Jetpack Compose
   │
   │ Evento
   ▼
ViewModel
   │
   ▼
Repositório / Caso de uso
   │
   ▼
Fonte de dados
   │
   ▼
Room / DataStore
```

As atualizações de estado serão observadas pela interface, permitindo recomposição automática dos elementos necessários.

---

## 6. Arquitetura de áudio

O motor de áudio será um dos componentes mais importantes do Softly.

Ele deverá permitir:

- Reprodução simultânea de sons.
- Controle individual de volume.
- Reprodução contínua.
- Ativação e desativação independente.
- Interrupção de todos os sons.
- Gerenciamento de recursos.
- Reprodução em segundo plano.

### Componentes planejados

**AudioPlaybackController**

Interface responsável pelas operações de reprodução.

**AudioPlaybackManager**

Responsável pela coordenação dos sons ativos, volumes e estados de reprodução.

**AudioPlaybackService**

Serviço Android responsável por manter a reprodução de mídia quando o aplicativo estiver em segundo plano, conforme os requisitos da plataforma.

### Fluxo conceitual

```text
SoundsScreen
     │
     ▼
SoundsViewModel
     │
     ▼
AudioPlaybackController
     │
     ▼
AudioPlaybackManager
     │
     ▼
Mecanismo de reprodução
     │
     ▼
Saída de áudio
```

O Media3 será avaliado como base para a reprodução e integração com MediaSession.

A implementação de múltiplos canais com volumes independentes deverá ser validada por um protótipo técnico antes da definição definitiva do motor de áudio.

Não será assumido que uma única instância de ExoPlayer fornece automaticamente todos os recursos necessários ao mixer.

### Ciclo de vida

O mecanismo de reprodução não deverá depender diretamente da existência de uma tela Compose.

A interface deverá observar o estado do controlador de áudio, enquanto o serviço de reprodução gerenciará os recursos associados à reprodução em segundo plano.

A implementação deverá respeitar as regras atuais do Android referentes a serviços de mídia, permissões e foco de áudio.

---

## 7. Arquitetura do temporizador

O Pomodoro será independente das telas.

### Responsabilidades

O componente responsável pelo timer deverá:

- Controlar o estado da sessão.
- Registrar o instante de início.
- Calcular o tempo restante.
- Processar pausa e retomada.
- Detectar a conclusão.
- Informar mudanças de estado.
- Permitir associação opcional com tarefas.

### Estados previstos

```text
IDLE
  │
  ▼
RUNNING
  │
  ├── PAUSED
  │      │
  │      └── RUNNING
  │
  └── COMPLETED
```

O temporizador deverá utilizar referências temporais apropriadas para calcular o tempo restante, evitando depender exclusivamente de incrementos periódicos de um contador.

Para intervalos decorridos, será considerada uma referência monotônica, como `SystemClock.elapsedRealtime()`.

A estratégia de recuperação após encerramento do processo ou reinicialização do aparelho será definida durante a implementação.

O funcionamento do timer em segundo plano será tratado separadamente da reprodução de áudio, considerando as restrições de execução do Android.

---

## 8. Persistência de dados

O Softly utilizará duas soluções principais.

### Room

Responsável pelos dados estruturados:

- Tarefas.
- Anotações.
- Sessões de foco.
- Ambientes personalizados em versões futuras.

Entidades planejadas:

```text
TaskEntity
NoteEntity
FocusSessionEntity
SoundPresetEntity (futuro)
```

As entidades serão criadas conforme os requisitos implementados.

### DataStore

Responsável por preferências:

- Tema selecionado.
- Duração do foco.
- Duração da pausa.
- Preferências gerais.
- Configurações simples de reprodução, quando aplicável.

A persistência será realizada de forma assíncrona, sem bloquear a thread principal.

---

## 9. Navegação

A navegação principal utilizará Navigation Compose.

### Destinos previstos

```text
HOME
FOCUS
ACTIVITIES
LIBRARY
SETTINGS
SOUND_DETAILS
```

A navegação inferior apresentará:

1. Início.
2. Foco.
3. Atividades.
4. Biblioteca.

As configurações serão acessadas por um controle específico da interface.

A tela de detalhes de um ambiente será aberta a partir da tela inicial ou da biblioteca.

---

## 10. Identidade visual

O Softly utilizará o design system Midnight Lavender.

### Cores principais

| Elemento | HEX |
|---|---|
| Background | `#101322` |
| Surface | `#1C2033` |
| Primary | `#B6A4F2` |
| Secondary | `#A3C9BA` |
| Accent | `#F2BFA5` |
| OnBackground | `#F4F2FA` |
| TextSecondary | `#A6A8BE` |

### Tipografia

Família principal planejada: Manrope.

### Componentes reutilizáveis previstos

- SoftlyButton.
- SoftlyCard.
- SoftlyTopBar.
- SoftlyBottomBar.
- SoundVolumeSlider.
- EnvironmentCard.
- FocusTimer.
- MiniPlayer.

Os componentes deverão respeitar princípios de acessibilidade, incluindo contraste, tamanhos de toque e adaptação ao dimensionamento de texto do Android.

---

## 11. Gerenciamento de dependências

Inicialmente, o aplicativo utilizará construção manual de dependências ou um contêiner simples, caso isso seja suficiente.

Uma biblioteca como Hilt ou Koin poderá ser introduzida quando a quantidade de dependências justificar sua utilização.

O objetivo é evitar complexidade desnecessária durante as primeiras etapas.

---

## 12. Estratégia de testes

### Testes unitários

Validarão:

- Regras de cálculo do temporizador.
- Transições entre estados de foco e pausa.
- Regras de conclusão de sessões.
- Validações de tarefas.
- Regras de combinação e controle de volumes.

### Testes de persistência

Validarão:

- Criação de registros.
- Atualização de registros.
- Exclusão.
- Recuperação dos dados armazenados.

### Testes instrumentados

Validarão:

- Navegação.
- Principais interações da interface.
- Integração com os recursos Android.

### Testes manuais

Serão especialmente importantes para:

- Reprodução simultânea.
- Bluetooth.
- Bloqueio da tela.
- Interrupções por chamadas.
- Comportamento em segundo plano.
- Consumo de recursos.

---

## 13. Estratégia de desenvolvimento

O Softly será implementado incrementalmente.

### Fase 1 — Fundação

- Configuração do projeto.
- Documentação.
- Design system.
- Navegação.

### Fase 2 — Interface inicial

- Tela Início.
- Cards de ambientes.
- Tela de detalhes.
- Componentes compartilhados.

### Fase 3 — Áudio

- Protótipo de reprodução simultânea.
- Controles de volume.
- Mixer de sons.
- Reprodução em segundo plano.

### Fase 4 — Produtividade

- Timer Pomodoro.
- Tarefas.
- Anotações.
- Persistência local.

### Fase 5 — Integração e qualidade

- Integração dos módulos.
- Testes.
- Correções.
- Otimizações.
- Preparação do APK.

---

## 14. Decisões arquiteturais

| ID | Decisão | Justificativa |
|---|---|---|
| ADR-001 | Android nativo | Aproveitar recursos da plataforma |
| ADR-002 | Kotlin + Compose | Desenvolvimento moderno e declarativo |
| ADR-003 | MVVM | Separação entre interface e lógica |
| ADR-004 | Módulo Gradle único inicialmente | Reduzir complexidade |
| ADR-005 | Room | Persistência estruturada |
| ADR-006 | DataStore | Armazenamento de preferências |
| ADR-007 | Motor de áudio desacoplado | Facilitar testes e manutenção |
| ADR-008 | Implementação incremental | Reduzir riscos e retrabalho |
| ADR-009 | Funcionamento offline essencial | Independência de serviços externos |

---

## 15. Princípios de desenvolvimento

Durante a implementação, seguiremos as seguintes diretrizes:

1. Priorizar soluções simples e testáveis.
2. Evitar duplicação desnecessária de código.
3. Manter responsabilidades bem definidas.
4. Não adicionar dependências sem justificativa.
5. Documentar decisões técnicas relevantes.
6. Validar cada funcionalidade antes de avançar.
7. Manter o GitHub atualizado.
8. Preservar a identidade visual aprovada.

---

## 16. Controle de alterações

| Versão | Alteração |
|---|---|
| 1.0 | Definição inicial da arquitetura Android do Softly |

---

**Softly — Seu espaço. Seu ritmo.**