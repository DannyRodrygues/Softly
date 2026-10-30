# Softly — UI Design System

**Projeto:** Softly  
**Versão do documento:** 1.0  
**Plataforma:** Android nativo  
**Framework de interface:** Jetpack Compose  
**Design System:** Material Design 3 personalizado  
**Identidade visual:** Midnight Lavender  
**Status:** Aprovado para implementação

---

## 1. Conceito visual

O Softly é um aplicativo de foco, relaxamento e produtividade que oferece ao usuário um refúgio digital.

Sua identidade visual deve transmitir:

- Aconchego.
- Tranquilidade.
- Imersão.
- Elegância.
- Clareza.
- Concentração.

A interface será inspirada em atmosferas acolhedoras, como noites chuvosas, cafeterias iluminadas, florestas tranquilas e paisagens noturnas.

### Princípio central

**O usuário deve sentir que está entrando em um espaço criado para seu próprio ritmo.**

A interface não deverá apresentar excesso de informações, animações invasivas ou elementos que prejudiquem a concentração.

---

## 2. Identidade da marca

**Nome:** Softly

**Slogan:** Seu espaço. Seu ritmo.

### Personalidade

A marca deverá ser:

- Moderna, mas acolhedora.
- Elegante, sem parecer excessivamente formal.
- Tranquila, sem transmitir monotonia.
- Tecnológica, sem perder a sensação de conforto.

### Logotipo

O logotipo será composto por:

1. Símbolo de três ondas suaves.
2. Nome Softly.
3. Tipografia geométrica com formas arredondadas.

As ondas representam som, equilíbrio e continuidade.

O símbolo deverá funcionar independentemente do nome para utilização no ícone do aplicativo e em elementos da interface.

**Importante:** o mockup aprovado é uma referência visual. O logotipo definitivo deverá ser produzido como recurso próprio antes da publicação.

---

## 3. Paleta de cores — Midnight Lavender

### Cores principais

| Token | HEX | Utilização |
|---|---|---|
| Background | `#101322` | Fundo principal |
| Surface | `#1C2033` | Cards e superfícies |
| Primary | `#B6A4F2` | Botões e destaques |
| Secondary | `#A3C9BA` | Elementos de relaxamento |
| Accent | `#F2BFA5` | Pequenos destaques |
| OnBackground | `#F4F2FA` | Texto principal |
| TextSecondary | `#A6A8BE` | Texto secundário |

### Regras de utilização

A cor lavanda será a principal referência visual da marca.

O azul-noturno deverá predominar nos fundos, enquanto os demais tons serão utilizados de forma moderada.

Não utilizar cores vibrantes em grandes áreas da interface.

Evitar fundos totalmente pretos quando não houver uma justificativa de acessibilidade ou contraste.

### Cores de estado

Além da paleta principal, serão definidos tokens específicos para:

- Erro.
- Sucesso.
- Aviso.
- Elementos desabilitados.
- Indicadores de reprodução.
- Estados de seleção.

Esses tokens deverão ser validados quanto ao contraste antes da implementação.

---

## 4. Temas

### Dark Mode

Será o tema padrão do aplicativo.

Características:

- Fundo azul-noturno.
- Superfícies azul-acinzentadas.
- Textos claros.
- Destaques lavanda.
- Gradientes suaves.
- Imagens atmosféricas.

### Light Mode

Será disponibilizado como alternativa.

O tema claro deverá preservar a personalidade visual da marca, utilizando fundos claros, superfícies suaves e cores adaptadas para garantir legibilidade.

A paleta definitiva do tema claro será definida e validada durante a implementação.

### Preferência do usuário

O aplicativo deverá oferecer:

- Tema escuro.
- Tema claro.
- Seguir configuração do sistema.

A preferência será armazenada utilizando DataStore.

---

## 5. Tipografia

### Família principal

**Manrope**

A família será utilizada nos títulos, botões, navegação e textos gerais.

### Hierarquia tipográfica inicial

| Elemento | Tamanho de referência | Peso |
|---|---|---|
| Título principal | 28 sp | Bold |
| Título de seção | 22 sp | SemiBold |
| Título de card | 18 sp | SemiBold |
| Texto principal | 16 sp | Regular |
| Texto secundário | 14 sp | Regular |
| Legendas | 12 sp | Medium |
| Temporizador | 56 sp | SemiBold |

Os tamanhos serão ajustados conforme os componentes do Material 3 e a acessibilidade do Android.

Não deverão ser utilizados tamanhos fixos que impeçam o dimensionamento adequado do texto.

---

## 6. Layout e espaçamento

### Unidade de referência

O layout utilizará dimensões em `dp`.

### Escala de espaçamento

| Token | Valor |
|---|---|
| ExtraSmall | 4 dp |
| Small | 8 dp |
| Medium | 16 dp |
| Large | 24 dp |
| ExtraLarge | 32 dp |

### Bordas arredondadas

| Componente | Raio inicial |
|---|---|
| Cards pequenos | 12 dp |
| Cards principais | 20 dp |
| Botões | 16 dp |
| Campos de entrada | 12 dp |
| Painéis de destaque | 24 dp |

Os valores são referências iniciais e poderão ser adaptados durante os testes visuais.

### Áreas de toque

Os controles interativos deverão respeitar dimensões mínimas de toque adequadas ao Android.

A interface deverá considerar barras do sistema, recortes da tela e navegação por gestos.

---

## 7. Navegação

A navegação principal será realizada por uma barra inferior.

### Destinos

1. Início.
2. Foco.
3. Atividades.
4. Biblioteca.

A tela de configurações será acessada pelo cabeçalho.

A barra inferior deverá indicar claramente a seção selecionada.

O aplicativo utilizará Navigation Compose para gerenciar os destinos.

---

## 8. Tela Início

### Objetivo

Apresentar os ambientes disponíveis e facilitar o início de uma experiência sonora.

### Elementos

**Cabeçalho**

- Logotipo Softly.
- Acesso às configurações.

**Saudação**

Texto principal:

"Qual é o seu momento agora?"

Texto de apoio:

"Ambientes que te acompanham em cada etapa do seu dia."

**Ambientes destacados**

Cards com imagens cinematográficas:

- Dia de Chuva.
- Refúgio Verde.
- Noite Serena.
- Café & Código.

Cada card apresentará:

- Imagem.
- Nome.
- Descrição curta.
- Ícone representativo.
- Controle de acesso ou reprodução.

**Área complementar**

Seção destinada a rotinas e ambientes personalizados, conforme a disponibilidade da funcionalidade.

### Comportamento

Ao selecionar um card, o usuário será direcionado para a tela de detalhes do ambiente.

---

## 9. Tela de ambiente sonoro

### Objetivo

Permitir controlar a atmosfera sonora selecionada.

### Elementos

**Imagem principal**

Imagem cinematográfica relacionada ao ambiente.

Exemplos:

- Chuva em uma janela.
- Lareira acesa.
- Floresta com neblina.
- Cafeteria iluminada.

**Informações**

- Nome do ambiente.
- Descrição.
- Categorias associadas.

**Mixer de áudio**

Lista de sons disponíveis com:

- Ícone.
- Nome.
- Controle de ativação.
- Controle individual de volume.

**Miniplayer**

Componente compacto que permitirá visualizar o ambiente ativo e acessar os controles principais.

### Estados visuais

- Som ativo.
- Som inativo.
- Carregando.
- Erro de reprodução.
- Reprodução pausada.

As informações exibidas deverão refletir o estado real do mecanismo de áudio.

---

## 10. Tela Foco

### Objetivo

Permitir realizar sessões de concentração utilizando o temporizador Pomodoro.

### Elementos

**Cabeçalho**

Título: Foco

Descrição:

"Mais presença. Mais resultados."

**Seletor de modo**

- Foco.
- Pausa.

**Temporizador**

Elemento circular com:

- Tempo restante.
- Indicador visual de progresso.
- Estado da sessão.
- Informações sobre ciclos concluídos.

**Controles**

- Iniciar.
- Pausar.
- Retomar.
- Reiniciar.

**Tarefa atual**

Card opcional contendo a tarefa associada à sessão.

### Animações

O progresso circular deverá ser atualizado de maneira suave, sem provocar recomposições desnecessárias em toda a interface.

---

## 11. Tela Atividades

### Objetivo

Organizar tarefas e anotações.

### Organização

A tela utilizará duas abas:

**Tarefas | Anotações**

### Tarefas

Cada item poderá apresentar:

- Título.
- Indicador de conclusão.
- Ações de edição e exclusão.

### Anotações

Cada anotação poderá apresentar:

- Título, quando informado.
- Prévia do conteúdo.
- Data de atualização.
- Ações disponíveis.

### Estados vazios

Quando não existirem registros, a interface deverá apresentar mensagens acolhedoras e orientações simples.

Exemplo:

"Seu espaço está livre. Que tal começar com uma pequena tarefa?"

---

## 12. Tela Biblioteca

### Objetivo

Organizar os recursos sonoros disponíveis.

### Elementos

- Categorias de sons.
- Lista de ambientes predefinidos.
- Acesso aos detalhes de cada ambiente.
- Indicação dos recursos disponíveis offline.

Em versões futuras, a biblioteca poderá incluir ambientes personalizados, favoritos e novos pacotes sonoros.

---

## 13. Componentes reutilizáveis

Serão criados progressivamente os seguintes componentes:

### SoftlyButton

Botão principal que utiliza os tokens do design system.

### SoftlyCard

Card reutilizável com superfícies e bordas padronizadas.

### EnvironmentCard

Card visual destinado à apresentação de ambientes.

### SoundVolumeSlider

Controle de volume individual.

### FocusTimer

Componente visual do temporizador Pomodoro.

### SoftlyBottomBar

Barra inferior de navegação.

### SoftlyMiniPlayer

Componente compacto de reprodução.

### SoftlyTopBar

Cabeçalho reutilizável.

Os componentes serão implementados somente quando necessários.

---

## 14. Imagens e recursos visuais

O Softly utilizará imagens de ambientes acolhedores e cinematográficos.

### Direção artística

- Iluminação suave.
- Tons noturnos.
- Luzes quentes.
- Profundidade de campo.
- Paisagens tranquilas.
- Ambientes internos aconchegantes.

### Regras

As imagens deverão:

- Possuir direitos de utilização adequados.
- Ser otimizadas para dispositivos móveis.
- Evitar tamanhos excessivos.
- Manter boa legibilidade dos textos sobrepostos.
- Preservar proporções adequadas aos cards.

Imagens geradas por inteligência artificial poderão ser utilizadas, desde que sejam avaliadas quanto à qualidade e adequação ao aplicativo.

---

## 15. Animações

As animações deverão reforçar a sensação de tranquilidade.

### Permitidas

- Transições suaves entre telas.
- Mudanças discretas de gradiente.
- Animações leves de botões.
- Indicadores de reprodução.
- Progresso do temporizador.

### Evitar

- Movimentos rápidos.
- Efeitos piscantes.
- Animações excessivamente longas.
- Vídeos contínuos de fundo no MVP.
- Efeitos que prejudiquem o desempenho.

A implementação deverá considerar configurações de acessibilidade e redução de movimento quando aplicável.

---

## 16. Acessibilidade

A interface deverá:

- Oferecer descrições acessíveis para ícones interativos.
- Suportar aumento do tamanho dos textos.
- Manter contraste adequado.
- Possuir áreas de toque confortáveis.
- Evitar depender exclusivamente de cores para indicar estados.
- Oferecer feedback claro sobre ações e erros.

As combinações de cores deverão ser verificadas durante a implementação.

---

## 17. Responsividade

A interface será desenvolvida inicialmente para smartphones Android.

Deverá adaptar-se a:

- Diferentes resoluções.
- Diferentes densidades de tela.
- Variações de proporção.
- Configurações de acessibilidade.

O uso em tablets e telas maiores poderá receber layouts específicos em versões posteriores.

---

## 18. Critérios de validação visual

Uma tela será considerada visualmente concluída quando:

1. Seguir os tokens definidos no design system.
2. Apresentar hierarquia visual clara.
3. Preservar a identidade Midnight Lavender.
4. Adaptar-se corretamente ao dispositivo de teste.
5. Não apresentar textos cortados ou componentes sobrepostos.
6. Utilizar componentes reutilizáveis quando apropriado.
7. Manter estados interativos coerentes.
8. Apresentar contraste e legibilidade adequados.
9. Funcionar com diferentes configurações de tamanho de fonte.
10. Estar visualmente alinhada ao mockup aprovado, respeitando as necessidades reais de implementação.

---

## 19. Referências visuais

O mockup aprovado do Softly será utilizado como referência principal.

Ele apresenta:

- Três telas Android.
- Identidade Midnight Lavender.
- Ambientes cinematográficos.
- Mixer de áudio.
- Temporizador Pomodoro.
- Navegação inferior.
- Componentes arredondados.
- Logotipo com ondas.

O mockup representa a direção artística, não uma especificação de posicionamento exato de pixels.

---

## 20. Controle de alterações

| Versão | Alteração |
|---|---|
| 1.0 | Definição inicial do design system e das telas principais |

---

**Softly — Seu espaço. Seu ritmo.**