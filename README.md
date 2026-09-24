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
