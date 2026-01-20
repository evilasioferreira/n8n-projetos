# Backup Automatizado de Workflows (n8n para Google Drive)

Este repositório contém um fluxo do **n8n** projetado para realizar o backup automático de todos os seus workflows. Ele extrai as estruturas JSON da sua instância n8n, organiza-as em pastas datadas e possui uma rotina de limpeza para remover backups antigos.

## 🚀 Funcionalidades

* **Exportação Global**: Conecta-se à API do n8n para listar e baixar todos os fluxos ativos e inativos.
* **Conversão de Dados**: Processa os dados brutos via código (Node.js/JavaScript) para garantir que o formato JSON esteja pronto para restauração.
* **Organização Inteligente**: Cria ou localiza pastas específicas para salvar os arquivos de forma organizada.
* **Gestão de Armazenamento (Retention)**: 
    * Calcula a diferença de dias entre a criação do backup e a data atual.
    * Filtra arquivos com mais de 15 dias (configurável).
    * Remove automaticamente backups antigos para otimizar o espaço.
* **Delay de Segurança**: Inclui intervalos (5s) para evitar sobrecarga na API durante o upload.

## 🛠️ Tecnologias Utilizadas

* [n8n](https://n8n.io/)
* **Node.js (n8n Code Node)**: Para manipulação avançada de strings e datas.
* **Google Drive API**: Para armazenamento e gerenciamento de arquivos e pastas.
* **n8n API**: Para extração dos dados da própria instância.

## 📋 Pré-requisitos

1.  **API Key do n8n**: Necessária para que o fluxo consiga ler os próprios workflows.
2.  **Credenciais do Google Drive**: Configuradas no n8n para permitir a criação de pastas e upload de arquivos.
3.  **Permissões**: Certifique-se de que a instância do n8n tem acesso de rede para se comunicar com o Google Drive.

## ⚙️ Configuração do Fluxo

1.  **Importação**: Importe o arquivo `backup.json` no seu n8n.
2.  **Nó `apiN8N`**: Configure a URL da sua instância e a sua API Key.
3.  **Nó de Upload**: Verifique se a conta do Google Drive está selecionada corretamente.
4.  **Ajuste de Retenção**: No nó `>15d`, você pode alterar o valor numérico para definir por quantos dias deseja manter os backups antes da exclusão automática.

## 📐 Lógica do Workflow

1.  **Listar**: O fluxo consulta todos os workflows da instância.
2.  **Tratar**: Um nó de código limpa caracteres especiais e formata o conteúdo.
3.  **Verificar**: O fluxo checa se a pasta de destino já existe ou precisa ser criada.
4.  **Salvar**: Faz o upload de cada fluxo individualmente.
5.  **Limpar**: Inicia uma sub-rotina que lista arquivos na pasta de backup, calcula a idade de cada um e deleta os que excederem o limite definido.

---
*Este workflow é essencial para ambientes de produção, garantindo a segurança dos seus agentes e automações.*
