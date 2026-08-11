# Microsoft Azure Data Fundamentals — DP-900
![Microsoft Azure](https://img.shields.io/badge/Microsoft%20Azure-Data%20Fundamentals-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white)
![Status](https://img.shields.io/badge/Status-Concluído-2EA44F?style=for-the-badge)
![Microsoft Learn](https://img.shields.io/badge/Microsoft%20Learn-Estudos-258FFA?style=for-the-badge&logo=microsoft&logoColor=white)
![License MIT](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)

Este repositório reúne meus estudos para a certificação **Microsoft Certified: Azure Data Fundamentals (DP-900)**.

O objetivo é registrar os principais conceitos estudados durante a preparação, consolidar o aprendizado e compartilhar materiais sobre fundamentos de dados e serviços de dados disponíveis no Microsoft Azure.

Em **julho de 2026**, concluí minha preparação e obtive a certificação **Microsoft Certified: Azure Data Fundamentals (DP-900)**.

---

## 📚 Como organizei meus estudos

Antes de transformar minhas anotações neste repositório, organizei todo o processo de preparação no **Notion**.

Criei um **Kanban de estudos** para acompanhar os módulos da certificação e utilizei um calendário para distribuir os conteúdos ao longo dos dias.

O fluxo era dividido entre:

* não iniciado;
* em andamento;
* concluído.

Cada conteúdo estudado era registrado no Notion, junto com minhas próprias anotações, pontos importantes, dúvidas e revisões.

Foi nesse espaço que concentrei inicialmente todo o material que, posteriormente, foi revisado e organizado para se tornar este repositório.

### Exemplo da organização

```text
📌 Módulo
   ↓
📖 Estudo no Microsoft Learn
   ↓
🎥 Vídeo complementar
   ↓
📝 Anotações no Notion
   ↓
❓ Revisão dos pontos de dúvida
   ↓
🧪 Simulado
   ↓
✅ Conteúdo concluído
   ↓
📂 Organização no GitHub
```

Essa organização também me ajudou a visualizar o progresso da preparação e identificar quais assuntos ainda precisavam de revisão.

---

# 📂 Conteúdo do repositório

As anotações foram revisadas e divididas em **oito módulos principais**, seguindo uma evolução dos fundamentos de dados até analytics e visualização.

## 01 — Conceitos fundamentais de dados

`01-explorando-conceitos-fundamentais-de-dados.md`

Conteúdos como:

* tipos de dados;
* dados estruturados, semiestruturados e não estruturados;
* formatos de arquivos;
* CSV, JSON e XML;
* Parquet, Avro e Delta Lake;
* bancos de dados;
* OLTP;
* workloads analíticos;
* ETL e ELT;
* Data Lake;
* Data Warehouse;
* Data Lakehouse;
* arquitetura Medallion.

---

## 02 — Funções e serviços de dados

`02-explorando-funcoes-e-servicos-de-dados.md`

Revisão das principais funções relacionadas a dados e dos serviços encontrados no ecossistema Microsoft, incluindo:

* Database Administrator;
* Data Engineer;
* Data Analyst;
* AI Engineer;
* Azure SQL;
* Azure Cosmos DB;
* Azure Storage;
* Azure Data Factory;
* Microsoft Fabric;
* Azure Databricks;
* Azure Stream Analytics;
* Power BI;
* Microsoft Purview.

---

## 03 — Conceitos fundamentais de dados relacionais

`03-conceitos-fundamentais-de-dados-relacionais.md`

Conteúdos relacionados ao modelo relacional e SQL:

* tabelas;
* normalização;
* Primary Key;
* Foreign Key;
* chave composta;
* SQL;
* DDL;
* DCL;
* DML;
* SELECT;
* WHERE;
* INSERT;
* ORDER BY;
* JOIN;
* Views;
* Stored Procedures;
* índices.

---

## 04 — Serviços de banco de dados relacional no Azure

`04-servicos-de-banco-de-dados-relacional-no-azure.md`

Comparação dos principais serviços relacionais:

* SQL Server em Azure VM;
* Azure SQL Managed Instance;
* Azure SQL Database;
* IaaS x PaaS;
* lift-and-shift;
* Elastic Pool;
* Hyperscale;
* Azure Database for MySQL;
* Azure Database for PostgreSQL.

---

## 05 — Dados não relacionais no Azure

`05-dados-nao-relacionais-no-azure.md`

Conteúdos sobre armazenamento não relacional e NoSQL:

* Azure Blob Storage;
* Block Blob;
* Page Blob;
* Append Blob;
* Hot, Cool, Cold e Archive;
* Lifecycle Management;
* redundância LRS, ZRS, GRS e GZRS;
* Azure Data Lake Storage Gen2;
* Microsoft OneLake;
* Azure Files;
* Azure Table Storage;
* Azure Cosmos DB;
* APIs NoSQL, MongoDB, Table, Cassandra e Gremlin;
* níveis de consistência;
* Request Units.

---

## 06 — Análise de dados em larga escala

`06-analise-de-dados-em-larga-escala.md`

Conteúdos relacionados a Big Data e arquiteturas analíticas:

* análise em larga escala;
* processamento distribuído;
* Apache Spark;
* Data Warehouse;
* Data Lake;
* Lakehouse;
* Delta Lake;
* fatos e dimensões;
* Star Schema;
* Snowflake Schema;
* Microsoft Fabric;
* OneLake;
* Fabric Lakehouse;
* Fabric Warehouse;
* Fabric Data Factory;
* Azure Data Factory;
* Azure Databricks;
* notebooks;
* OneLake Shortcuts;
* Mirroring;
* Lakeflow;
* Unity Catalog.

---

## 07 — Análise de dados em tempo real

`07-analise-de-dados-em-tempo-real.md`

Conteúdos relacionados ao processamento de streaming:

* processamento Batch;
* processamento Streaming;
* latência;
* micro-batches;
* janelas de tempo;
* Source, Processor e Sink;
* Azure Event Hubs;
* Azure IoT Hub;
* Apache Kafka;
* Azure Stream Analytics;
* Microsoft Fabric Real-Time Intelligence;
* Eventstream;
* Eventhouse;
* Real-Time Hub;
* Activator;
* Spark Structured Streaming;
* Delta Lake aplicado a streaming.

---

## 08 — Visualização e análise com Power BI

`08-visualizacao-e-analise-com-power-bi.md`

Conteúdos relacionados a Business Intelligence e visualização:

* Power BI Desktop;
* Power BI Service;
* Power BI no Microsoft Fabric;
* workspaces;
* modelos semânticos;
* Direct Lake;
* medidas;
* dimensões;
* tabelas fato e dimensão;
* Star Schema;
* Snowflake Schema;
* VertiPaq;
* hierarquias;
* drill-down;
* tipos de visualização;
* relatórios interativos;
* Copilot;
* Smart Narrative;
* Q&A;
* Key Influencers;
* Decomposition Tree.

---

# 🧪 Materiais extras

Além dos módulos principais, organizei materiais específicos de revisão e prática.

## Revisão dos simulados

`extras/revisao-simulados.md`

Durante os simulados, registrei principalmente os assuntos em que tive mais dificuldade ou em que confundia serviços semelhantes.

O material reúne:

* conceitos que precisei revisar;
* diferenças entre serviços;
* pegadinhas identificadas durante os estudos;
* associações rápidas;
* regras mentais;
* comparações entre tecnologias.

Alguns exemplos:

```text
Data Factory
→ movimentação e orquestração

Databricks
→ Spark e processamento distribuído

Event Hubs
→ ingestão de eventos

Stream Analytics
→ processamento de eventos

Azure Files
→ compartilhamento de arquivos

ADLS Gen2
→ armazenamento para analytics
```

A proposta dessa seção é registrar não apenas **o que estudei**, mas também **os conceitos que precisei reforçar após errar ou ter dúvidas em simulados**.

---

## 🤖 Prompt para agente de IA de simulados

`extras/agente-ia-simulados-prompt.md`

Durante os estudos, também desenvolvi um prompt para utilizar IA como agente de apoio na preparação para a DP-900.

O agente foi estruturado para:

* gerar questões;
* aplicar simulados;
* corrigir respostas;
* explicar alternativas incorretas;
* identificar padrões de dificuldade;
* adaptar perguntas conforme o desempenho;
* trabalhar em modo estudo ou modo prova;
* reforçar diferenças entre serviços semelhantes.

O objetivo do agente não é substituir a documentação oficial, mas funcionar como uma ferramenta de **estudo ativo e revisão personalizada**.

---

## 📝 Simulado com 60 questões

`extras/simulado-60-questoes.md`

Também organizei um simulado próprio contendo **60 questões de revisão** distribuídas entre os principais assuntos estudados.

Os temas incluem:

* fundamentos de dados;
* SQL e dados relacionais;
* serviços relacionais no Azure;
* armazenamento não relacional;
* Azure Cosmos DB;
* analytics em larga escala;
* streaming e tempo real;
* Power BI.

O arquivo inclui um gabarito ao final e foi criado para permitir uma revisão completa dos conteúdos depois da conclusão dos módulos.

---

# 📘 Microsoft Learn

Utilizei como principal referência a documentação e a trilha oficial da Microsoft para a certificação DP-900:

[Microsoft Certified: Azure Data Fundamentals](https://learn.microsoft.com/pt-br/credentials/certifications/azure-data-fundamentals/?practice-assessment-type=certification)

A documentação oficial foi utilizada para estudar os conceitos cobrados no exame e entender os principais serviços relacionados a dados dentro do Azure.

---

# 🎥 Microsoft Learn no YouTube

Também complementei os estudos com conteúdos disponibilizados no canal oficial da Microsoft:

[Microsoft Learn — YouTube](https://www.youtube.com/@MicrosoftLearn)

Os vídeos foram utilizados principalmente para revisar conceitos, complementar os conteúdos da documentação e visualizar alguns temas de maneira mais prática.

---

# 🧪 Simulados

Durante a preparação, realizei simulados para:

* identificar assuntos que precisavam de mais revisão;
* me familiarizar com o formato das questões;
* reforçar conceitos importantes;
* acompanhar minha evolução;
* revisar os conteúdos a partir dos erros cometidos.

Os erros dos simulados passaram a fazer parte do próprio processo de estudo, direcionando novas revisões.

Uma parte dessas anotações foi posteriormente organizada no arquivo:

```text
extras/revisao-simulados.md
```

---

# 🤖 Agente pessoal de estudos com GPT

Como apoio adicional, criei um **agente pessoal no GPT voltado especificamente para minha preparação para a DP-900**.

Utilizei o agente para:

* revisar conteúdos;
* tirar dúvidas;
* gerar perguntas;
* comparar conceitos;
* criar exemplos;
* simular questões;
* testar minha compreensão antes da prova.

A experiência também deu origem ao arquivo:

```text
extras/agente-ia-simulados-prompt.md
```

A IA foi utilizada como ferramenta complementar de estudo ativo, mantendo a documentação oficial da Microsoft como principal referência.

---

# 🎯 Objetivo deste repositório

Além de registrar minha preparação para a certificação, este repositório tem como objetivo consolidar conhecimentos relacionados a:

* conceitos fundamentais de dados;
* dados estruturados, semiestruturados e não estruturados;
* dados relacionais;
* dados não relacionais;
* workloads transacionais;
* workloads analíticos;
* engenharia de dados;
* processamento distribuído;
* processamento em tempo real;
* análise de dados;
* visualização de dados;
* Microsoft Fabric;
* serviços de dados disponíveis no Microsoft Azure.

O conteúdo representa minhas próprias anotações, resumos e interpretações construídas durante o processo de estudo.

---

# 🏅 Certificação

## Microsoft Certified: Azure Data Fundamentals — DP-900

**Certificação obtida em julho de 2026.**

✅ Microsoft Learn concluído
✅ Conteúdos em vídeo revisados
✅ Anotações organizadas no Notion
✅ Kanban de acompanhamento dos módulos
✅ Simulados realizados
✅ Pontos de dificuldade documentados
✅ Revisões com agente pessoal em GPT
✅ Prompt de agente de simulados documentado
✅ Simulado próprio com 60 questões
✅ Conteúdo consolidado em oito módulos
✅ Certificação DP-900 obtida

Este repositório representa a consolidação do material que utilizei durante essa jornada de preparação.

---

# 📄 Licença

Este projeto está licenciado sob a **MIT License**.

Isso significa que o conteúdo deste repositório pode ser utilizado, modificado, distribuído e compartilhado, desde que os termos da licença sejam respeitados.

Para mais detalhes, consulte o arquivo `LICENSE` presente neste repositório.

---

> Este material foi criado para fins de estudo e compartilhamento de conhecimento. Para informações oficiais e atualizadas sobre a certificação DP-900 e os serviços do Microsoft Azure, consulte sempre a documentação oficial da Microsoft.
