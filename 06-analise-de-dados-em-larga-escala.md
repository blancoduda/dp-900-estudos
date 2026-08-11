# 06 — Análise de dados em larga escala

> Anotações de estudo para a certificação **Microsoft Azure Data Fundamentals (DP-900)**.

A análise em larga escala combina conceitos tradicionais de **Data Warehouse e Business Intelligence** com tecnologias de **Big Data**, processamento distribuído, Data Lakes e arquiteturas Lakehouse.

Entre as principais plataformas estudadas estão:

* Microsoft Fabric;
* Azure Databricks;
* Apache Spark;
* Delta Lake;
* Azure Data Factory;
* Fabric Data Factory.

---

# 1. O que é análise em larga escala?

Soluções analíticas em grande escala precisam trabalhar com:

* grandes volumes de dados;
* diferentes formatos;
* múltiplas fontes;
* dados históricos;
* dados em lote;
* dados em streaming.

Uma arquitetura desse tipo pode combinar:

```text
Dados transacionais
        +
Arquivos
        +
Streaming
        ↓
Ingestão e processamento
        ↓
Armazenamento analítico
        ↓
Modelo semântico
        ↓
BI / Analytics
```

Soluções de Big Data costumam utilizar mecanismos de processamento distribuído, como o **Apache Spark**, para processar grandes volumes de dados em paralelo.

---

# 2. Arquitetura analítica em larga escala

Uma arquitetura analítica geralmente possui cinco grandes etapas:

```text
1. Ingestão e processamento
        ↓
2. Repositório analítico
        ↓
3. Modelo analítico
        ↓
4. Visualização
        ↓
5. Análise assistida por IA
```

---

# 3. Ingestão e processamento

Os dados podem vir de diferentes origens:

```text
Bancos de dados
Arquivos
APIs
Sistemas transacionais
Streaming
IoT
        ↓
     Ingestão
```

Durante esse processo, podem ser utilizados padrões como:

```text
ETL
Extract
Transform
Load
```

ou:

```text
ELT
Extract
Load
Transform
```

No **ETL**, os dados são transformados antes de serem carregados no armazenamento analítico.

No **ELT**, os dados são carregados primeiro e transformados posteriormente.

Também podem existir dois modelos de processamento:

* processamento em lote;
* processamento de streaming.

---

# 4. Processamento distribuído

Para processar grandes volumes de dados, sistemas analíticos podem utilizar vários computadores trabalhando em conjunto.

```text
Grande conjunto de dados
        ↓
      Cluster
   ↙    ↓    ↘
 Nó 1   Nó 2   Nó 3
   ↘    ↓    ↙
     Resultado
```

Esse modelo permite processar partes diferentes dos dados em paralelo.

O **Apache Spark** é um dos principais mecanismos utilizados nesse tipo de cenário.

---

# 5. Repositórios analíticos

Os principais modelos de armazenamento estudados são:

```text
Repositórios analíticos
│
├── Data Warehouse
├── Data Lake
└── Data Lakehouse
```

---

# 6. Data Warehouse

Um **Data Warehouse** é um banco de dados relacional otimizado para análise.

É adequado quando:

* os dados são estruturados;
* existe um esquema definido;
* SQL será utilizado;
* são necessárias consultas analíticas;
* os dados serão utilizados em BI.

```text
Sistemas transacionais
        ↓
Transformação
        ↓
Data Warehouse
        ↓
SQL
        ↓
BI
```

---

# 7. Tabelas fato e dimensão

Um Data Warehouse normalmente utiliza modelagem dimensional.

Os dados são organizados em:

```text
Tabela Fato
    +
Tabelas Dimensão
```

---

## Tabela fato

A tabela fato contém principalmente **valores numéricos e eventos de negócio**.

Exemplo:

```text
FATO_VENDAS
│
├── id_produto
├── id_cliente
├── id_data
├── quantidade
└── valor
```

---

## Tabelas dimensão

Representam entidades utilizadas para analisar os fatos.

Exemplos:

```text
DIM_PRODUTO
DIM_CLIENTE
DIM_TEMPO
DIM_LOJA
```

Isso permite perguntas como:

```text
Receita
por produto
por loja
por cliente
por mês
```

---

# 8. Star Schema

Quando uma tabela fato central se relaciona diretamente com várias dimensões, temos um **Star Schema**.

```text
          DIM_CLIENTE
               |
DIM_DATA — FATO_VENDAS — DIM_PRODUTO
               |
            DIM_LOJA
```

O formato visual lembra uma estrela.

---

# 9. Snowflake Schema

O **Snowflake Schema** expande o Star Schema adicionando tabelas relacionadas às dimensões.

Exemplo:

```text
FATO_VENDAS
     |
 DIM_PRODUTO
     |
DIM_CATEGORIA
```

Isso permite representar hierarquias mais detalhadas.

---

# 10. Data Lake

Um **Data Lake** é um armazenamento baseado principalmente em arquivos.

Pode armazenar:

* dados estruturados;
* dados semiestruturados;
* dados não estruturados.

```text
Data Lake
│
├── CSV
├── JSON
├── Parquet
├── Imagens
├── Logs
└── Outros arquivos
```

---

# 11. Schema-on-read

Data Lakes normalmente utilizam uma abordagem conhecida como:

**Schema-on-read**

Isso significa que o esquema é aplicado quando o dado é lido para análise.

```text
Dados armazenados
sem esquema rígido
        ↓
     Leitura
        ↓
Esquema aplicado
        ↓
     Análise
```

Isso oferece maior flexibilidade para armazenar diferentes formatos de dados.

---

# 12. Data Lakehouse

O **Data Lakehouse** combina características de:

```text
Data Lake
   +
Data Warehouse
```

Os dados continuam armazenados como arquivos, mas podem ser expostos como tabelas e consultados utilizando SQL.

```text
Arquivos
   ↓
Data Lake
   ↓
Delta Lake
   ↓
Tabelas
   ↓
SQL / Spark / BI
```

---

# 13. Delta Lake

O **Delta Lake** é fundamental nas arquiteturas Lakehouse estudadas.

Ele adiciona recursos de armazenamento relacional sobre arquivos Parquet.

Entre eles:

* transações;
* imposição de esquema;
* consistência;
* controle de versão;
* suporte a batch;
* suporte a streaming.

```text
Parquet
   +
Transaction Log
   ↓
Delta Lake
```

Microsoft Fabric e Azure Databricks utilizam Delta Lake em suas arquiteturas Lakehouse.

---

# 14. Comparação: Warehouse x Lake x Lakehouse

| Característica          | Data Warehouse | Data Lake      | Lakehouse          |
| ----------------------- | -------------- | -------------- | ------------------ |
| Armazenamento principal | Tabelas        | Arquivos       | Arquivos + tabelas |
| Dados estruturados      | Sim            | Sim            | Sim                |
| Dados semiestruturados  | Limitado       | Sim            | Sim                |
| Dados não estruturados  | Limitado       | Sim            | Sim                |
| SQL                     | Sim            | Via engines    | Sim                |
| Schema                  | Forte          | Schema-on-read | Suporta schema     |
| BI                      | Excelente      | Possível       | Excelente          |
| Spark                   | Não é foco     | Comum          | Comum              |

---

# 15. Modelos analíticos

Nem sempre os usuários consultam diretamente o Data Warehouse ou Lakehouse.

É comum criar um **modelo analítico** entre os dados e os relatórios.

Historicamente, esses modelos eram frequentemente chamados de **cubos OLAP**.

Atualmente, o conceito mais comum é o **modelo semântico**.

```text
Data Warehouse / Lakehouse
          ↓
    Modelo semântico
          ↓
       Power BI
```

---

# 16. Modelo semântico

Um modelo semântico pode definir:

* tabelas;
* relacionamentos;
* medidas;
* hierarquias;
* regras de negócio.

No ecossistema Microsoft, cálculos podem ser definidos utilizando **DAX**.

```text
Dados
   ↓
Modelo semântico
│
├── Relacionamentos
├── Medidas
├── Hierarquias
└── Regras
   ↓
Power BI
```

---

# 17. Direct Lake

No Microsoft Fabric, modelos semânticos podem utilizar o modo **Direct Lake**.

Nesse modelo, o Power BI pode ler tabelas Delta diretamente do OneLake.

```text
OneLake
   ↓
Delta Tables
   ↓
Direct Lake
   ↓
Power BI
```

Isso reduz a necessidade de importar ou pré-agregar os dados.

---

# 18. Microsoft Fabric

O **Microsoft Fabric** é uma plataforma SaaS unificada para análise de dados.

Ele reúne várias partes da arquitetura analítica dentro de um único workspace.

```text
Microsoft Fabric
│
├── OneLake
├── Lakehouse
├── Warehouse
├── Data Factory
└── Power BI
```

---

# 19. OneLake

O **OneLake** é a camada de armazenamento compartilhada do Fabric.

Diferentes workloads podem utilizar os mesmos dados.

```text
           OneLake
         /    |    \
Lakehouse Warehouse Power BI
```

Isso reduz a necessidade de criar vários silos de armazenamento.

No Fabric, o Delta Lake é utilizado como formato aberto padrão para dados Lakehouse.

---

# 20. Fabric Lakehouse

O **Fabric Lakehouse** combina armazenamento em Data Lake com uma experiência tabular e SQL.

Características:

* dados armazenados em Delta Lake;
* suporte a Spark;
* suporte a notebooks;
* endpoint de análise SQL;
* integração com Power BI.

```text
OneLake
   ↓
Delta Lake
   ↓
Fabric Lakehouse
   ├── Spark
   ├── SQL
   └── Power BI
```

---

# 21. Fabric Warehouse

O **Fabric Warehouse** é um Data Warehouse relacional totalmente gerenciado.

É adequado principalmente para:

* dados estruturados;
* equipes que trabalham com SQL;
* esquema rígido;
* consultas analíticas;
* BI;
* múltiplos usuários simultâneos.

---

# 22. Fabric Lakehouse x Fabric Warehouse

| Cenário                | Lakehouse     | Warehouse      |
| ---------------------- | ------------- | -------------- |
| Dados estruturados     | Sim           | Sim            |
| Dados semiestruturados | Sim           | Menos indicado |
| Spark                  | Sim           | Não é foco     |
| Notebooks              | Sim           | Não é foco     |
| SQL                    | Sim           | Sim            |
| Machine Learning       | Mais adequado | Menos focado   |
| BI tradicional         | Sim           | Excelente      |
| Schema rígido          | Flexível      | Forte          |

As anotações indicam o **Lakehouse** para dados mistos e workflows de Spark/ML, enquanto o **Warehouse** é mais indicado quando os dados são estruturados e o uso principal é SQL.

---

# 23. Fabric Data Factory

O **Fabric Data Factory** é utilizado para ingestão, movimentação e transformação de dados dentro do Fabric.

Ele possui duas ferramentas principais:

```text
Fabric Data Factory
│
├── Pipelines
└── Dataflows Gen2
```

---

# 24. Pipelines

Pipelines permitem orquestrar várias atividades.

```text
Fonte
  ↓
Copy Data
  ↓
Notebook
  ↓
Transformação
  ↓
Destino
```

As atividades podem ser executadas:

* em sequência;
* em paralelo.

Também podem:

* carregar dados;
* executar procedures;
* chamar notebooks;
* aplicar lógica personalizada.

---

# 25. Dataflows Gen2

Os **Dataflows Gen2** oferecem uma experiência visual e de baixo código para transformação de dados.

Utilizam **Power Query**.

```text
Fonte
  ↓
Power Query
  ↓
Transformação
  ↓
Destino
```

São adequados quando é necessário transformar dados sem escrever muito código.

---

# 26. OneLake Shortcuts

Um **Shortcut** cria uma referência para dados armazenados externamente.

Exemplos de origens:

* ADLS Gen2;
* Amazon S3;
* Google Cloud Storage;
* outros locais do OneLake.

```text
Dados no S3
     ↓
Shortcut
     ↓
Fabric Lakehouse
```

Os dados continuam no local original.

Ou seja:

```text
Sem copiar
Sem duplicar
Sem movimentar
```

---

# 27. Fabric Mirroring

O **Mirroring** replica continuamente dados de bancos externos para o OneLake.

Exemplos citados:

* Azure SQL Database;
* Snowflake;
* Azure Cosmos DB.

```text
Banco externo
      ↓
   Mirroring
      ↓
    OneLake
```

A replicação ocorre sem a necessidade de construir um pipeline personalizado.

Os dados são armazenados em Delta Lake e podem ser consultados no endpoint SQL.

---

# 28. Eventstream

O **Fabric Eventstream** é utilizado para ingestão de dados de streaming.

Pode receber eventos de fontes como:

* Azure Event Hubs;
* Apache Kafka;
* Azure IoT Hub;
* endpoints personalizados.

```text
Eventos
   ↓
Eventstream
   ↓
Filtrar / transformar
   ↓
Lakehouse / KQL / Real-Time Intelligence
```

---

# 29. Fabric Notebooks

Os **Fabric Notebooks** são baseados em Apache Spark.

Podem utilizar:

* PySpark;
* Python;
* Scala;
* R;
* SQL.

São adequados quando:

* não existe um conector pronto;
* é necessária lógica personalizada;
* é necessário trabalhar diretamente com código.

```text
API / Banco / Arquivo
        ↓
Fabric Notebook
        ↓
Transformação
        ↓
Delta Table / Warehouse
```

Também podem ser agendados dentro de pipelines.

---

# 30. Azure Data Factory

O **Azure Data Factory — ADF** é o serviço independente do Azure para integração e movimentação de dados.

Ele é útil especialmente quando:

* a solução não está totalmente dentro do Fabric;
* existem fontes locais;
* existem ambientes híbridos;
* o destino é outro serviço Azure;
* existem sistemas externos.

```text
Fonte local / Azure / externa
           ↓
    Azure Data Factory
           ↓
         Destino
```

---

# 31. Fabric Data Factory x Azure Data Factory

```text
Fabric Data Factory
→ integrado ao Microsoft Fabric

Azure Data Factory
→ serviço Azure independente
```

Ambos trabalham com conceitos semelhantes de pipelines e integração de dados.

---

# 32. Azure Databricks

O **Azure Databricks** é uma plataforma de análise baseada em **Apache Spark**.

É voltado principalmente para:

* engenharia de dados;
* processamento distribuído;
* ciência de dados;
* SQL analytics;
* machine learning;
* Lakehouse.

Utiliza o **Delta Lake** como formato de armazenamento principal.

---

# 33. Componentes do Azure Databricks

Entre os componentes estudados estão:

```text
Azure Databricks
│
├── Databricks Lakehouse
├── Databricks SQL
├── Notebooks
├── Unity Catalog
└── Genie
```

---

# 34. Databricks Lakehouse

O **Databricks Lakehouse** utiliza Delta Lake como camada de armazenamento.

Pode suportar no mesmo ambiente:

* SQL;
* engenharia de dados;
* ciência de dados;
* Machine Learning.

```text
Delta Lake
    ↓
Databricks Lakehouse
    ├── SQL
    ├── Spark
    └── ML
```

---

# 35. Databricks SQL

O **Databricks SQL** permite executar consultas analíticas utilizando SQL sobre tabelas Delta.

As anotações mencionam recursos como:

* SQL Warehouse;
* histórico de consultas;
* dashboards;
* alertas.

---

# 36. Databricks Notebooks

Notebooks do Databricks suportam:

* PySpark;
* Python;
* Scala;
* SQL;
* R.

Podem ser utilizados para:

* ingestão;
* exploração;
* transformação;
* processamento;
* Machine Learning.

```text
Fonte
  ↓
Databricks Notebook
  ↓
Spark
  ↓
Delta Lake
```

---

# 37. Lakeflow Spark Declarative Pipelines

O **Lakeflow Spark Declarative Pipelines** permite criar pipelines declarativos no Databricks.

Nesse modelo, define-se o estado esperado dos dados.

```text
Definir resultado desejado
        ↓
Lakeflow
        ↓
Dependências
Ordenação
Incremental
        ↓
Delta Lake
```

O Databricks gerencia aspectos como:

* ordem de execução;
* dependências;
* processamento incremental.

---

# 38. Unity Catalog

O **Unity Catalog** aparece nas anotações como uma camada centralizada de governança do Databricks.

Ele oferece:

* controle de acesso;
* linhagem;
* descoberta dos dados;
* governança de ativos de dados e IA.

---

# 39. Genie

O **Genie** permite realizar perguntas sobre os dados utilizando linguagem natural.

```text
Usuário
   ↓
Pergunta em linguagem natural
   ↓
Genie
   ↓
SQL
   ↓
Resultado
```

O sistema gera e executa consultas SQL automaticamente.

---

# 40. Análise assistida por IA

As anotações também apresentam IA como uma camada adicional das plataformas analíticas modernas.

Alguns exemplos são:

```text
Power BI
→ Q&A

Microsoft Fabric
→ Copilot

Azure Databricks
→ Genie
```

Esses recursos permitem utilizar linguagem natural para:

* consultar dados;
* criar SQL;
* gerar DAX;
* explicar tendências;
* resumir informações.

---

# 41. Comparação Fabric x Databricks

| Característica          | Microsoft Fabric     | Azure Databricks              |
| ----------------------- | -------------------- | ----------------------------- |
| Modelo                  | SaaS                 | Serviço gerenciado no Azure   |
| Armazenamento principal | OneLake              | Delta Lake                    |
| Spark                   | Sim                  | Sim                           |
| SQL                     | Sim                  | Sim                           |
| Power BI                | Integrado            | Pode integrar                 |
| Engenharia de dados     | Sim                  | Forte                         |
| Machine Learning        | Sim                  | Forte                         |
| Notebooks               | Sim                  | Sim                           |
| Perfil                  | Plataforma integrada | Mais orientado a código/Spark |
| Lakehouse               | Fabric Lakehouse     | Databricks Lakehouse          |

---

# 42. Comparação de formas de ingestão no Fabric

| Recurso       | Quando utilizar                       |
| ------------- | ------------------------------------- |
| Pipeline      | Orquestração e movimentação           |
| Dataflow Gen2 | Transformação visual com Power Query  |
| Shortcut      | Acessar dados externos sem copiar     |
| Mirroring     | Replicar bancos continuamente         |
| Eventstream   | Streaming de eventos                  |
| Notebook      | Transformação personalizada em código |

---

# 🧠 Mapa mental

```text
ANÁLISE EM LARGA ESCALA
│
├── Ingestão
│   ├── ETL
│   ├── ELT
│   ├── Batch
│   └── Streaming
│
├── Armazenamento
│   ├── Data Warehouse
│   │   ├── Fact
│   │   ├── Dimension
│   │   └── Star Schema
│   │
│   ├── Data Lake
│   │   └── Schema-on-read
│   │
│   └── Lakehouse
│       └── Delta Lake
│
├── Microsoft Fabric
│   ├── OneLake
│   ├── Lakehouse
│   ├── Warehouse
│   ├── Data Factory
│   └── Power BI
│
└── Azure Databricks
    ├── Apache Spark
    ├── Delta Lake
    ├── Notebooks
    ├── Databricks SQL
    ├── Unity Catalog
    └── Genie
```

---

# ✅ Pontos que eu levaria para a prova

* **Big Data** → grandes volumes e variedade de dados.
* **Apache Spark** → processamento distribuído em larga escala.
* **ETL** → transforma antes de carregar.
* **ELT** → carrega antes de transformar.
* **Data Warehouse** → relacional, estruturado e otimizado para análise.
* **Tabela fato** → métricas e eventos de negócio.
* **Tabela dimensão** → entidades utilizadas para analisar os fatos.
* **Star Schema** → fato central relacionada diretamente às dimensões.
* **Data Lake** → armazenamento de arquivos de diferentes formatos.
* **Schema-on-read** → esquema aplicado no momento da leitura.
* **Lakehouse** → combina Data Lake e Data Warehouse.
* **Delta Lake** → Parquet + recursos transacionais e de esquema.
* **Modelo semântico** → camada analítica usada para BI.
* **Direct Lake** → leitura de tabelas Delta diretamente do OneLake.
* **OneLake** → camada de armazenamento compartilhada do Microsoft Fabric.
* **Fabric Lakehouse** → Lakehouse com Spark e endpoint SQL.
* **Fabric Warehouse** → Data Warehouse relacional gerenciado.
* **Fabric Data Factory** → pipelines e Dataflows Gen2.
* **Shortcut** → referência dados externos sem copiá-los.
* **Mirroring** → replica bancos externos continuamente para o OneLake.
* **Eventstream** → ingestão de streaming.
* **Fabric Notebook** → Spark e transformações baseadas em código.
* **Azure Data Factory** → integração de dados fora ou além do Fabric.
* **Azure Databricks** → Spark, engenharia de dados e Lakehouse.
* **Databricks SQL** → análise SQL sobre tabelas Delta.
* **Lakeflow** → pipelines declarativos do Databricks.
* **Unity Catalog** → governança.
* **Genie** → consultas aos dados usando linguagem natural.

---

> Material organizado a partir das minhas próprias anotações durante a preparação para a certificação **Microsoft Azure Data Fundamentals (DP-900)**.

