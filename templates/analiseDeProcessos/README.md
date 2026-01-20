# ⚖️ Automação de Consulta Processual (DataJud CNJ)

Este repositório contém um workflow do **n8n** projetado para automatizar a consulta de processos jurídicos na base de dados pública do **DataJud (CNJ)**. O sistema é capaz de realizar buscas por número de processo, classe processual ou órgão julgador, enviando os resultados estruturados via **Telegram** e **Evolution API (WhatsApp)**.

## 🚀 Funcionalidades

* **Busca por Número de Processo**: Identifica automaticamente números de 20 dígitos e realiza a consulta direta no TRF1.
* **Busca por Classe e Órgão**: Permite a pesquisa avançada utilizando códigos de classe processual e órgão julgador, com roteamento para o TJDFT.
* **Paginação Automática**: Suporte a consultas de grandes volumes de dados utilizando `search_after` e ordenação por timestamp.
* **Limpeza e Organização de Dados**: Nó de código dedicado para remover caracteres especiais de números de processos e validar a integridade dos dados de entrada.
* **Notificação Multicanal**:
    * Envio de resumos detalhados via **Telegram**.
    * Integração com **Evolution API** para disparos via WhatsApp.
* **Processamento em Lote**: Utiliza loops para processar múltiplos resultados da API sem sobrecarregar o sistema.

## 🛠️ Tecnologias Utilizadas

* **n8n**: Orquestrador do workflow.
* **Google Sheets**: Utilizado como base de dados de entrada para os termos de busca.
* **API Pública DataJud (CNJ)**: Fonte oficial dos dados processuais.
* **Telegram API**: Canal de saída para notificações.
* **Evolution API**: Canal de saída para mensagens via WhatsApp.
* **JavaScript (Code Nodes)**: Para lógica de montagem de requisições dinâmicas e tratamento de JSON.

## 📐 Estrutura do Workflow

1.  **Gatilho (Manual/Sheets)**: O fluxo inicia lendo dados de uma planilha do Google Sheets contendo os números ou classes dos processos.
2.  **Organização de Dados**: Limpeza de strings e validação de requisitos mínimos para a consulta.
3.  **Montagem de Requisição**: Lógica dinâmica que define a URL (TRF1 ou TJDFT) e o corpo do `POST` (Elasticsearch) baseado no tipo de entrada.
4.  **Consulta API**: Realiza a chamada autenticada à base do DataJud.
5.  **Estruturação de Resultados**: Extrai informações críticas como:
    * Número do processo, Classe e Assunto.
    * Tribunal, Grau e Órgão Julgador.
    * Histórico completo de movimentações com datas.
6.  **Distribuição**: Envia os dados formatados para os destinatários configurados.

## ⚙️ Configuração

* **API Key**: O fluxo utiliza uma chave de autorização para o DataJud. Certifique-se de configurar o Header `Authorization: ApiKey <SUA_CHAVE>` no nó de montagem de requisição.
* **Google Sheets**: Configure as credenciais de OAuth2 e aponte para o ID da sua planilha de controle.
* **Evolution API**: Configure o endereço da instância e a apikey no nó `Enviar texto`.

---
*Documentação gerada para automação de processos jurídicos e análise de dados judiciais.*
