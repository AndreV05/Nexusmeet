# NexusMeet - Escopo e Justificativas

## 1. Definição do Produto e Problema

**Produto:** 
*NexusMeet* – Uma plataforma inteligente de gestão de reuniões corporativas focada em agendamento otimizado via IA, transcrição automatizada e extração de plano de ação.

**Problema:** 
Equipes corporativas perdem, em média, 30% do seu tempo útil tentando conciliar agendas, documentando atas manualmente e rastreando tarefas (follow-ups) que se perdem após as reuniões. Há uma clara ineficiência administrativa e quebra de produtividade devido à falta de centralização das informações discutidas e decisões tomadas.

## 2. Personas e Stakeholders

### Personas
* **Persona 1: Helena (Gerente de Produto)**
  * *Perfil:* Lida com múltiplas equipes e tem a agenda sempre lotada. 
  * *Necessidade:* Precisa marcar reuniões rapidamente e garantir que as decisões sejam documentadas sem esforço manual.
* **Persona 2: Carlos (Desenvolvedor Sênior)**
  * *Perfil:* Focado em código, detesta interrupções e reuniões longas sem propósito.
  * *Necessidade:* Quer saber exatamente o que precisa fazer (tarefas) sem precisar ler uma ata de 5 páginas.

### Stakeholders
* **Diretor de TI:** Preocupa-se com a segurança dos dados, custos de infraestrutura e viabilidade de integração com ferramentas já existentes (SSO, Google Workspace, Jira).
* **Diretor de RH:** Focado na adesão da ferramenta pelos colaboradores e na redução do esgotamento causado pelo excesso de reuniões ("Zoom fatigue").

## 3. Justificativa Técnica das Decisões

A priorização do backlog do *NexusMeet* foi fundamentada em diretrizes de mitigação de riscos técnicos, entrega rápida de valor e gestão de escopo. Utilizou-se a técnica MoSCoW para separar estritamente o que é essencial para o funcionamento do fluxo principal (MVP) daquilo que representa melhorias incrementais ou desvios complexos de engenharia.

**1. Foco do Minimum Viable Product (Must Have):**
As histórias classificadas como "Must Have" formam o núcleo indissociável da proposta de valor. Sem o login seguro via SSO e a leitura de calendário, a funcionalidade principal de agendamento por IA seria impossível, pois o algoritmo depende do consumo de dados de disponibilidade. Da mesma forma, a gravação e a transcrição alimentam o modelo de linguagem que gera o resumo automatizado. Tecnicamente, este fluxo exige a integração com APIs de calendário e o uso de modelos de processamento de linguagem natural (NLP) em nuvem. Garantir essa infraestrutura é a prioridade zero do ciclo de desenvolvimento, validando o modelo de negócio imediatamente.

**2. Automação de Processos e Escalabilidade (Should Have):**
Funcionalidades como extração de tarefas e integração com o Jira adicionam alto valor, mas sua ausência não impede o uso primário do sistema. Elas requerem maior refinamento na lógica de *Machine Learning*, especialmente no reconhecimento de entidades nomeadas (NER) para associar comandos a usuários específicos. Foram priorizadas logo após o MVP pois atendem diretamente à dor de desenvolvedores e da gerência de TI, consolidando a plataforma como um *hub* de produtividade.

**3. Funcionalidades Acessórias (Could Have):**
Itens como exportação em PDF, comandos de voz estruturados e painéis gerenciais foram alocados como "Could Have". Do ponto de vista técnico, a criação de dashboards analíticos exige a implementação de um pipeline de dados secundário e ferramentas de visualização que consumiriam tempo de desenvolvimento na fase inicial. 

**4. Redução de Risco e Custo Operacional (Won't Have):**
Decisões drásticas foram tomadas para proteger o orçamento e o escopo. A escolha de **não** hospedar vídeos em infraestrutura própria elimina um custo massivo de servidores (armazenamento e processamento). O sistema atuará de forma *headless* com relação à infraestrutura de vídeo, delegando o streaming para plataformas terceiras consolidadas (Zoom/Teams) e focando apenas no processamento de texto. Similarmente, a tradução simultânea de áudio com baixa latência adicionaria uma complexidade proibitiva para esta fase, sendo postergada para futuros roadmaps.

---

## Execução da Sprint 1

**Duração da Sprint:** 2 Semanas (10 dias úteis)

### 1. Sprint Planning

**Objetivo da Sprint:**  
Estabelecer a infraestrutura inicial de acesso seguro ao sistema e a integração bidirecional com calendários corporativos, formando a base de dados estrutural indispensável para o futuro motor de agendamento por Inteligência Artificial.

**Histórias Selecionadas e Sprint Backlog:**  
Para atingir o objetivo, a equipa selecionou as tarefas fundamentais de maior risco técnico do MVP (Must Have), utilizando a sequência de *Fibonacci* para estimar os *Story Points* (SP).

| ID | História de Usuário | Critérios de Aceitação | Pontos (SP) |
| :--- | :--- | :--- | :--- |
| **US01** | Como utilizador, quero fazer login utilizando o SSO corporativo (Google/Microsoft) para aceder ao sistema com segurança. | 1. Autenticação via OAuth2.<br>2. Bloqueio se credenciais forem revogadas.<br>3. Criação de perfil no 1º login. | 5 SP |
| **US02** | Como utilizador, quero sincronizar a minha agenda profissional para que o sistema leia os meus horários livres. | 1. Sincronização bidirecional.<br>2. Atualização de status em tempo real. | 8 SP |
| **US06** | Como organizador, quero poder cancelar ou reagendar a reunião com um clique, notificando todos. | 1. Remoção automática nas agendas.<br>2. Disparo de e-mail de notificação. | 3 SP |
| **Total** | | | **16 SP** |

### 2. Definição de Pronto (Definition of Done - DoD)
Uma história de utilizador só é considerada "Pronta" na Sprint atual se cumprir todos os seguintes critérios:
* O código foi desenvolvido, revisto por pelo menos um colega (*Pull Request* aprovado) e fundido na ramificação principal.
* A cobertura de testes unitários da nova funcionalidade é superior a 80%.
* Todos os critérios de aceitação específicos da história foram validados e testados.
* A funcionalidade foi implementada e está operacional no ambiente de *Staging* (Homologação).
* Não existem defeitos (*bugs*) impeditivos conhecidos.

### 3. Registo da Execução da Sprint e Acompanhamento
A execução foi acompanhada diariamente (*Daily Scrum*) e o progresso foi registado no painel Kanban (GitHub Projects). O fluxo de trabalho decorreu da seguinte forma:
* **Dias 1 a 3:** Configuração da infraestrutura do projeto e implementação do *backend* para autenticação OAuth2 (US01).
* **Dias 4 a 5:** Finalização do *frontend* do ecrã de login e validação dos tokens de acesso. A **US01 foi movida para *Done*** no 5º dia.
* **Dias 6 a 8:** Foco intensivo na US02. A equipa enfrentou um desafio técnico com as permissões da Microsoft Graph API, o que exigiu investigação extra (*Spike*). A sincronização foi concluída e a **US02 movida para *Done*** no 8º dia.
* **Dia 9:** Implementação da lógica de exclusão de eventos e disparo de e-mails via SMTP (US06). Tarefa concluída rapidamente devido à arquitetura estabelecida nos dias anteriores. **US06 movida para *Done***.
* **Dia 10:** Testes finais de integração no ambiente de *Staging*, verificação da Definição de Pronto (DoD) e preparação para a *Review*.

### 4. Sprint Review
* **Participantes:** Equipa de Desenvolvimento, Product Owner e Diretor de TI (Stakeholder).
* **Resultados Apresentados:** A equipa demonstrou o acesso ao NexusMeet através de uma conta Google simulada, a importação instantânea da agenda e o cancelamento de um evento com notificação por e-mail recebida em tempo real.
* **Feedback e Aceitação:** O Diretor de TI aprovou a implementação da segurança OAuth2 (US01) e o desempenho da API de calendário (US02 e US06). Todas as histórias entregues cumpriram a DoD. O objetivo da Sprint foi considerado **100% atingido**.

### 5. Retrospectiva da Sprint
Realizada imediatamente após a *Review*, a equipa levantou os seguintes pontos para melhoria contínua:
* **O que correu bem:** A arquitetura do sistema provou ser escalável. A comunicação durante o bloqueio com a API da Microsoft foi rápida e eficiente.
* **O que pode ser melhorado:** O processo de implantação (*deploy*) para o ambiente de *Staging* foi manual e consumiu tempo desnecessário no Dia 10.
* **Plano de Ação para a Sprint 2:** A equipa técnica comprometeu-se a configurar um fluxo básico de CI/CD (Integração e Entrega Contínuas) através do GitHub Actions já no primeiro dia da próxima Sprint, para automatizar as implantações.

### 6. Métricas da Sprint: Velocity e Burndown
* **Velocity (Velocidade):** A equipa planeou e comprometeu-se com 16 *Story Points*. Todas as histórias foram concluídas. Portanto, o **Velocity atual da equipa é de 16 pontos**.
* **Gráfico de Burndown (Tabela de Registo de Queima):**

| Dia da Sprint | Pontos Restantes (Real) | Histórias Concluídas | Status |
| :---: | :---: | :--- | :--- |
| **Dia 0 (Início)** | 16 SP | Nenhuma | Planeamento concluído. |
| **Dia 3** | 16 SP | Nenhuma | Desenvolvimento em curso. |
| **Dia 5** | 11 SP | US01 concluída (-5 SP) | Login operante. |
| **Dia 8** | 3 SP | US02 concluída (-8 SP) | API de Calendário resolvida. |
| **Dia 9** | 0 SP | US06 concluída (-3 SP) | Notificações prontas. |
| **Dia 10 (Fim)** | **0 SP** | Revisão Final | **Meta Atingida.** |

---

## Gestão de Mudança (Change Request)

### 1. Requisito Original
* **ID da História:** `[US05] Geração de resumo automatizado por IA`
* **Descrição Original:** Como participante, quero receber um resumo gerado por IA logo após a reunião, para revisar as decisões tomadas.
* **Critérios de Aceitação Originais:**
  1. Resumo enviado em até 5 minutos após o fim da reunião.
  2. Separação visual por tópicos principais.
* **Prioridade e Estimativa Originais:** *Must Have* | 5 Story Points.

### 2. Mudança Solicitada
O Diretor de RH solicitou a inclusão obrigatória de um "Termómetro de Sentimento" nos resumos gerados. O sistema deverá analisar o tom da conversa (Positivo, Neutro, Negativo ou Tenso) e incluir esse indicador no cabeçalho do documento final.

### 3. Motivo da Mudança
A alteração visa atender a uma nova diretriz estratégica do departamento de Recursos Humanos focada na saúde mental corporativa. O objetivo é mapear equipas sob elevado nível de stress ou desgaste emocional crónico (*Zoom fatigue*), permitindo intervenções preventivas de gestão.

### 4. Análise de Impacto
* **Impacto Arquitetural e Técnico:** A inclusão da análise de sentimento exige uma instrução adicional (*prompt engineering*) no modelo de *Machine Learning* (LLM), o que aumentará o consumo de *tokens* (custo financeiro por API) em aproximadamente 15% por reunião.
* **Impacto no Desempenho (Performance):** A adição desta camada de processamento de texto implicará uma maior latência. O sistema não conseguirá garantir o envio do resumo no limite restrito de 5 minutos utilizando a infraestrutura de servidores orçamentada para o MVP.
* **Impacto no Esforço (Estimativas):** A complexidade da história aumenta, forçando a reavaliação da US05 de 5 para 8 Story Points.

### 5. Decisão Tomada e Justificativa Técnica
**Decisão:** A mudança foi **Aprovada com Condicionante de Escopo** (Renegociação).

**Justificativa:** O valor estratégico que a análise de sentimento acrescenta à plataforma para os decisores (RH) é imenso e alinha-se perfeitamente com a dor central do utilizador. No entanto, para absorver este novo requisito sem comprometer o orçamento do projeto com servidores de alta performance, a equipa técnica (juntamente com o *Product Owner*) decidiu flexibilizar o critério de aceitação de tempo de resposta. O envio do resumo passará de 5 para 10 minutos após a reunião, acomodando o tempo extra de processamento da IA.

### 6. Alterações Realizadas no Backlog
O cartão da `[US05]` no GitHub Projects foi atualizado para refletir o novo acordo:
* **Estimativa atualizada:** De 5 SP para 8 SP.
* **Critérios de Aceitação Atualizados:**
  1. Resumo enviado em até 10 minutos após o fim da reunião.
  2. Separação visual por tópicos principais.
  3. *(NOVO)* Inclusão de um indicador visual de "Clima da Reunião" (Positivo, Neutro, Negativo ou Tenso).

### 7. Rastreabilidade da Mudança
Para garantir a rastreabilidade e a consistência histórica do *backlog*, adotou-se o seguinte protocolo no sistema:
1. O título da *issue* no GitHub foi alterado para `[US05 - Rev.1] Geração de resumo automatizado com Análise de Sentimento`.
2. Foi adicionada a *Label* (Etiqueta) amarela `Change Request` ao cartão.
3. O motivo da mudança e a justificação técnica foram registados como um comentário fixado na própria *issue*, documentando a alteração na latência exigida e o impacto nos *Story Points*.

