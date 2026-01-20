# Disparo de Mensagens (n8n + Evolution API + Google Sheets)

Este repositório contém um fluxo de automação para o **n8n** focado no disparo em massa de mensagens de texto via **Evolution API**, utilizando o **Google Sheets** como base de dados e controle de status.

## 🚀 Funcionalidades

* **Leitura Automatizada**: Extrai contatos e números diretamente de uma planilha do Google Sheets.
* **Processamento em Lotes**: Utiliza lógica de loop (*Split in Batches*) para processar os registros de forma organizada.
* **Integração via Evolution API**: Realiza disparos de texto através de requisições HTTP POST.
* **Gestão de Status em Tempo Real**:
    * Atualiza a planilha para **ENVIADO** em caso de sucesso.
    * Atualiza a planilha para **FALHA NO ENVIO** em caso de erro na API.
* **Controle de Delay**: Inclui nós de espera (*Wait*) para mitigar riscos de bloqueio e respeitar limites de taxa.

## 🛠️ Tecnologias Utilizadas

* [n8n](https://n8n.io/)
* [Evolution API](https://evolution-api.com/)
* Google Sheets API

## 📋 Pré-requisitos

1.  **n8n** instalado e funcional.
2.  Planilha Google Sheets configurada com as colunas: `Cliente`, `Numero`, `Status` e `row_number`.
3.  Instância da **Evolution API** conectada a um dispositivo WhatsApp.
4.  Credenciais de OAuth2 para Google Sheets configuradas no seu n8n.

## ⚙️ Configuração do Fluxo

1.  **Importar JSON**: Importe o arquivo `disparo_mgs.json` para o seu editor n8n.
2.  **Configurar Planilha**: No nó `Get row(s) in sheet`, selecione o ID da sua planilha.
3.  **Configurar API**:
    * No nó `enviaText`, altere a URL para o endpoint da sua instância.
    * Insira sua `apikey` no campo de Headers.
4.  **Ajustar Delays**: Configure o tempo nos nós `Wait` e `Wait1` de acordo com a sua necessidade de cadência.

## 📐 Estrutura do Workflow

O fluxo opera em um ciclo contínuo até que todos os itens da planilha sejam processados:
1.  **Trigger**: Início manual.
2.  **Fetch**: Coleta de dados da planilha.
3.  **Loop**: Divisão dos dados em itens individuais.
4.  **Action**: Envio da mensagem via HTTP Request.
5.  **Feedback**: Registro do resultado (Sucesso ou Falha) na linha correspondente da planilha.

---
Documentação desenvolvida como parte de projetos de **Especialista em Agentes de IA e Automação**.
