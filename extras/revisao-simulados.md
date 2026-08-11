# Extras — Revisão dos simulados DP-900

> Este arquivo reúne conceitos que precisei revisar com mais atenção durante os simulados da certificação **Microsoft Azure Data Fundamentals (DP-900)**. A proposta é registrar não apenas o conteúdo revisado, mas também as associações e regras mentais que utilizei para diferenciar serviços e evitar erros recorrentes.

Durante a preparação, utilizei simulados não apenas para medir meu desempenho, mas principalmente para identificar os conceitos em que ainda tinha dúvidas ou confundia serviços com finalidades semelhantes.

Este material não reproduz questões do exame. Ele reúne os **conceitos que precisei revisar com mais atenção** durante os estudos.

---

# 1. Azure Data Factory x Azure Databricks x HDInsight x Azure Synapse

Um dos pontos de atenção foi diferenciar serviços que podem aparecer em cenários de engenharia e processamento de dados.

## Azure Data Factory

O **Azure Data Factory** está relacionado principalmente a:

```text
ETL / ELT
↓
Pipelines
↓
Integração e movimentação de dados
```

Resumo:

```text
Data Factory
→ pipelines
→ integração
→ ETL / ELT
```

---

## Azure Databricks

O **Azure Databricks** está relacionado principalmente ao processamento de grandes volumes de dados.

```text
Azure Databricks
↓
Apache Spark
↓
Processamento distribuído
↓
Engenharia / Analytics
```

Também possui forte relação com:

* notebooks;
* Delta Lake;
* processamento em escala;
* diferentes provedores de nuvem.

---

## HDInsight

O **Azure HDInsight** aparece nas anotações como um serviço utilizado para processamento de grandes volumes de dados utilizando tecnologias do ecossistema Hadoop.

```text
HDInsight
→ Big Data
→ Apache Hadoop
```

---

## Azure Synapse Analytics

Nas revisões, o **Azure Synapse Analytics** aparece associado a cenários analíticos e ao processamento utilizando Apache Spark.

Também aparece relacionado à análise próxima do tempo real sobre dados operacionais.

---

# 2. Data Warehouse x Banco Relacional x Data Lake

Outro ponto importante foi separar claramente essas estruturas.

## Data Warehouse

Data Warehouses utilizam modelagem analítica.

```text
Data Warehouse
│
├── Fact Tables
├── Dimension Tables
├── Star Schema
└── Snowflake Schema
```

São voltados principalmente para análise e leitura.

---

## Banco de dados relacional

Um banco relacional utilizado em cargas transacionais é normalmente voltado para operações como:

```text
Banco transacional
↓
CRUD
↓
INSERT / UPDATE / DELETE / SELECT
```

Não é correto assumir que qualquer banco relacional utiliza necessariamente modelagem com tabelas fato e dimensão.

---

## Data Lake

Data Lakes armazenam principalmente **arquivos**.

```text
Data Lake
↓
Arquivos
↓
Dados estruturados
Dados semiestruturados
Dados não estruturados
```

---

# 3. Normalização x Desnormalização

Esse foi outro conceito importante de revisão.

## Sistemas transacionais

Bancos transacionais tendem a utilizar estruturas mais **normalizadas**.

A normalização:

* reduz duplicidade;
* reduz armazenamento desnecessário;
* facilita inserções;
* facilita atualizações;
* facilita exclusões;
* ajuda na integridade dos dados.

```text
OLTP
↓
Normalização
↓
CRUD
```

---

## Sistemas analíticos

Cargas analíticas tendem a utilizar estruturas mais **desnormalizadas**, priorizando consultas e leitura.

```text
Analytics
↓
Desnormalização
↓
Leitura
```

Resumo:

```text
OLTP
→ normalizado
→ CRUD

OLAP / Analytics
→ mais desnormalizado
→ leitura
```

---

# 4. Pipelines, serviços vinculados e datasets

No Azure Data Factory, foi importante diferenciar os componentes.

## Linked Service

O **Linked Service** representa a conexão com uma fonte ou destino.

```text
Linked Service
→ conexão
```

Ele precisa existir para que o pipeline consiga acessar determinados serviços.

---

## Dataset

O **Dataset** representa os dados que serão utilizados como entrada ou saída.

```text
Dataset
→ referência aos dados
```

---

## Pipeline

O **Pipeline** organiza o fluxo.

```text
Pipeline
│
├── Activity
├── Activity
└── Activity
```

---

## Activity

As atividades representam ações executadas dentro do pipeline.

Fluxo mental:

```text
Linked Service
      ↓
   Dataset
      ↓
   Pipeline
      ↓
  Activities
```

---

# 5. Streaming: Event Hubs x IoT Hub x Stream Analytics

Esse conjunto de serviços pode ser facilmente confundido.

## Azure Event Hubs

Utilizado principalmente para ingestão e transporte de grandes volumes de eventos.

```text
Eventos
↓
Event Hubs
```

---

## Azure IoT Hub

Voltado principalmente a eventos provenientes de dispositivos IoT.

```text
Dispositivos IoT
↓
IoT Hub
```

---

## Azure Stream Analytics

É responsável pelo **processamento** dos dados de streaming.

```text
Event Hubs / IoT Hub
        ↓
Stream Analytics
        ↓
Consulta contínua
        ↓
Resultado
```

O Stream Analytics também pode realizar agregações dentro de períodos específicos antes de gravar os resultados.

---

# 6. Source x Processor x Sink

Uma forma simples de lembrar uma arquitetura de streaming:

```text
SOURCE
   ↓
PROCESSOR
   ↓
SINK
```

Exemplo:

```text
Event Hubs
     ↓
Stream Analytics
     ↓
Azure SQL Database
```

Nesse cenário:

```text
Event Hubs
→ fonte

Stream Analytics
→ processamento

Azure SQL Database
→ persistência
```

---

# 7. Azure Data Lake Storage Gen2 x Azure Files x Page Blobs x Table Storage

Esses serviços também apareceram juntos em diferentes alternativas dos simulados.

## Azure Data Lake Storage Gen2

Utilizado para armazenar grandes volumes de dados que posteriormente serão processados por serviços analíticos.

Exemplos citados:

* Databricks;
* Azure Synapse Analytics;
* HDInsight.

```text
ADLS Gen2
↓
Grande volume de dados
↓
Analytics / Big Data
```

---

## Azure Files

Utilizado para **compartilhamento de arquivos**.

Protocolos:

```text
SMB
NFS
```

```text
Azure Files
→ compartilhamento
```

---

## Page Blob

Utilizado principalmente para:

```text
VHD
→ discos de máquinas virtuais
```

---

## Azure Table Storage

Utilizado para armazenamento NoSQL baseado em:

```text
PartitionKey
+
RowKey
```

---

# 8. PartitionKey x RowKey

No Azure Table Storage, a chave é composta por:

```text
PartitionKey + RowKey
```

Um ponto que precisei reforçar:

> A `RowKey` é única dentro de uma partição, e não isoladamente em toda a tabela.

Os registros dentro de uma partição são organizados pela RowKey.

Uma consulta utilizando a PartitionKey pode reduzir o volume de dados que precisa ser examinado.

---

# 9. SQL — DDL x DCL x DML

Esse foi um ponto de revisão direta.

```text
SQL
│
├── DDL
├── DCL
└── DML
```

## DDL

Define a estrutura.

```text
CREATE
ALTER
DROP
RENAME
```

---

## DCL

Controla acesso e permissões.

```text
GRANT
DENY
REVOKE
```

---

## DML

Opera sobre os dados armazenados.

```text
INSERT
UPDATE
SELECT
DELETE
```

Resumo:

```text
DDL → estrutura
DCL → acesso
DML → dados
```

---

# 10. Blobs imutáveis

Outro conceito que apareceu nas revisões foi **immutability**.

Blobs imutáveis podem utilizar políticas de retenção para impedir alterações ou exclusões durante determinado período.

```text
Blob
↓
Retention Policy
↓
Não modificar
Não excluir
```

Esse tipo de recurso é importante principalmente para:

* conformidade;
* preservação de dados;
* retenção regulatória;
* proteção contra alterações indevidas.

---

## Diferença para recuperação

Alguns recursos ajudam a recuperar dados depois de exclusões ou modificações.

Já a imutabilidade busca **impedir que a alteração ou exclusão aconteça durante o período definido**.

---

# 11. APIs do Azure Cosmos DB

Um dos pontos mais importantes de memorização foi relacionar cada API ao respectivo modelo.

| API       | Modelo             |
| --------- | ------------------ |
| NoSQL     | Documentos JSON    |
| MongoDB   | Documentos BSON    |
| Table     | Chave-valor        |
| Cassandra | Família de colunas |
| Gremlin   | Grafos             |

---

# 12. Cosmos DB for Cassandra

Utilizado para dados no modelo de **família de colunas**.

```text
Cassandra
→ Column Family
```

A linguagem utilizada é:

```text
CQL
→ Cassandra Query Language
```

---

# 13. Cosmos DB for MongoDB

Trabalha com dados no formato:

```text
BSON
→ Binary JSON
```

A linguagem de consulta é:

```text
MQL
→ MongoDB Query Language
```

---

# 14. Cosmos DB for Gremlin

Voltado para bancos de dados em grafo.

```text
Graph
│
├── Nodes
└── Edges
```

Casos de uso:

* redes;
* relações;
* hierarquias;
* grafos organizacionais.

A linguagem utilizada é **Gremlin**.

---

# 15. Cosmos DB for Table

Utiliza armazenamento baseado em:

```text
Key / Value
```

Nas anotações dos simulados, consultas aparecem relacionadas a tecnologias como OData e LINQ.

---

# 16. Blob Storage x Table Storage

Outra distinção importante:

```text
Preciso armazenar arquivos?
        ↓
Blob Storage
```

```text
Preciso armazenar pares chave-valor?
        ↓
Table Storage
```

O Table Storage não é uma solução voltada para armazenamento de arquivos.

---

# 17. Cosmos DB Gremlin e hierarquias

Quando o problema depende fortemente das relações entre elementos, um banco em grafo pode fazer mais sentido.

Exemplo:

```text
CEO
 |
 ├── Diretor A
 |      ├── Gerente A
 |      └── Gerente B
 |
 └── Diretor B
```

Esse tipo de relacionamento pode ser modelado utilizando:

```text
Cosmos DB for Gremlin
```

---

# 18. CRUD e bancos transacionais

Bancos de dados transacionais são otimizados para operações:

```text
C → Create
R → Read
U → Update
D → Delete
```

Também costumam utilizar estruturas mais normalizadas.

```text
OLTP
↓
CRUD
↓
Normalização
```

---

# 19. Workloads analíticos

Cargas analíticas possuem outro objetivo.

```text
Analytics
↓
Grande volume
↓
Leitura
↓
Agregação
↓
Insights
```

São normalmente otimizadas para leitura e podem utilizar estruturas mais desnormalizadas.

---

# 20. Views, Functions e Stored Procedures

Outro ponto anotado durante os simulados foi a possibilidade de reutilizar lógica de consultas.

Nas anotações aparecem:

* Views;
* Functions;
* Stored Procedures.

Esses objetos podem ajudar a encapsular ou reutilizar lógica utilizada em consultas mais complexas.

---

# 21. Spark e grandes volumes de dados

Azure Databricks e recursos baseados em Spark podem processar grandes volumes de dados de forma distribuída.

```text
Grande conjunto de dados
        ↓
Apache Spark
        ↓
Cluster
        ↓
Processamento paralelo
```

Nas revisões, Scala também aparece como uma das linguagens associadas ao processamento Spark.

---

# 22. Fabric: qual armazenamento escolher?

O Microsoft Fabric oferece diferentes armazenamentos conforme o workload.

```text
Microsoft Fabric
│
├── SQL Database
├── Warehouse
├── Lakehouse
└── Eventhouse
```

Um dos pontos que precisei reforçar foi entender que cada um tem uma finalidade diferente.

---

## SQL Database

```text
SQL Database
→ operacional
→ transacional
```

---

## Warehouse

```text
Warehouse
→ analytics estruturado
→ SQL
→ alta concorrência
→ Data Warehouse
```

É a escolha indicada nas minhas revisões para análise estruturada em larga escala.

---

## Lakehouse

```text
Lakehouse
→ Data Lake + Analytics
→ flexibilidade
```

---

## Eventhouse

```text
Eventhouse
→ eventos
→ streaming
→ tempo real
```

---

# 23. Databricks Notebooks

Os notebooks do Databricks são ambientes interativos para trabalhar diretamente com os dados.

Neles é possível:

* executar código;
* executar SQL;
* consultar dados;
* explorar informações;
* criar tabelas Delta;
* persistir dados estruturados;
* criar bancos de dados no metastore.

```text
Databricks Notebook
│
├── Python
├── Spark
├── SQL
└── Delta
```

Um ponto que apareceu nas revisões é que criar outro notebook é uma tarefa de gerenciamento do workspace e não uma operação executada de dentro de um notebook existente.

---

# 24. Azure Data Explorer x Stream Analytics x Data Lake x Cosmos DB

Outro conjunto de serviços que precisei diferenciar:

## Azure Data Explorer

Voltado principalmente para análise de grandes volumes de:

* logs;
* telemetria;
* dados de sites;
* dados IoT.

```text
Logs / Telemetria
↓
Azure Data Explorer
↓
Análise
```

---

## Azure Stream Analytics

```text
Streaming
↓
Consulta perpétua
↓
Processamento
↓
Output
```

---

## Data Lake Storage Gen2

```text
ADLS Gen2
→ armazenamento
→ fonte de dados
```

---

## Cosmos DB

```text
Cosmos DB
→ banco NoSQL
→ armazenamento de dados
```

---

# 25. SQL Server no Azure

Um detalhe que apareceu nos simulados foi a diferença de compatibilidade entre as opções de SQL Server.

Nas minhas anotações, o **SQL Server em Azure VM executando Windows** aparece como a alternativa que oferece suporte ao conjunto completo de recursos do SQL Server na nuvem.

As demais opções possuem diferentes níveis de compatibilidade:

* Azure SQL Database;
* Azure SQL Managed Instance;
* SQL Server em VM Linux.

---

# 26. PostgreSQL

Outro ponto de revisão foi lembrar que o PostgreSQL não é apenas um banco relacional tradicional.

Ele é descrito como um sistema:

```text
Relacional
+
Objeto-relacional
```

Permite:

* tabelas relacionais;
* tipos de dados personalizados;
* propriedades não relacionais.

---

# 🧠 Mapa mental dos pontos de dificuldade

```text
REVISÃO DOS SIMULADOS
│
├── Engenharia
│   ├── Data Factory → pipelines
│   ├── Databricks → Spark
│   ├── Synapse → analytics
│   └── HDInsight → Hadoop
│
├── Storage
│   ├── ADLS → Big Data
│   ├── Azure Files → SMB / NFS
│   ├── Page Blob → VHD
│   └── Table Storage → key/value
│
├── Streaming
│   ├── Event Hubs → eventos
│   ├── IoT Hub → dispositivos
│   └── Stream Analytics → processamento
│
├── Cosmos DB
│   ├── NoSQL → JSON
│   ├── MongoDB → BSON
│   ├── Table → key/value
│   ├── Cassandra → column family
│   └── Gremlin → graph
│
├── SQL
│   ├── DDL → estrutura
│   ├── DCL → acesso
│   └── DML → dados
│
├── Workloads
│   ├── OLTP → normalizado / CRUD
│   └── Analytics → leitura / desnormalizado
│
└── Fabric
    ├── SQL Database → transacional
    ├── Warehouse → analytics
    ├── Lakehouse → flexível
    └── Eventhouse → streaming
```

---

# ✅ Revisão rápida

* **Data Factory** → ETL/ELT e pipelines.
* **Databricks** → processamento distribuído e Spark.
* **HDInsight** → Big Data e Hadoop.
* **Data Warehouse** → fato, dimensão e modelagem analítica.
* **Data Lake** → arquivos.
* **Linked Service** → conexão com uma fonte ou destino.
* **Dataset** → referência aos dados.
* **Pipeline** → conjunto de atividades.
* **Event Hubs** → ingestão de eventos.
* **IoT Hub** → ingestão de dados IoT.
* **Stream Analytics** → processamento de streaming.
* **ADLS Gen2** → grandes volumes de dados para processamento analítico.
* **Azure Files** → SMB e NFS.
* **Page Blob** → VHD.
* **Table Storage** → PartitionKey + RowKey.
* **DDL** → estrutura.
* **DCL** → permissões.
* **DML** → manipulação.
* **Cosmos DB Cassandra** → família de colunas.
* **Cosmos DB MongoDB** → BSON.
* **Cosmos DB Gremlin** → grafos.
* **Cosmos DB Table** → chave-valor.
* **OLTP** → CRUD e normalização.
* **Analytics** → leitura e estruturas mais desnormalizadas.
* **Warehouse** → análise estruturada.
* **Lakehouse** → flexibilidade analítica.
* **Eventhouse** → eventos e tempo real.
* **Azure Data Explorer** → logs e telemetria.
* **PostgreSQL** → relacional e objeto-relacional.

---

# 🔎 Como eu diferenciava serviços parecidos nos simulados

Durante os simulados, percebi que muitas questões não exigiam apenas conhecer um serviço, mas principalmente saber **diferenciá-lo de outras opções parecidas**.

Por isso, criei algumas associações rápidas para identificar o serviço mais adequado de acordo com o cenário apresentado.

| Se a questão fala em...                                  | Eu associava a...              |
| -------------------------------------------------------- | ------------------------------ |
| Pipeline, integração ou ETL/ELT                          | Azure Data Factory             |
| Processamento distribuído com Apache Spark               | Azure Databricks               |
| Grande volume de eventos                                 | Azure Event Hubs               |
| Dispositivos e telemetria IoT                            | Azure IoT Hub                  |
| Processamento contínuo de streams                        | Azure Stream Analytics         |
| Logs e telemetria para análise                           | Azure Data Explorer            |
| Compartilhamento de arquivos por SMB ou NFS              | Azure Files                    |
| Grandes volumes de arquivos para analytics               | Azure Data Lake Storage Gen2   |
| Disco de máquina virtual                                 | Page Blob                      |
| Armazenamento chave-valor simples                        | Azure Table Storage            |
| Banco NoSQL global e de baixa latência                   | Azure Cosmos DB                |
| Documentos JSON                                          | Cosmos DB for NoSQL            |
| Aplicação MongoDB existente                              | Cosmos DB for MongoDB          |
| Família de colunas                                       | Cosmos DB for Apache Cassandra |
| Dados em grafo                                           | Cosmos DB for Apache Gremlin   |
| Nova aplicação SQL desenvolvida para nuvem               | Azure SQL Database             |
| Migração de SQL Server com alta compatibilidade          | Azure SQL Managed Instance     |
| Controle completo sobre SQL Server e sistema operacional | SQL Server em Azure VM         |
| Analytics estruturado baseado em SQL                     | Data Warehouse                 |
| Arquivos + Spark + analytics                             | Lakehouse                      |
| Eventos e séries temporais no Microsoft Fabric           | Eventhouse                     |

---

# ⚠️ Pegadinhas que eu precisei reforçar

Alguns conceitos apareciam em alternativas muito parecidas e exigiram atenção extra durante os simulados.

## Azure Event Hubs ≠ Azure Stream Analytics

```text
Event Hubs
→ recebe e transporta eventos

Stream Analytics
→ processa os eventos
```

---

## Azure IoT Hub ≠ Azure Event Hubs

```text
IoT Hub
→ dispositivos IoT

Event Hubs
→ ingestão genérica de grandes volumes de eventos
```

---

## Azure Data Factory ≠ Azure Databricks

```text
Data Factory
→ integração
→ movimentação
→ pipelines
→ ETL / ELT

Databricks
→ Apache Spark
→ processamento distribuído
→ engenharia de dados
```

---

## Azure Files ≠ Azure Data Lake Storage Gen2

```text
Azure Files
→ compartilhamento de arquivos
→ SMB / NFS

ADLS Gen2
→ armazenamento para analytics
→ grandes volumes
→ processamento com engines analíticas
```

---

## Azure Table Storage ≠ banco de dados relacional

Apesar de utilizar o termo "Table", o Azure Table Storage é um armazenamento **NoSQL chave-valor**.

```text
Azure Table Storage

PartitionKey
+
RowKey
```

Não possui os principais conceitos relacionais, como:

```text
Foreign Key
Relacionamentos
Stored Procedures
Views
```

---

## RowKey não é globalmente única

A `RowKey` é única **dentro de uma PartitionKey**.

```text
PartitionKey + RowKey
→ identificação do item
```

---

## Page Blob = VHD

Uma associação que precisei memorizar:

```text
Page Blob
→ Virtual Hard Disk
→ discos de Azure VMs
```

---

## OLTP ≠ Analytics

```text
OLTP
→ transações
→ CRUD
→ normalização

Analytics
→ leitura
→ agregações
→ estruturas mais desnormalizadas
```

---

## Data Lake ≠ Data Warehouse

```text
Data Lake
→ arquivos
→ diferentes formatos
→ flexibilidade

Data Warehouse
→ dados estruturados
→ SQL
→ fatos e dimensões
→ analytics
```

---

## Cosmos DB APIs

```text
NoSQL
→ documentos JSON

MongoDB
→ BSON / MQL

Table
→ chave-valor

Cassandra
→ família de colunas

Gremlin
→ grafos
```

---

## SQL Server em VM ≠ Managed Instance ≠ Azure SQL Database

```text
SQL Server em VM
→ IaaS
→ maior controle

Managed Instance
→ PaaS
→ alta compatibilidade com SQL Server

Azure SQL Database
→ PaaS
→ aplicação cloud-native
→ menor administração
```

---

# 🧠 Erros que viraram regra mental

Depois de errar ou ficar em dúvida em algumas questões, transformei os conceitos em associações rápidas para facilitar a revisão.

```text
Mover ou orquestrar dados
→ Data Factory

Processar muito dado
→ Databricks / Spark

Receber eventos
→ Event Hubs

Receber dados de dispositivos
→ IoT Hub

Processar eventos
→ Stream Analytics

Analisar logs e telemetria
→ Data Explorer

Compartilhar arquivos
→ Azure Files

Armazenar grandes volumes para analytics
→ ADLS Gen2

Disco de VM
→ Page Blob

Chave-valor
→ Table Storage

JSON NoSQL
→ Cosmos DB for NoSQL

MongoDB
→ BSON

Cassandra
→ Column Family

Gremlin
→ Graph

OLTP
→ CRUD + normalização

Analytics
→ leitura + desnormalização

Data Warehouse
→ fatos + dimensões

Data Lake
→ arquivos

Lakehouse
→ Data Lake + recursos analíticos

Warehouse no Fabric
→ analytics estruturado

Eventhouse
→ eventos + tempo real
```

---

# 🎯 Como eu pensava nas questões

Quando duas ou mais alternativas pareciam corretas, tentei identificar primeiro **qual era a necessidade principal do cenário**.

```text
A questão quer armazenar?
        ↓
Qual tipo de dado?

A questão quer processar?
        ↓
Batch ou streaming?

A questão quer movimentar?
        ↓
Pipeline / Data Factory

A questão quer analisar?
        ↓
SQL, Spark, BI ou tempo real?

A questão fala em migração?
        ↓
Qual nível de compatibilidade e controle?
```

A ideia era deixar de escolher serviços apenas pelo nome e passar a associá-los ao **papel que desempenham dentro da arquitetura**.

---

# 📌 Resumo das associações

```text
ORQUESTRAÇÃO
→ Azure Data Factory

SPARK
→ Azure Databricks

EVENTOS
→ Event Hubs

IOT
→ IoT Hub

PROCESSAMENTO DE STREAM
→ Stream Analytics

LOGS E TELEMETRIA
→ Data Explorer

ARQUIVOS COMPARTILHADOS
→ Azure Files

DATA LAKE
→ ADLS Gen2

VHD
→ Page Blob

KEY/VALUE
→ Table Storage

JSON / NOSQL
→ Cosmos DB for NoSQL

MONGODB
→ BSON / MQL

COLUMN FAMILY
→ Cassandra

GRAPH
→ Gremlin

TRANSAÇÕES
→ OLTP

ANALYTICS
→ OLAP

DADOS ESTRUTURADOS PARA BI
→ Data Warehouse

ARQUIVOS + ANALYTICS
→ Lakehouse

TEMPO REAL NO FABRIC
→ Eventhouse
```

---

> Os simulados foram utilizados como ferramenta de diagnóstico durante minha preparação. Estas anotações representam os conceitos que precisei reforçar após identificar dúvidas ou erros recorrentes durante os estudos para a certificação **Microsoft Azure Data Fundamentals (DP-900)**.
