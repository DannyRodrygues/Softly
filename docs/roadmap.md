# Softly — Roadmap de Desenvolvimento

**Projeto:** Softly  
**Versão do documento:** 1.0  
**Plataforma:** Android nativo  
**Linguagem:** Kotlin  
**Interface:** Jetpack Compose  
**Arquitetura:** MVVM + Clean Architecture simplificada  
**Status:** Em desenvolvimento

---

## 1. Objetivo

Este documento define as etapas de desenvolvimento do Softly, estabelecendo prioridades, entregas e critérios de conclusão.

O desenvolvimento será incremental, priorizando funcionalidades essenciais, estabilidade e qualidade.

Cada fase deverá ser validada antes do início da próxima.

## 2. Visão do produto

O Softly será um aplicativo Android de concentração, relaxamento e produtividade.

O usuário poderá criar uma atmosfera acolhedora combinando sons ambientes, utilizando um temporizador Pomodoro e organizando tarefas e anotações.

**Slogan:** Seu espaço. Seu ritmo.

### Princípios

- Interface intuitiva e acolhedora.
- Identidade visual original.
- Funcionamento offline para recursos essenciais.
- Reprodução de áudio estável.
- Arquitetura organizada e testável.
- Desenvolvimento documentado.
- Evolução contínua.

---

## 3. Estratégia de desenvolvimento

O desenvolvimento será dividido em fases.

Cada fase deverá possuir:

1. Objetivos definidos.
2. Entregas verificáveis.
3. Testes apropriados.
4. Critérios de conclusão.
5. Registro das alterações no GitHub.

Não serão adicionadas funcionalidades fora do escopo sem avaliar seus impactos.

---

## 4. Fase 0 — Fundação do projeto

**Status:** Em andamento

### Objetivos

Preparar o ambiente de desenvolvimento, o versionamento e a documentação.

### Entregas

- [x] Criar projeto Android nativo.
- [x] Configurar Kotlin e Jetpack Compose.
- [x] Sincronizar o Gradle.
- [x] Inicializar o Git.
- [x] Criar repositório no GitHub.
- [x] Realizar o primeiro commit e push.
- [x] Definir identidade visual.
- [x] Criar `docs/requirements.md`.
- [x] Criar `docs/architecture.md`.
- [x] Criar `docs/ui-design.md`.
- [x] Criar `docs/audio-engine.md`.
- [ ] Finalizar `docs/roadmap.md`.
- [ ] Criar README inicial.
- [ ] Registrar o marco de documentação no GitHub.

### Critério de conclusão

Projeto criado, compilando e versionado, com documentação inicial disponível no repositório.

---

## 5. Fase 1 — Design System e estrutura da aplicação

**Status:** Pendente

### Objetivos

Implementar a identidade visual Midnight Lavender e estabelecer a navegação.

### Entregas

- [ ] Revisar a configuração do Gradle.
- [ ] Configurar as dependências necessárias.
- [ ] Implementar a paleta Midnight Lavender.
- [ ] Configurar a tipografia.
- [ ] Personalizar o Material 3.
- [ ] Criar componentes básicos reutilizáveis.
- [ ] Configurar Navigation Compose.
- [ ] Criar a estrutura inicial das telas.
- [ ] Implementar a navegação inferior.

### Critério de conclusão

Aplicativo executando com a identidade visual básica, navegação funcional e ausência de erros de compilação.

---

## 6. Fase 2 — Protótipo técnico do motor de áudio

**Status:** Pendente

**Prioridade:** Crítica

### Objetivos

Validar a reprodução simultânea de sons antes da implementação definitiva.

### Entregas

- [ ] Selecionar arquivos sonoros de teste com licença adequada.
- [ ] Implementar reprodução de um som.
- [ ] Implementar reprodução simultânea de dois sons.
- [ ] Testar quatro canais simultâneos.
- [ ] Implementar controle individual de volume.
- [ ] Implementar repetição contínua.
- [ ] Implementar parada individual.
- [ ] Implementar interrupção de todos os sons.
- [ ] Monitorar consumo de memória e CPU.
- [ ] Documentar os resultados.
- [ ] Confirmar ou revisar a estratégia de reprodução.

### Critério de conclusão

Quatro sons reproduzidos simultaneamente, com volumes independentes, sem falhas perceptíveis ou problemas críticos de desempenho nos dispositivos de teste.

### Risco principal

A solução inicial baseada em múltiplos players poderá exigir ajustes ou substituição caso apresente consumo excessivo de recursos.

---

## 7. Fase 3 — Experiência de ambientes sonoros

**Status:** Pendente

### Objetivos

Transformar o protótipo de áudio em uma funcionalidade integrada à interface.

### Entregas

- [ ] Criar a tela Início.
- [ ] Implementar cards de ambientes.
- [ ] Criar a tela de detalhes de ambiente.
- [ ] Implementar controles de reprodução.
- [ ] Implementar controles individuais de volume.
- [ ] Exibir estados de carregamento e erro.
- [ ] Implementar um miniplayer.
- [ ] Integrar interface e motor de áudio.
- [ ] Testar transições entre telas.

### Critério de conclusão

Usuário conseguindo selecionar um ambiente, iniciar a reprodução, ajustar volumes e navegar pelo aplicativo sem interromper indevidamente os sons.

---

## 8. Fase 4 — Reprodução em segundo plano

**Status:** Pendente

### Objetivos

Garantir que a reprodução funcione adequadamente fora da tela principal.

### Entregas

- [ ] Implementar serviço de reprodução.
- [ ] Integrar MediaSession conforme a arquitetura escolhida.
- [ ] Configurar notificações de mídia.
- [ ] Implementar gerenciamento de foco de áudio.
- [ ] Testar bloqueio de tela.
- [ ] Testar reprodução em segundo plano.
- [ ] Testar interrupções por outros aplicativos.
- [ ] Testar dispositivos Bluetooth.
- [ ] Validar encerramento e liberação de recursos.

### Critério de conclusão

Reprodução estável em segundo plano, com gerenciamento correto dos recursos e respeito às regras do Android.

---

## 9. Fase 5 — Temporizador Pomodoro

**Status:** Pendente

### Objetivos

Implementar sessões configuráveis de foco e descanso.

### Entregas

- [ ] Criar modelo de sessão.
- [ ] Implementar o controlador do temporizador.
- [ ] Implementar iniciar.
- [ ] Implementar pausar.
- [ ] Implementar retomar.
- [ ] Implementar reiniciar.
- [ ] Configurar duração de foco.
- [ ] Configurar duração de pausa.
- [ ] Implementar indicador circular de progresso.
- [ ] Implementar alerta de conclusão.
- [ ] Registrar ciclos concluídos.
- [ ] Testar comportamento em segundo plano.

### Critério de conclusão

Temporizador funcionando corretamente, inclusive após mudanças de tela e interrupções normais do ciclo de vida Android.

---

## 10. Fase 6 — Tarefas e anotações

**Status:** Pendente

### Objetivos

Oferecer ferramentas locais de produtividade.

### Entregas

- [ ] Configurar Room.
- [ ] Criar entidades de tarefas.
- [ ] Criar DAOs.
- [ ] Implementar repositórios.
- [ ] Criar tela de tarefas.
- [ ] Implementar cadastro.
- [ ] Implementar edição.
- [ ] Implementar exclusão.
- [ ] Implementar conclusão de tarefas.
- [ ] Criar entidades de anotações.
- [ ] Implementar gerenciamento de anotações.
- [ ] Associar tarefas a sessões de foco.
- [ ] Testar persistência dos dados.

### Critério de conclusão

Tarefas e anotações funcionando com armazenamento local e recuperação correta após reiniciar o aplicativo.

---

## 11. Fase 7 — Preferências e personalização

**Status:** Pendente

### Objetivos

Permitir configurações básicas da experiência do usuário.

### Entregas

- [ ] Configurar DataStore.
- [ ] Implementar preferências do timer.
- [ ] Implementar preferência de tema.
- [ ] Criar tela de configurações.
- [ ] Implementar Dark Mode.
- [ ] Implementar Light Mode.
- [ ] Implementar opção de seguir o sistema.
- [ ] Validar persistência das preferências.

### Critério de conclusão

Preferências funcionando e permanecendo armazenadas após o encerramento do aplicativo.

---

## 12. Fase 8 — Integração e qualidade

**Status:** Pendente

### Objetivos

Validar o funcionamento conjunto dos módulos e preparar o MVP.

### Entregas

- [ ] Revisar navegação.
- [ ] Validar estados da interface.
- [ ] Executar testes unitários.
- [ ] Executar testes instrumentados essenciais.
- [ ] Testar funcionamento offline.
- [ ] Testar desempenho.
- [ ] Testar acessibilidade.
- [ ] Revisar permissões Android.
- [ ] Validar tratamento de erros.
- [ ] Corrigir problemas identificados.
- [ ] Revisar documentação.

### Critério de conclusão

MVP funcionando sem falhas críticas conhecidas e com os principais fluxos validados.

---

## 13. Fase 9 — Distribuição inicial

**Status:** Pendente

### Objetivos

Preparar uma versão instalável para testes.

### Entregas

- [ ] Configurar versão do aplicativo.
- [ ] Revisar nome e identidade visual.
- [ ] Criar ícone definitivo.
- [ ] Revisar recursos e licenças.
- [ ] Gerar APK de teste.
- [ ] Instalar em dispositivo físico.
- [ ] Executar testes de aceitação.
- [ ] Atualizar README.
- [ ] Registrar versão no GitHub.

### Critério de conclusão

APK funcional, testado em dispositivo físico e acompanhado de documentação atualizada.

---

## 14. Versões futuras

Após a validação do MVP, poderão ser desenvolvidos:

### Versão 1.1

- Ambientes personalizados.
- Salvamento de combinações sonoras.
- Favoritos.

### Versão 1.2

- Estatísticas de concentração.
- Histórico de sessões.
- Indicadores de produtividade.

### Versão 1.3

- Biblioteca ampliada de sons.
- Pacotes sonoros adicionais.
- Melhorias de personalização.

### Versões posteriores

- Sincronização em nuvem.
- Backup.
- Recursos multiplataforma, caso exista justificativa.

As versões e funcionalidades poderão ser ajustadas conforme os testes e a evolução do produto.

---

## 15. Critérios gerais de qualidade

Uma fase será considerada concluída quando:

1. Os requisitos correspondentes estiverem implementados.
2. O projeto compilar sem erros.
3. Os testes aplicáveis forem executados.
4. Não existirem falhas críticas conhecidas.
5. A documentação estiver atualizada.
6. As alterações estiverem registradas no Git.

A conclusão de uma fase não deverá depender apenas da aparência visual.

---

## 16. Controle de progresso

| Fase | Descrição | Status |
|---|---|---|
| 0 | Fundação | Em andamento |
| 1 | Design System e navegação | Pendente |
| 2 | Protótipo de áudio | Pendente |
| 3 | Ambientes sonoros | Pendente |
| 4 | Reprodução em segundo plano | Pendente |
| 5 | Pomodoro | Pendente |
| 6 | Tarefas e anotações | Pendente |
| 7 | Preferências | Pendente |
| 8 | Integração e testes | Pendente |
| 9 | Distribuição | Pendente |

---

## 17. Registro de decisões

| ID | Decisão |
|---|---|
| RD001 | Desenvolvimento Android nativo |
| RD002 | Kotlin e Jetpack Compose |
| RD003 | MVP com funcionamento offline essencial |
| RD004 | Validação antecipada do motor de áudio |
| RD005 | Desenvolvimento incremental |
| RD006 | Documentação versionada no GitHub |
| RD007 | Priorização de desempenho e estabilidade |

---

## 18. Controle de alterações

| Versão | Descrição |
|---|---|
| 1.0 | Planejamento inicial das fases de desenvolvimento |

---

**Softly — Seu espaço. Seu ritmo.**