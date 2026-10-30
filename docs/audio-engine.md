# Softly — Arquitetura do Motor de Áudio

**Projeto:** Softly  
**Versão:** 1.0  
**Plataforma:** Android nativo  
**Linguagem:** Kotlin  
**Status:** Planejamento técnico  
**Prioridade:** Alta

---

## 1. Objetivo

O motor de áudio do Softly será responsável por proporcionar experiências sonoras personalizáveis, permitindo que o usuário combine diferentes sons ambientes.

O sistema deverá oferecer reprodução contínua, controle independente de volume e funcionamento em segundo plano.

A implementação deverá priorizar estabilidade, desempenho e baixo consumo de recursos.

---

## 2. Funcionalidades principais

O motor de áudio deverá permitir:

- Reproduzir sons ambientes.
- Reproduzir múltiplos sons simultaneamente.
- Ajustar o volume individual.
- Ativar e desativar sons.
- Interromper todos os sons.
- Reproduzir arquivos em repetição contínua.
- Continuar reproduzindo com a tela bloqueada.
- Identificar erros de carregamento.
- Liberar recursos quando não forem mais necessários.

A reprodução deverá funcionar independentemente do temporizador Pomodoro.

---

## 3. Biblioteca inicial de sons

A primeira versão terá os seguintes ambientes sonoros:

| ID | Som | Categoria |
|---|---|---|
| rain | Chuva | Natureza |
| forest | Floresta | Natureza |
| fireplace | Lareira | Aconchego |
| ocean | Oceano | Natureza |
| storm | Tempestade | Natureza |
| coffee | Cafeteria | Ambiente |
| wind | Vento | Natureza |
| river | Rio | Natureza |

Esses sons serão utilizados individualmente ou combinados.

A disponibilização dependerá da obtenção de arquivos com licença apropriada.

---

## 4. Tecnologias avaliadas

### 4.1. AndroidX Media3 / ExoPlayer

O Media3 oferece recursos para reprodução de mídia e integração com os componentes de mídia do Android.

Vantagens:

- Suporte à reprodução de arquivos de áudio.
- Gerenciamento de estados.
- Reprodução contínua.
- Controle de volume.
- Integração com MediaSession.
- Suporte à reprodução em segundo plano.

Limitação relevante:

Uma única instância convencional de ExoPlayer não deve ser tratada como um mixer capaz de reproduzir várias faixas independentes simultaneamente.

Será necessário avaliar a utilização de múltiplas instâncias ou uma implementação específica de mixagem.

### 4.2. SoundPool

O SoundPool permite reproduzir múltiplos efeitos sonoros com baixa latência.

Entretanto, seus arquivos são decodificados para memória, tornando-o menos adequado para gravações ambientais longas.

Poderá ser utilizado futuramente para efeitos curtos, como alertas.

### 4.3. AudioTrack

O AudioTrack oferece controle mais direto sobre a saída de áudio.

Entretanto, uma implementação de mixagem com AudioTrack exigiria gerenciar buffers, decodificação, sincronização e mistura de amostras.

Por isso, não será a primeira alternativa.

---

## 5. Estratégia técnica inicial

A primeira abordagem será um protótipo utilizando Media3/ExoPlayer.

Cada som ativo poderá possuir uma instância independente de reprodução.

O sistema deverá disponibilizar uma interface única para coordenar essas instâncias.

### Fluxo conceitual

```text
Softly Audio Engine
        |
        v
AudioPlaybackController
        |
        v
AudioPlaybackManager
        |
        +---- Player 1: Chuva
        |         Volume: 70%
        |
        +---- Player 2: Lareira
        |         Volume: 40%
        |
        +---- Player 3: Floresta
                  Volume: 25%
```

Os fluxos de áudio serão combinados pela infraestrutura de áudio do Android.

O aplicativo deverá coordenar os players de maneira centralizada.

Essa estratégia será considerada provisória até a conclusão dos testes.

---

## 6. Protótipo técnico obrigatório

Antes da implementação definitiva, será criado um protótipo para verificar:

1. Reprodução de um arquivo local.
2. Reprodução simultânea de dois arquivos.
3. Reprodução simultânea de quatro arquivos.
4. Ajuste independente dos volumes.
5. Repetição contínua.
6. Interrupção individual.
7. Interrupção global.
8. Liberação dos recursos.

### Critérios de aprovação

O protótipo deverá:

- Reproduzir quatro sons simultaneamente sem falhas perceptíveis nos dispositivos de teste.
- Permitir ajustes individuais de volume.
- Não interromper outros sons ao desativar um canal.
- Não apresentar travamentos da interface.
- Liberar corretamente os recursos ao encerrar a reprodução.
- Não apresentar consumo de memória incompatível com os dispositivos utilizados.

Se os resultados não forem satisfatórios, a arquitetura deverá ser reavaliada antes da implementação definitiva.

---

## 7. Gerenciamento de estados

Cada som poderá apresentar os seguintes estados:

| Estado | Significado |
|---|---|
| IDLE | Não inicializado |
| LOADING | Carregando |
| READY | Preparado |
| PLAYING | Reproduzindo |
| PAUSED | Pausado |
| ERROR | Falha |
| STOPPED | Interrompido |

A interface deverá refletir o estado efetivo do mecanismo de áudio.

Não será permitido indicar que um som está reproduzindo quando o player estiver em erro ou interrompido.

---

## 8. Controle de volume

Cada canal deverá possuir um volume independente.

O intervalo inicial será:

```text
0.0 = Silêncio
0.5 = 50%
1.0 = 100%
```

O volume de cada player deverá ser atualizado sem reinicializar o arquivo.

### Regras

**RA001:** Alterar o volume de um som não deverá modificar o volume dos demais.

**RA002:** O volume deverá permanecer dentro do intervalo permitido.

**RA003:** Desativar um som não deverá interromper os demais.

**RA004:** O volume geral do dispositivo continuará sob controle do Android.

**RA005:** O mecanismo deverá impedir valores inválidos de volume.

---

## 9. Reprodução contínua

Os sons ambientes deverão permitir repetição automática.

Os arquivos utilizados deverão ser selecionados e preparados para reduzir interrupções perceptíveis na transição entre o final e o início.

A implementação deverá avaliar:

- Ausência de silêncios indesejados.
- Qualidade das transições.
- Repetição sem interrupções perceptíveis.
- Comportamento com vários canais ativos.

A reprodução contínua não deverá depender da tela Compose permanecer aberta.

---

## 10. Reprodução em segundo plano

O Softly deverá permitir que os sons continuem sendo reproduzidos quando:

- O usuário navegar entre telas.
- O aplicativo estiver em segundo plano.
- A tela do dispositivo estiver bloqueada.

A abordagem inicial será utilizar um serviço de reprodução baseado em Media3.

O serviço deverá controlar o ciclo de vida dos players e disponibilizar comandos de reprodução.

### Componentes previstos

**AudioPlaybackService**

Responsável pelo ciclo de vida da reprodução em segundo plano.

**AudioPlaybackManager**

Responsável pelo gerenciamento dos canais sonoros.

**AudioPlaybackController**

Contrato utilizado pelos componentes de apresentação.

### Integração com o Android

A implementação deverá considerar:

- MediaSession.
- MediaSessionService.
- Foreground Service do tipo mediaPlayback.
- Notificação de reprodução.
- Permissões exigidas pelas versões Android suportadas.
- Controles de mídia do sistema.
- Encerramento adequado do serviço.

O serviço não deverá permanecer ativo desnecessariamente após o encerramento de todas as reproduções.

---

## 11. Foco de áudio

O Softly deverá respeitar as solicitações de foco de áudio do Android.

Situações previstas:

- Chamadas telefônicas.
- Reprodução iniciada por outro aplicativo.
- Notificações.
- Conexão ou desconexão de dispositivos de áudio.

O gerenciador deverá coordenar a reação de todos os canais a essas situações.

Uma interrupção de foco não deverá resultar em estados inconsistentes entre os players.

As regras específicas de pausa, redução de volume e retomada serão definidas e testadas conforme o comportamento exigido pelo Android.

---

## 12. Gerenciamento de recursos

O sistema deverá evitar manter players desnecessários em memória.

### Diretrizes

- Criar recursos quando necessários.
- Evitar instâncias duplicadas para o mesmo som.
- Liberar players encerrados.
- Evitar carregamento simultâneo desnecessário.
- Tratar falhas de reprodução.
- Evitar operações pesadas na thread principal.

Inicialmente, o protótipo validará até quatro canais simultâneos.

Esse limite poderá ser ajustado conforme os resultados obtidos.

---

## 13. Funcionamento offline

Os sons essenciais deverão estar disponíveis sem internet.

Os arquivos serão distribuídos junto ao aplicativo ou por meio de uma estratégia de instalação local definida durante o desenvolvimento.

### Requisitos

**RA006:** A reprodução dos sons essenciais não dependerá de APIs externas.

**RA007:** A ausência de conexão não deverá impedir o funcionamento do mixer local.

**RA008:** Os recursos deverão possuir identificação estável.

---

## 14. Formatos de áudio

Os formatos iniciais considerados serão:

- OGG.
- AAC.
- MP3.

A escolha definitiva dependerá de testes de compatibilidade, tamanho e qualidade.

### Critérios de seleção

- Suporte nas versões Android utilizadas.
- Qualidade sonora.
- Tamanho dos arquivos.
- Compatibilidade com reprodução contínua.
- Licença de distribuição.

Não será adotado um formato único sem validação.

---

## 15. Direitos autorais

Todos os sons distribuídos com o aplicativo deverão possuir autorização de uso compatível com o projeto.

As fontes e respectivas licenças deverão ser documentadas.

O Softly não deverá distribuir músicas comerciais sem autorização.

Arquivos obtidos de bibliotecas externas deverão passar por verificação antes de serem adicionados ao projeto.

---

## 16. Integração com Jetpack Compose

A interface não deverá gerenciar diretamente instâncias de ExoPlayer.

Os controles visuais enviarão comandos ao ViewModel ou controlador apropriado.

### Fluxo

```text
SoundVolumeSlider
        |
        v
SoundsViewModel
        |
        v
AudioPlaybackController
        |
        v
AudioPlaybackManager
        |
        v
Player correspondente
```

O estado de reprodução deverá ser disponibilizado à interface por meio de um fluxo observável.

A saída visual deverá permanecer sincronizada com o estado real do mecanismo.

---

## 17. Testes

### Testes funcionais

- Reproduzir um som.
- Reproduzir vários sons.
- Alterar volumes.
- Pausar reprodução.
- Interromper um som.
- Interromper todos os sons.
- Reiniciar reprodução.
- Tratar arquivo indisponível.

### Testes de integração

- Navegação entre telas.
- Aplicativo em segundo plano.
- Bloqueio da tela.
- Conexão Bluetooth.
- Desconexão de fones.
- Interrupção por outros aplicativos.

### Testes de desempenho

- Consumo de memória.
- Utilização de CPU.
- Consumo de bateria.
- Tempo de inicialização.
- Estabilidade com múltiplos canais.

---

## 18. Evoluções futuras

Funcionalidades planejadas para versões posteriores:

- Ambientes personalizados.
- Salvamento de combinações sonoras.
- Favoritos.
- Biblioteca ampliada.
- Pacotes adicionais de áudio.
- Transições graduais de volume.
- Perfis automáticos de concentração.
- Integração com o temporizador Pomodoro.

Essas funcionalidades não fazem parte da implementação inicial do motor de áudio.

---

## 19. Decisões técnicas

| ID | Decisão | Status |
|---|---|---|
| AD-001 | Avaliar Media3 como mecanismo inicial | Aprovada |
| AD-002 | Criar protótipo de reprodução simultânea | Aprovada |
| AD-003 | Manter interface desacoplada dos players | Aprovada |
| AD-004 | Implementar reprodução offline essencial | Aprovada |
| AD-005 | Utilizar serviço de mídia para segundo plano | Planejada |
| AD-006 | Validar quatro canais simultâneos | Planejada |
| AD-007 | Avaliar desempenho antes de definir o limite final | Planejada |

---

## 20. Referências técnicas

Documentação oficial Android:

- Media3 — https://developer.android.com/media/media3
- ExoPlayer — https://developer.android.com/media/media3/exoplayer
- Background Playback — https://developer.android.com/media/media3/session/background-playback
- Audio Focus — https://developer.android.com/media/optimize/audio-focus
- SoundPool — https://developer.android.com/reference/android/media/SoundPool

---

## 21. Controle de alterações

| Versão | Alteração |
|---|---|
| 1.0 | Planejamento inicial do motor de áudio e estratégia de validação |

---

**Softly — Seu espaço. Seu ritmo.**