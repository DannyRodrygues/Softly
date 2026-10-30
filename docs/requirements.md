# Softly — Requisitos do Aplicativo

**Projeto:** Softly  
**Versão do documento:** 1.0  
**Plataforma:** Android nativo  
**Linguagem:** Kotlin  
**Interface:** Jetpack Compose  
**Arquitetura:** MVVM com separação entre apresentação, domínio e dados  
**Status:** Planejamento

---

## 1. Visão geral

O Softly é um aplicativo Android de concentração, relaxamento e produtividade.

Seu objetivo é oferecer um espaço digital acolhedor, no qual o usuário possa personalizar ambientes sonoros, realizar sessões de concentração e organizar suas atividades.

O aplicativo terá identidade visual própria, baseada em uma experiência minimalista e cinematográfica.

**Slogan:** Seu espaço. Seu ritmo.

## 2. Objetivos

- Proporcionar experiências sonoras personalizáveis.
- Auxiliar na concentração e no relaxamento.
- Oferecer ferramentas simples de produtividade.
- Permitir a utilização das funcionalidades essenciais sem conexão com a internet.
- Manter uma experiência visual consistente, acessível e intuitiva.

## 3. Escopo do MVP

A primeira versão funcional deverá incluir:

1. Tela inicial com ambientes sonoros predefinidos.
2. Reprodução simultânea de sons ambientes.
3. Controle individual de volume.
4. Temporizador Pomodoro configurável.
5. Gerenciamento de tarefas.
6. Gerenciamento de anotações.
7. Armazenamento local.
8. Configurações básicas do aplicativo.

Funcionalidades como sincronização em nuvem, autenticação, estatísticas avançadas e integração com plataformas de música ficam fora do MVP.

## 4. Requisitos funcionais

### 4.1. Tela inicial e navegação

**RF001:** O aplicativo deverá apresentar uma tela inicial com os ambientes sonoros disponíveis.

**RF002:** O usuário deverá conseguir navegar entre Início, Foco, Atividades e Biblioteca.

**RF003:** Cada ambiente deverá apresentar nome, imagem ilustrativa e descrição.

**RF004:** O usuário deverá conseguir selecionar um ambiente para visualizar seus sons.

### 4.2. Reprodução de áudio

**RF005:** O aplicativo deverá permitir a reprodução de sons ambientes.

**RF006:** O usuário deverá conseguir reproduzir dois ou mais sons simultaneamente.

**RF007:** Cada som deverá possuir controle individual de volume.

**RF008:** O usuário deverá conseguir ativar e desativar cada som independentemente.

**RF009:** O aplicativo deverá oferecer um comando para interromper todos os sons.

**RF010:** Os sons deverão permitir reprodução contínua, utilizando arquivos preparados para repetição.

**RF011:** O aplicativo deverá permitir reprodução em segundo plano, inclusive com a tela bloqueada, respeitando as restrições do Android.

**RF012:** O aplicativo deverá tratar interrupções e solicitações de foco de áudio de outros aplicativos.

### 4.3. Temporizador Pomodoro

**RF013:** O usuário deverá conseguir iniciar uma sessão de concentração.

**RF014:** O usuário deverá conseguir pausar e retomar uma sessão.

**RF015:** O usuário deverá conseguir reiniciar o temporizador.

**RF016:** O usuário deverá conseguir configurar as durações de foco e pausa.

**RF017:** O aplicativo deverá indicar visualmente o tempo restante.

**RF018:** O aplicativo deverá emitir um alerta ao finalizar uma sessão.

**RF019:** O aplicativo deverá registrar a quantidade de ciclos de foco concluídos.

**RF020:** O usuário deverá conseguir associar uma tarefa a uma sessão de concentração.

### 4.4. Gerenciamento de tarefas

**RF021:** O usuário deverá conseguir cadastrar tarefas.

**RF022:** O usuário deverá conseguir editar tarefas existentes.

**RF023:** O usuário deverá conseguir excluir tarefas.

**RF024:** O usuário deverá conseguir marcar tarefas como concluídas.

**RF025:** As tarefas deverão permanecer armazenadas após o encerramento do aplicativo.

### 4.5. Anotações

**RF026:** O usuário deverá conseguir criar anotações.

**RF027:** O usuário deverá conseguir editar anotações.

**RF028:** O usuário deverá conseguir excluir anotações.

**RF029:** As anotações deverão ser armazenadas localmente.

### 4.6. Preferências

**RF030:** O aplicativo deverá armazenar as configurações de foco e pausa.

**RF031:** O aplicativo deverá armazenar as preferências de aparência do usuário.

**RF032:** O aplicativo deverá oferecer uma opção para selecionar o tema claro ou escuro.

## 5. Funcionalidades previstas para versões futuras

Os requisitos abaixo não fazem parte do MVP inicial.

**RF033:** Permitir criar ambientes sonoros personalizados.

**RF034:** Permitir salvar combinações de sons e volumes.

**RF035:** Permitir marcar ambientes como favoritos.

**RF036:** Apresentar estatísticas de produtividade.

**RF037:** Disponibilizar uma biblioteca ampliada de músicas e sons.

**RF038:** Permitir sincronização de dados entre dispositivos.

## 6. Requisitos não funcionais

### 6.1. Desempenho

**RNF001:** A interface deverá permanecer responsiva durante a reprodução de áudio.

**RNF002:** A aplicação deverá evitar o carregamento desnecessário de arquivos sonoros.

**RNF003:** Recursos de áudio deverão ser liberados quando não forem mais necessários.

### 6.2. Compatibilidade

**RNF004:** A versão inicial terá como requisito mínimo Android 8.0 (API 26).

**RNF005:** A interface deverá adaptar-se a diferentes dimensões de telas Android.

**RNF006:** O aplicativo deverá respeitar o ciclo de vida dos componentes Android.

### 6.3. Persistência

**RNF007:** As tarefas, anotações e sessões deverão utilizar armazenamento local estruturado.

**RNF008:** As preferências do aplicativo deverão ser armazenadas utilizando DataStore.

**RNF009:** As operações de armazenamento não deverão bloquear a interface principal.

### 6.4. Usabilidade e acessibilidade

**RNF010:** A interface deverá manter consistência visual entre suas telas.

**RNF011:** Os elementos interativos deverão apresentar identificação acessível.

**RNF012:** O aplicativo deverá oferecer contraste adequado entre textos e fundos.

**RNF013:** A interface deverá considerar diferentes configurações de tamanho de fonte e escala de exibição do Android.

### 6.5. Funcionamento offline

**RNF014:** O temporizador, as tarefas e as anotações deverão funcionar sem conexão com a internet.

**RNF015:** Os sons essenciais deverão estar disponíveis offline.

### 6.6. Segurança e privacidade

**RNF016:** A versão inicial não deverá exigir criação de conta.

**RNF017:** Os dados pessoais de produtividade deverão permanecer no dispositivo, salvo funcionalidades futuras expressamente autorizadas pelo usuário.

**RNF018:** O aplicativo deverá solicitar apenas as permissões necessárias para as funcionalidades implementadas.

### 6.7. Qualidade

**RNF019:** As regras de negócio deverão ser implementadas de forma testável.

**RNF020:** O projeto deverá manter documentação técnica versionada.

**RNF021:** O código deverá utilizar nomes claros e organização consistente entre camadas.

## 7. Regras de negócio

**RN001:** A reprodução de sons ambientes deverá funcionar independentemente do temporizador Pomodoro.

**RN002:** Interromper um som não deverá interromper os demais sons ativos.

**RN003:** A duração das sessões deverá ser configurável pelo usuário.

**RN004:** Somente sessões de foco concluídas deverão incrementar o contador de ciclos completos.

**RN005:** O usuário poderá utilizar o temporizador sem selecionar uma tarefa.

**RN006:** A exclusão de uma tarefa não deverá apagar automaticamente os registros históricos de sessões já realizadas.

**RN007:** As configurações de volume deverão respeitar os limites definidos pelo mecanismo de áudio.

**RN008:** Quando uma reprodução for interrompida pelo sistema, o aplicativo deverá manter um estado de interface coerente com a reprodução efetiva.

## 8. Arquitetura prevista

A implementação deverá utilizar:

- Kotlin.
- Jetpack Compose.
- Material Design 3.
- ViewModel.
- StateFlow e Coroutines.
- Room.
- DataStore.
- AndroidX Media3.
- Navigation Compose.

A separação inicial será organizada em:

- **Presentation:** telas, componentes e ViewModels.
- **Domain:** modelos, contratos e regras de negócio.
- **Data:** repositórios, banco de dados e preferências.
- **Playback:** controle e serviços de reprodução de áudio.

As dependências e suas versões serão definidas durante a configuração técnica.

## 9. Identidade visual

O Softly utilizará a identidade Midnight Lavender.

| Elemento | Cor |
|---|---|
| Fundo principal | `#101322` |
| Superfícies | `#1C2033` |
| Primária | `#B6A4F2` |
| Secundária | `#A3C9BA` |
| Destaques | `#F2BFA5` |
| Texto principal | `#F4F2FA` |
| Texto secundário | `#A6A8BE` |

A tipografia principal prevista será Manrope.

A interface utilizará imagens atmosféricas, gradientes suaves, cards arredondados e animações discretas.

## 10. Critérios de conclusão do MVP

O MVP poderá ser considerado funcional quando:

- O aplicativo iniciar e permitir navegar entre as telas principais.
- O usuário conseguir selecionar e reproduzir ambientes sonoros.
- Dois ou mais sons puderem tocar simultaneamente.
- Os volumes puderem ser ajustados individualmente.
- A reprodução em segundo plano funcionar nos dispositivos de teste.
- O temporizador permitir iniciar, pausar, retomar e reiniciar sessões.
- Tarefas e anotações puderem ser criadas, editadas, excluídas e recuperadas após reiniciar o aplicativo.
- As configurações essenciais forem preservadas.
- Os principais fluxos forem validados por testes.
- Não existirem falhas críticas conhecidas que impeçam o uso das funcionalidades principais.

## 11. Controle de alterações

| Versão | Alteração |
|---|---|
| 1.0 | Definição inicial dos requisitos funcionais, não funcionais e regras de negócio |

---

**Softly — Seu espaço. Seu ritmo.**