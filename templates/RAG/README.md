# 📚 Pipeline de Ingestão RAG (Google Drive & PDF Form)

Este repositório contém uma solução avançada de **RAG (Retrieval-Augmented Generation)** desenvolvida no **n8n**. O sistema automatiza o ciclo de vida do conhecimento para agentes de IA, permitindo a ingestão, processamento e vetorização de documentos a partir de duas fontes principais: monitorização de ficheiros na cloud (Google Drive) e submissão direta via formulário web.

## 🚀 Funcionalidades

* **Ingestão Automatizada via Google Drive:** Deteta automaticamente quando ficheiros são criados ou editados em pastas específicas.
* **Carregamento Direto via Formulário:** Interface web integrada para submissão manual de ficheiros PDF.
* **Processamento de Texto Inteligente:**
    * Segmentação de documentos (Chunking) utilizando o **Recursive Character Text Splitter** para manter o contexto semântico.
    * Extração de conteúdo binário e conversão de documentos para formato de texto simples.
* **Vetorização e Armazenamento:**
    * Geração de embeddings de alta qualidade via **OpenAI**.
    * Armazenamento vetorial no **Supabase Vector Store** para consultas de busca semântica rápidas e eficientes.
* **Gestão de Ficheiros Mistral AI:** Upload automatizado para a infraestrutura da Mistral AI para processamento complementar.

## 🛠️ Tecnologias Utilizadas

* **n8n:** Orquestrador principal dos fluxos e lógica de negócio.
* **Supabase:** Base de dados vetorial para persistência do conhecimento.
* **OpenAI:** Modelos de Embedding para transformar texto em representações matemáticas.
* **Google Drive API:** Integração para monitorização e download de documentos.
* **Mistral AI:** Processamento avançado de ficheiros via API.

## 📐 Estrutura dos Workflows

### 1. Fluxo de Monitorização (Google Drive)
Este fluxo corre em background e reage a eventos na cloud:
1.  **Trigger:** O nó `arquivoCriado` ou `arquivoEditado` inicia o processo.
2.  **Download:** O ficheiro é descarregado e convertido para texto simples.
3.  **Vetorização:** O texto é fragmentado e inserido no Supabase.

### 2. Fluxo de Submissão Manual (RAG PDF)
Este fluxo oferece uma interface para utilizadores:
1.  **Trigger:** Formulário n8n (`On form submission`) recebe o PDF.
2.  **Ingestão Dupla:** O ficheiro é enviado para o armazenamento da Mistral AI e processado para a base vetorial do Supabase simultaneamente.
3.  **Embedding:** Utiliza a inteligência da OpenAI para indexar o conteúdo.

## ⚙️ Configuração

Para que os fluxos funcionem corretamente, configure as seguintes credenciais no seu ambiente n8n:
* **Google Drive OAuth2:** Para acesso às pastas de documentos.
* **OpenAI API:** Para geração dos embeddings.
* **Supabase API:** URL e Service Role Key para gestão da base vetorial.
* **Mistral AI:** Bearer Token para autenticação na API.
