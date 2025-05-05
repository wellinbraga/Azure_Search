# Azure AI Search - Guia de Implementação

Este repositório documenta o uso prático do **Azure AI Search**, desde a criação dos recursos até a configuração de pipelines de enriquecimento de dados com inteligência artificial. O objetivo é servir como material de apoio para estudos e implementações futuras.

---

## Sumário

- [Visão Geral](#visão-geral)
- [Recursos Necessários](#recursos-necessários)
- [Criação dos Recursos](#criação-dos-recursos)
- [Importação e Indexação dos Dados](#importação-e-indexação-dos-dados)
- [Enriquecimento com IA](#enriquecimento-com-ia)
- [Gerenciamento de Índices](#gerenciamento-de-índices)
- [Consultas e Pesquisas](#consultas-e-pesquisas)
- [Boas Práticas](#boas-práticas)
- [Links Úteis](#links-úteis)

---

## Visão Geral

O **Azure AI Search** é um mecanismo de busca totalmente gerenciado com integração nativa de inteligência artificial. Permite extrair, enriquecer, indexar e consultar dados de forma eficiente e escalável.

---

## Recursos Necessários

- **Azure AI Search**
- **Cognitive Services (AI Enrichment)**
- **Storage Account (Blob Storage)**
- **Data Source (container com documentos)**
- **Indexer (para importar os dados)**
- **Índice de Pesquisa**
- **Skillset (para enriquecimento com IA)**

---

## Criação dos Recursos

### 1. Criar o Azure AI Search

1. Vá para o portal do Azure.
2. Crie um recurso → **Azure AI Search**
3. Defina:
   - Nome do serviço
   - Região
   - Pricing Tier (Free, Basic, Standard...)

### 2. Criar o Recurso de Inteligência Artificial (Cognitive Services)

1. Crie um novo recurso → **Cognitive Services**
2. Escolha a região e crie um **key + endpoint**

### 3. Criar o Storage Account

1. Crie um recurso → **Storage Account**
2. Escolha:
   - Tipo: Blob Storage
   - Redundância: LRS ou ZRS
3. Finalize a criação.

### 4. Configurar os Containers e Importar os Dados

1. No Storage, crie um **container** (ex: `documentos`).
2. Faça o upload de arquivos suportados (PDF, DOCX, imagens, JSON).
3. Garanta que o container esteja com acesso autorizado para leitura pelo Azure Search.

---

## Importação e Indexação dos Dados

1. No Azure AI Search, vá até **Import Data**.
2. Selecione:
   - **Data Source**: seu Storage Account e container
   - **Skillset**: opcional, use para IA
   - **Index**: defina nome e campos
   - **Indexer**: agendamento e execução

---

## Enriquecimento com IA

Use **Skillsets** para aplicar inteligência artificial na transformação dos dados:

### Exemplo de Skills disponíveis:
- OCR (leitura de texto em imagens)
- Reconhecimento de entidade (pessoas, locais, etc)
- Detecção de idioma
- Extração de frases-chave
- Tradução automática
- Custom Skills (via Azure Functions)

> Requer um recurso de Cognitive Services vinculado ao Azure Search.

---

## Gerenciamento de Índices

- **Estrutura dos Campos**:
  - `name`: string, searchable, retrievable
  - `content`: text, searchable, facetable
- **Tipos de Dados**: `Edm.String`, `Edm.Boolean`, `Edm.Int32`, `Edm.GeographyPoint`
- **Operações REST/API**:
  - Criar, atualizar, deletar índices
  - Modificar esquemas dinamicamente

---

## Consultas e Pesquisas

### Métodos de consulta:

- **REST API**:  
GET /indexes/{indexName}/docs?search=texto


- **SDKs (C#, Python, JS)**

- **Filtros e Facetas**:
- `$filter=category eq 'Tecnologia'`
- `facet=autor,count:10`

- **Tipos de busca**:
- Fuzzy (`search=term~`)
- Boost (`search=AI^2 data`)
- Lucene-style queries (`search=“azure ai”~5`)

---

## Boas Práticas

- Use **índices normalizados** com campos descritivos e anotados.
- Evite reprocessamento total: use indexadores incrementais.
- Ative logging e monitoramento.
- Para produção, use pricing tier **Standard** ou superior.
- Combine com **Azure OpenAI** para chat semântico baseado em índice.

---

## Links Úteis

- [Documentação Azure AI Search](https://learn.microsoft.com/en-us/azure/search/)
- [Skillsets e enriquecimento](https://learn.microsoft.com/en-us/azure/search/cognitive-search-skillset)
- [REST API Search](https://learn.microsoft.com/en-us/rest/api/searchservice/)
- [Azure SDKs](https://learn.microsoft.com/en-us/azure/search/search-howto-sdk)



