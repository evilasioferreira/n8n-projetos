# 🤖 Sistema de Atendimento Inteligente Multiagentes

Este workflow implementa uma camada de inteligência que atua como um **orquestrador central** dentro do n8n. Ele identifica a intenção do usuário e delega a tarefa para o **Agente Especialista** mais adequado, garantindo respostas precisas, personalizadas e contextuais.

## 🚀 Funcionalidades Principais

* **Classificação Dinâmica de Personas:** Um agente supervisor analisa o histórico e a mensagem atual para definir o perfil do usuário entre mais de 10 categorias distintas (ex: *Ideal, Monossilábico, Agência, Influencer*).
* **Arquitetura Multiagentes:** Diversos agentes especializados (Especialista em Roteiros, Agente de Parcerias, Agente de Preços, entre outros) operam com instruções de sistema (*System Messages*) exclusivas e focadas em seus domínios.
* **Processamento Multimodal:**
    * **Áudio:** Transcrição automática de mensagens de voz integrada ao fluxo via OpenAI Whisper.
    * **Texto:** Processamento de linguagem natural utilizando modelos de última geração como GPT-4o e GPT-4o-mini.
* **Gestão de Memória Avançada:**
    * Uso de **Window Buffer Memory** para manter o contexto imediato das últimas interações.
    * **Persistência Híbrida:** Armazenamento de dados em n8n Data Tables e Redis para recuperação de histórico de longo prazo e controle de estados.
* **Validação de Dados por IA:** Nós de código e agentes específicos validam informações críticas, como a lógica de datas de viagem e a consistência da composição do grupo (adultos/crianças).

## 🛠️ Tecnologias Utilizadas

* **n8n:** Orquestrador principal responsável pela lógica do fluxo e conexões.
* **LangChain:** Framework utilizado para integração de IA, gerenciamento de memória e uso de ferramentas (*Tools*).
* **OpenAI (GPT-4o / GPT-5-mini):** Motores de inferência de alto desempenho para raciocínio e geração de respostas.
* **Redis:** Utilizado para armazenamento temporário, gerenciamento de sessões e controle de mensagens fracionadas.
* **Data Tables (n8n):** Persistência estruturada de dados dos leads, histórico de atendimentos e estados das personas.
* **HTTP Requests:** Conexão com APIs externas para consulta de serviços, disponibilidade e integração com sistemas de mensageria.

## 📐 Estrutura do Workflow

1.  **Entrada (Webhook):** Ponto inicial que recebe os dados brutos das plataformas de comunicação.
2.  **Normalização:** O nó `normalizaEntrada` (via JavaScript) padroniza diferentes formatos de texto, transcrições de áudio e interpretações de reações por emojis.
3.  **Supervisor de Persona:** O nó `classificadorPersona` utiliza modelos de IA para decidir qual agente especialista deve assumir o controle daquela iteração.
4.  **Execução Especialista:** O fluxo é direcionado por um nó de *Switch* para o agente correspondente (ex: `ideal`, `monossilabico`, `agencia`, `influencer`), cada um com seu próprio prompt especializado.
5.  **Gerenciamento de Ferramentas (Tools):** Os agentes utilizam ferramentas como o `getLead` para consultar tabelas de dados em tempo real, garantindo que a IA não repita perguntas já respondidas.
6.  **Saída Humanizada:** O sistema processa a resposta final e a fraciona em múltiplos parágrafos com atrasos (*Wait*) para simular um comportamento de digitação humana.

## ⚙️ Configuração

* **Credenciais:** Configure suas chaves de API para OpenAI, instâncias Redis e bancos de dados dentro das configurações de credenciais do n8n.
* **Variáveis de Ambiente:** Ajuste as URLs nos nós de `HTTP Request` para apontar para seus respectivos endpoints de backend ou serviços de mensageria.
* **Ajuste de Prompts:** As instruções comportamentais podem ser editadas individualmente nos nós de **AI Agent**, permitindo o refinamento contínuo da equipe multiagentes.

---
*Documentação técnica desenvolvida para fluxos de IA Generativa e Automação de Processos.*
