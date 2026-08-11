# Simulado DP-900 — 60 questões

> Simulado de revisão para a certificação **Microsoft Azure Data Fundamentals (DP-900)**, criado a partir dos conteúdos estudados durante minha preparação.

O simulado contém **60 questões**, divididas entre os principais domínios revisados:

* fundamentos de dados;
* dados relacionais;
* serviços relacionais no Azure;
* dados não relacionais;
* análise em larga escala;
* análise em tempo real;
* Power BI e visualização.

Cada questão possui apenas **uma alternativa correta**.

---

# Parte 1 — Fundamentos de dados

## Questão 1

Uma aplicação recebe informações no seguinte formato:

```json
{
  "cliente": "Ana",
  "cidade": "Porto Alegre",
  "pedidos": 4
}
```

Como esses dados são classificados?

A. Dados não estruturados
B. Dados relacionais
C. Dados semiestruturados
D. Dados exclusivamente binários

---

## Questão 2

Uma empresa possui milhares de vídeos, imagens e documentos que precisam ser armazenados para processamento posterior.

Esses dados são classificados principalmente como:

A. Não estruturados
B. Estruturados
C. Relacionais
D. Normalizados

---

## Questão 3

Qual formato de arquivo é especialmente adequado para workloads analíticos por utilizar armazenamento colunar?

A. XML
B. TXT
C. JSON
D. Parquet

---

## Questão 4

Qual característica diferencia principalmente o processamento OLTP de workloads analíticos?

A. OLTP é voltado exclusivamente para arquivos.
B. OLTP é otimizado para transações e operações CRUD.
C. OLTP é utilizado apenas para streaming.
D. OLTP não utiliza bancos relacionais.

---

## Questão 5

Uma aplicação executa constantemente operações de inserção, atualização e exclusão sobre registros individuais.

Qual tipo de workload melhor representa esse cenário?

A. Data Lake
B. OLAP
C. OLTP
D. Streaming Analytics

---

## Questão 6

Qual propriedade do modelo ACID garante que uma transação seja executada completamente ou não seja executada?

A. Atomicidade
B. Consistência
C. Isolamento
D. Durabilidade

---

## Questão 7

Qual abordagem transforma os dados **depois** que eles já foram carregados no armazenamento de destino?

A. CRUD
B. ELT
C. OLTP
D. DDL

---

## Questão 8

Qual arquitetura combina características de um Data Lake com recursos tradicionalmente associados a Data Warehouses?

A. OLTP
B. Blob Storage
C. Lakehouse
D. File Share

---

# Parte 2 — Dados relacionais e SQL

## Questão 9

Em uma tabela `Cliente`, a coluna `id_cliente` identifica exclusivamente cada registro.

Essa coluna é uma:

A. Foreign Key
B. Dimension
C. Measure
D. Primary Key

---

## Questão 10

Uma tabela `Pedido` possui uma coluna `id_cliente` que referencia a chave primária da tabela `Cliente`.

A coluna `id_cliente` em `Pedido` é uma:

A. Foreign Key
B. View
C. Stored Procedure
D. Measure

---

## Questão 11

Qual é um dos principais objetivos da normalização?

A. Aumentar propositalmente a duplicação
B. Transformar tabelas em arquivos JSON
C. Reduzir redundância e melhorar a integridade
D. Eliminar todas as chaves estrangeiras

---

## Questão 12

Qual grupo SQL é utilizado para criar ou alterar a estrutura de objetos do banco?

A. DML
B. DDL
C. DCL
D. CRUD

---

## Questão 13

Qual comando pertence à DCL?

A. INSERT
B. DROP
C. SELECT
D. GRANT

---

## Questão 14

Qual conjunto contém apenas comandos DML?

A. SELECT, INSERT, UPDATE, DELETE
B. CREATE, ALTER, DROP, RENAME
C. GRANT, DENY, REVOKE
D. CREATE, SELECT, GRANT, DELETE

---

## Questão 15

O que pode acontecer se uma instrução `UPDATE` for executada sem uma cláusula `WHERE`?

A. Nenhuma linha será alterada.
B. Apenas a primeira linha será alterada.
C. Todas as linhas poderão ser alteradas.
D. A tabela será automaticamente excluída.

---

## Questão 16

Qual recurso SQL cria uma tabela virtual baseada no resultado de uma consulta?

A. Index
B. View
C. Trigger
D. Primary Key

---

## Questão 17

Qual recurso encapsula instruções SQL que podem ser executadas sob demanda e pode receber parâmetros?

A. Stored Procedure
B. Foreign Key
C. Dataset
D. PartitionKey

---

## Questão 18

Qual é o principal benefício de um índice?

A. Impedir totalmente operações DELETE
B. Normalizar automaticamente uma tabela
C. Substituir uma Primary Key
D. Melhorar o desempenho de determinadas consultas

---

# Parte 3 — Serviços relacionais no Azure

## Questão 19

Uma empresa deseja migrar um SQL Server local para Azure mantendo controle sobre o sistema operacional e alto nível de compatibilidade.

Qual opção é mais adequada?

A. Azure SQL Database
B. SQL Server em Azure VM
C. Azure Table Storage
D. Azure Cosmos DB

---

## Questão 20

Qual opção do Azure SQL é classificada como IaaS?

A. SQL Server em Azure VM
B. Azure SQL Database
C. Azure SQL Managed Instance
D. Azure Database for PostgreSQL

---

## Questão 21

Uma empresa possui uma solução SQL Server existente com recursos avançados e deseja migrá-la com poucas alterações, mas reduzir tarefas administrativas.

Qual serviço é mais adequado?

A. Azure Files
B. Azure SQL Database
C. Azure SQL Managed Instance
D. Azure Blob Storage

---

## Questão 22

Uma equipe está desenvolvendo uma nova aplicação cloud-native e deseja o mínimo possível de administração da infraestrutura do SQL Server.

Qual opção é mais adequada?

A. SQL Server local
B. SQL Server em Azure VM
C. Azure SQL Managed Instance
D. Azure SQL Database

---

## Questão 23

Qual funcionalidade permite que vários bancos no Azure SQL Database compartilhem recursos computacionais?

A. Elastic Pool
B. PartitionKey
C. Eventhouse
D. Dataflow Gen2

---

## Questão 24

Qual camada do Azure SQL Database é voltada para bancos de dados muito grandes e dimensionamento rápido?

A. Archive
B. Hyperscale
C. Cold
D. Flexible Server

---

## Questão 25

Qual serviço oferece uma implementação PaaS gerenciada do MySQL no Azure?

A. Azure Cosmos DB
B. Azure SQL Managed Instance
C. Azure Database for MySQL
D. SQL Server em Azure VM

---

## Questão 26

Qual afirmação descreve corretamente o PostgreSQL?

A. É exclusivamente um banco chave-valor.
B. É exclusivamente um armazenamento de arquivos.
C. É um mecanismo de streaming.
D. Possui características relacionais e objeto-relacionais.

---

# Parte 4 — Dados não relacionais e armazenamento

## Questão 27

Uma aplicação precisa armazenar imagens, vídeos e documentos na nuvem.

Qual serviço é mais apropriado?

A. Azure Blob Storage
B. Azure SQL Database
C. Azure Stream Analytics
D. Azure Table Storage

---

## Questão 28

Qual tipo de blob é utilizado principalmente para discos de máquinas virtuais?

A. Append Blob
B. Block Blob
C. Page Blob
D. Archive Blob

---

## Questão 29

Uma aplicação grava continuamente novas informações no final de um arquivo de log.

Qual tipo de blob é adequado?

A. Page Blob
B. Append Blob
C. Table Blob
D. SQL Blob

---

## Questão 30

Qual camada de acesso do Blob Storage possui menor custo de armazenamento, mas exige reidratação antes do acesso aos dados?

A. Hot
B. Cool
C. Cold
D. Archive

---

## Questão 31

Uma política move arquivos automaticamente de Hot para Cool, depois para Cold e Archive conforme envelhecem.

Qual recurso está sendo utilizado?

A. Lifecycle Management
B. Elastic Pool
C. Unity Catalog
D. Stream Analytics

---

## Questão 32

Qual opção de redundância distribui cópias dos dados entre zonas de disponibilidade da mesma região?

A. LRS
B. GRS
C. ZRS
D. RA-GRS

---

## Questão 33

O Azure Data Lake Storage Gen2 adiciona qual recurso importante ao Blob Storage?

A. SQL Server
B. Hierarchical Namespace
C. Graph API
D. Elastic Pool

---

## Questão 34

Qual serviço é utilizado para compartilhamento de arquivos usando protocolos como SMB e NFS?

A. Azure Files
B. Azure Cosmos DB
C. Azure Stream Analytics
D. Azure Data Explorer

---

## Questão 35

No Azure Table Storage, qual combinação identifica uma entidade?

A. PrimaryKey + ForeignKey
B. Dataset + Pipeline
C. RowKey + Index
D. PartitionKey + RowKey

---

## Questão 36

Qual afirmação sobre Azure Table Storage está correta?

A. Exige esquema relacional rígido.
B. É um armazenamento NoSQL chave-valor.
C. Utiliza foreign keys obrigatoriamente.
D. Foi projetado para armazenar VHDs.

---

# Parte 5 — Azure Cosmos DB

## Questão 37

Qual serviço é um banco NoSQL PaaS totalmente gerenciado e projetado para distribuição global?

A. Azure Files
B. Azure SQL Database
C. Azure Cosmos DB
D. Azure Data Factory

---

## Questão 38

Qual é a hierarquia correta dos principais recursos do Cosmos DB?

A. Account → Database → Container → Item
B. Database → Account → Item → Container
C. Container → Account → Database → Item
D. Item → Container → Database → Account

---

## Questão 39

Qual API nativa do Cosmos DB trabalha com documentos JSON?

A. Gremlin
B. Cassandra
C. MongoDB
D. Cosmos DB for NoSQL

---

## Questão 40

Qual API do Cosmos DB é apropriada para uma aplicação existente baseada em MongoDB?

A. Cosmos DB for Table
B. Cosmos DB for MongoDB
C. Cosmos DB for Gremlin
D. Cosmos DB for Cassandra

---

## Questão 41

Qual API do Cosmos DB utiliza o modelo de família de colunas?

A. Apache Cassandra
B. Gremlin
C. NoSQL
D. Table

---

## Questão 42

Uma aplicação precisa modelar uma rede social na qual os relacionamentos entre usuários são tão importantes quanto os próprios usuários.

Qual API é adequada?

A. MongoDB
B. Table
C. Apache Gremlin
D. Apache Cassandra

---

## Questão 43

Como o Cosmos DB mede capacidade de processamento?

A. DTUs exclusivamente
B. RU/s
C. Terabytes por segundo
D. DAX Units

---

## Questão 44

Qual nível de consistência garante que uma leitura reflita a gravação mais recente?

A. Eventual
B. Session
C. Consistent Prefix
D. Strong

---

## Questão 45

Qual nível de consistência é garantido dentro de uma sessão de cliente?

A. Session
B. Eventual
C. Strong
D. Bounded Staleness

---

## Questão 46

Qual recurso é importante para distribuir dados do Cosmos DB de maneira equilibrada entre partições?

A. Foreign Key
B. Stored Procedure
C. Partition Key
D. View

---

# Parte 6 — Analytics em larga escala

## Questão 47

Uma empresa precisa armazenar dados estruturados, semiestruturados e não estruturados em arquivos para análise posterior com Spark.

Qual arquitetura é mais adequada?

A. Banco OLTP
B. Data Lake
C. Elastic Pool
D. Azure Files

---

## Questão 48

Qual tecnologia é utilizada para processamento distribuído em plataformas como Azure Databricks?

A. Apache Spark
B. SMB
C. T-SQL exclusivamente
D. Azure RBAC

---

## Questão 49

Qual serviço está principalmente associado à criação e orquestração de pipelines de integração de dados?

A. Azure Event Hubs
B. Azure Cosmos DB
C. Azure Data Factory
D. Azure Files

---

## Questão 50

Qual serviço é mais associado a processamento distribuído, notebooks e Apache Spark?

A. Azure Files
B. Azure SQL Database
C. Azure Stream Analytics
D. Azure Databricks

---

## Questão 51

Qual formato adiciona recursos como transações, imposição de esquema e controle de versão sobre arquivos Parquet?

A. Delta Lake
B. XML
C. CSV
D. SMB

---

## Questão 52

No Microsoft Fabric, qual recurso permite acessar dados externos como se eles estivessem no OneLake sem copiá-los?

A. Activator
B. Shortcut
C. Elastic Pool
D. Page Blob

---

## Questão 53

Qual recurso do Microsoft Fabric replica continuamente dados de bancos externos para o OneLake?

A. Dataflow
B. Direct Lake
C. Mirroring
D. VertiPaq

---

## Questão 54

Qual armazenamento é mais adequado quando os dados são estruturados, o principal acesso é SQL e a finalidade é analytics empresarial?

A. Eventhouse
B. SQL Database transacional
C. Blob Container
D. Fabric Warehouse

---

# Parte 7 — Streaming e tempo real

## Questão 55

Qual serviço é utilizado principalmente para ingestão de grandes volumes de eventos?

A. Azure Event Hubs
B. Azure SQL Database
C. Azure Files
D. Azure Table Storage

---

## Questão 56

Qual serviço é especialmente voltado para comunicação e eventos provenientes de dispositivos IoT?

A. Azure Event Hubs
B. Azure IoT Hub
C. Azure Data Factory
D. Azure SQL Managed Instance

---

## Questão 57

Uma solução recebe eventos pelo Event Hubs, precisa agregá-los continuamente e gravar o resultado em Azure SQL Database.

Qual serviço pode executar esse processamento de streaming?

A. Azure Files
B. Azure Table Storage
C. Azure Stream Analytics
D. Azure SQL Managed Instance

---

## Questão 58

No Microsoft Fabric Real-Time Intelligence, qual componente é otimizado para eventos, logs e séries temporais e utiliza KQL?

A. Warehouse
B. Lakehouse
C. Dataflow Gen2
D. Eventhouse

---

# Parte 8 — Power BI e visualização

## Questão 59

Qual visual é mais adequado para analisar a relação entre duas medidas numéricas?

A. Scatter Plot
B. Card
C. Pie Chart
D. Table

---

## Questão 60

Em um modelo analítico, qual estrutura normalmente armazena métricas como quantidade vendida e receita?

A. Dimension Table
B. Fact Table
C. Hierarchy
D. Workspace

---

# Gabarito

| Questão | Resposta |
| ------: | :------: |
|       1 |     C    |
|       2 |     A    |
|       3 |     D    |
|       4 |     B    |
|       5 |     C    |
|       6 |     A    |
|       7 |     B    |
|       8 |     C    |
|       9 |     D    |
|      10 |     A    |
|      11 |     C    |
|      12 |     B    |
|      13 |     D    |
|      14 |     A    |
|      15 |     C    |
|      16 |     B    |
|      17 |     A    |
|      18 |     D    |
|      19 |     B    |
|      20 |     A    |
|      21 |     C    |
|      22 |     D    |
|      23 |     A    |
|      24 |     B    |
|      25 |     C    |
|      26 |     D    |
|      27 |     A    |
|      28 |     C    |
|      29 |     B    |
|      30 |     D    |
|      31 |     A    |
|      32 |     C    |
|      33 |     B    |
|      34 |     A    |
|      35 |     D    |
|      36 |     B    |
|      37 |     C    |
|      38 |     A    |
|      39 |     D    |
|      40 |     B    |
|      41 |     A    |
|      42 |     C    |
|      43 |     B    |
|      44 |     D    |
|      45 |     A    |
|      46 |     C    |
|      47 |     B    |
|      48 |     A    |
|      49 |     C    |
|      50 |     D    |
|      51 |     A    |
|      52 |     B    |
|      53 |     C    |
|      54 |     D    |
|      55 |     A    |
|      56 |     B    |
|      57 |     C    |
|      58 |     D    |
|      59 |     A    |
|      60 |     B    |

---

# Distribuição do simulado

| Tema                          | Questões |
| ----------------------------- | -------: |
| Fundamentos de dados          |      1–8 |
| Dados relacionais e SQL       |     9–18 |
| Serviços relacionais no Azure |    19–26 |
| Armazenamento não relacional  |    27–36 |
| Azure Cosmos DB               |    37–46 |
| Analytics em larga escala     |    47–54 |
| Streaming e tempo real        |    55–58 |
| Power BI e visualização       |    59–60 |

---

> Este simulado foi criado como material complementar de estudo para a certificação **Microsoft Azure Data Fundamentals (DP-900)**. As questões têm finalidade educacional e não representam questões oficiais do exame Microsoft.
