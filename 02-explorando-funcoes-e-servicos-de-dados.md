# 02 — Explorando funções e serviços de dados

> Anotações de estudo para a certificação **Microsoft Azure Data Fundamentals (DP-900)**.

Este módulo aborda os principais **papéis profissionais relacionados a dados** e os principais **serviços de dados disponíveis no ecossistema Microsoft Azure**.

---

# 1. Funções profissionais no mundo dos dados

As soluções modernas de dados envolvem diferentes profissionais, cada um com responsabilidades específicas.

Entre os principais papéis estão:

* Administrador de Banco de Dados;
* Engenheiro de Dados;
* Analista de Dados;
* Engenheiro de IA.

---

## 🗄️ Administrador de Banco de Dados

O **Database Administrator — DBA** é responsável principalmente pela administração, disponibilidade, segurança e desempenho dos bancos de dados.

Entre suas atividades estão:

* gerenciar bancos de dados;
* atribuir permissões aos usuários;
* realizar e gerenciar backups;
* restaurar dados em caso de falhas;
* implementar e manter sistemas de banco de dados;
* monitorar disponibilidade;
* otimizar desempenho;
* implementar políticas de segurança;
* criar estratégias de recuperação;
* controlar privilégios e acessos.

Também atua tanto em ambientes locais quanto em nuvem.

### Resumo

```text
DBA
│
├── Administração
├── Segurança
├── Backup
├── Recovery
├── Disponibilidade
└── Performance
```

> O DBA se preocupa principalmente com a **operação e manutenção do banco de dados**.

---

# 2. Engenheiro de Dados

O **Data Engineer** trabalha principalmente na movimentação, transformação, organização e disponibilização dos dados.

Entre suas responsabilidades estão:

* implementar pipelines de dados;
* realizar limpeza dos dados;
* transformar informações entre diferentes sistemas;
* implementar processos de ingestão;
* identificar regras de governança;
* criar armazenamentos de dados para cargas analíticas;
* monitorar pipelines;
* garantir que as cargas sejam executadas corretamente;
* trabalhar com dados locais e em nuvem;
* colaborar com stakeholders na criação de soluções relacionadas a dados.

Também precisa considerar aspectos relacionados à privacidade e governança dos dados.

### Exemplo de fluxo

```text
Sistema A
   ↓
Ingestão
   ↓
Transformação
   ↓
Pipeline
   ↓
Armazenamento
   ↓
Analytics / BI
```

### Resumo

```text
Data Engineer
│
├── Ingestão
├── Pipelines
├── ETL / ELT
├── Transformação
├── Data Lake / Warehouse
├── Governança
└── Monitoramento
```

> O engenheiro de dados cria a **infraestrutura e os fluxos que permitem que os dados sejam utilizados**.

---

# 3. Analista de Dados

O **Data Analyst** transforma dados em informações que possam apoiar decisões de negócio.

Suas principais atividades incluem:

* explorar dados;
* analisar informações;
* identificar tendências;
* identificar relações entre variáveis;
* construir modelos analíticos;
* criar relatórios;
* criar dashboards;
* desenvolver visualizações;
* transformar dados brutos em insights relevantes.

O trabalho normalmente começa a partir de uma necessidade ou requisito de negócio.

```text
Dados
  ↓
Exploração
  ↓
Análise
  ↓
Modelo
  ↓
Visualização
  ↓
Insight
  ↓
Decisão
```

### Resumo

```text
Data Analyst
│
├── Análise
├── Modelagem
├── Métricas
├── Visualização
├── Relatórios
└── Insights
```

> O analista de dados utiliza os dados para **responder perguntas e apoiar decisões**.

---

# 4. Engenheiro de IA

O **AI Engineer** desenvolve e integra recursos baseados em inteligência artificial.

Entre suas atividades estão:

* trabalhar com grandes modelos de linguagem;
* desenvolver soluções utilizando IA;
* criar pipelines de Machine Learning;
* integrar IA a aplicações;
* utilizar fontes de dados para habilitar cenários inteligentes;
* implementar classificação automatizada;
* desenvolver aplicações de geração de conteúdo;
* criar soluções de chat utilizando dados corporativos.

O engenheiro de IA também trabalha em conjunto com engenheiros e analistas de dados.

```text
Data Engineer
      ↓
Dados preparados
      ↓
AI Engineer
      ↓
Modelos / IA
      ↓
Data Analyst / Aplicações
      ↓
Insights
```

Um dos serviços mencionados neste contexto é o **Microsoft Foundry**, utilizado na criação, teste e implantação de soluções de IA.

---

# 5. Comparando as funções

| Função        | Principal responsabilidade                |
| ------------- | ----------------------------------------- |
| DBA           | Administrar bancos de dados               |
| Data Engineer | Construir pipelines e estruturas de dados |
| Data Analyst  | Analisar dados e gerar insights           |
| AI Engineer   | Construir soluções baseadas em IA         |

### Forma rápida de lembrar

```text
DBA
→ mantém o banco

Data Engineer
→ movimenta e prepara os dados

Data Analyst
→ interpreta os dados

AI Engineer
→ cria soluções inteligentes usando os dados
```

---

# 6. Serviços de dados no Azure

O Azure possui diferentes serviços voltados para armazenamento, processamento, integração, análise e governança de dados.

Os principais serviços abordados neste módulo são:

* Azure SQL;
* Azure Database for MySQL;
* Azure Database for PostgreSQL;
* Azure Cosmos DB;
* Azure Storage;
* Azure Data Factory;
* Microsoft Fabric;
* Microsoft Fabric IQ;
* Power BI;
* Azure Databricks;
* Azure Stream Analytics;
* Azure Data Explorer;
* Microsoft Purview;
* Microsoft Foundry.

---

# 7. Azure SQL

**Azure SQL** é o nome utilizado para uma família de soluções de banco de dados relacionais baseadas no mecanismo do **Microsoft SQL Server**.

As principais opções são:

### Azure SQL Database

Banco de dados oferecido como **PaaS — Platform as a Service**.

É totalmente gerenciado e hospedado no Azure.

```text
Azure SQL Database
→ PaaS
→ Banco gerenciado
→ Menor responsabilidade administrativa
```

---

### Azure SQL Managed Instance

Também é uma solução PaaS.

Oferece uma instância hospedada do SQL Server com manutenção automatizada e maior flexibilidade de configuração.

```text
Azure SQL Managed Instance
→ PaaS
→ Maior compatibilidade com SQL Server
→ Maior flexibilidade
```

---

### SQL Server em Azure Virtual Machine

É uma máquina virtual executando uma instalação do SQL Server.

Nesse cenário existe maior controle sobre a configuração, mas também maior responsabilidade administrativa.

```text
SQL Server na VM
→ Maior controle
→ Maior responsabilidade
```

### Comparação simples

```text
Mais gerenciamento Microsoft
        ↑
Azure SQL Database
        ↓
Managed Instance
        ↓
SQL Server em VM
        ↓
Mais gerenciamento do cliente
```

Administradores de banco de dados normalmente provisionam esses serviços, enquanto engenheiros de dados podem utilizá-los como fontes para pipelines e analistas podem consultá-los para geração de relatórios.

---

# 8. Azure Database for MySQL

O **Azure Database for MySQL** permite utilizar MySQL como um serviço de banco de dados no Azure.

MySQL é um sistema de banco de dados relacional de código aberto muito utilizado em aplicações.

Um cenário bastante conhecido é a stack:

```text
LAMP

Linux
Apache
MySQL
PHP
```

É uma alternativa para organizações que já utilizam MySQL e desejam executar suas cargas no Azure.

---

# 9. Azure Database for PostgreSQL

O **Azure Database for PostgreSQL** oferece PostgreSQL como serviço no Azure.

O PostgreSQL é um banco de dados híbrido relacional-objeto.

Além de trabalhar com tabelas relacionais, permite utilizar tipos de dados personalizados.

```text
PostgreSQL
│
├── Relacional
└── Recursos objeto-relacionais
```

Tanto MySQL quanto PostgreSQL podem ser utilizados por administradores, engenheiros e analistas de dados.

---

# 10. Azure Cosmos DB

O **Azure Cosmos DB** é um serviço de banco de dados **NoSQL distribuído globalmente**.

Pode armazenar diferentes modelos de dados por meio de APIs.

Entre eles:

* documentos JSON;
* chave-valor;
* famílias de colunas;
* grafos.

```text
Azure Cosmos DB
│
├── Documento
├── Chave-valor
├── Família de colunas
└── Grafo
```

O Cosmos DB pode ser utilizado como parte da arquitetura de aplicações e também integrado a soluções analíticas.

---

# 11. Azure Storage

O **Azure Storage** fornece diferentes opções de armazenamento.

Entre elas:

### Blob Containers

Armazenamento escalável para arquivos e objetos binários.

```text
Blob
→ arquivos
→ imagens
→ vídeos
→ documentos
→ dados não estruturados
```

### Azure Files

Compartilhamentos de arquivos em rede.

Funcionam de forma semelhante aos compartilhamentos utilizados tradicionalmente em ambientes corporativos.

### Tables

Armazenamento no modelo **chave-valor**.

Adequado para aplicações que precisam ler e gravar valores rapidamente.

---

## Azure Storage e Data Lakes

Engenheiros de dados podem utilizar o Azure Storage para hospedar **Data Lakes**.

Nesse cenário, os blobs podem utilizar um **namespace hierárquico**, permitindo organizar os arquivos em diretórios e pastas.

---

# 12. Azure Data Factory

O **Azure Data Factory — ADF** é um serviço utilizado para criação e orquestração de pipelines de dados.

Permite:

* transferir dados;
* transformar dados;
* agendar pipelines;
* integrar diferentes fontes;
* executar processos ETL;
* integrar outros serviços Azure.

### Exemplo

```text
Banco de dados
      ↓
Azure Data Factory
      ↓
Extração
      ↓
Transformação
      ↓
Carga
      ↓
Data Warehouse
```

É uma ferramenta muito utilizada por engenheiros de dados.

Também existe uma versão integrada ao Microsoft Fabric chamada **Fabric Data Factory**.

---

# 13. Microsoft Fabric

O **Microsoft Fabric** é uma plataforma SaaS unificada para análise de dados.

Reúne diferentes recursos em um único ambiente baseado em navegador.

Entre eles:

* engenharia de dados;
* ingestão de dados;
* Data Factory;
* Data Lakehouse;
* Data Warehouse;
* ciência de dados;
* Machine Learning;
* análise em tempo real;
* Power BI;
* governança;
* bancos de dados.

O armazenamento compartilhado da plataforma é chamado de **OneLake**.

```text
Microsoft Fabric
│
├── Data Factory
├── Lakehouse
├── Warehouse
├── Data Science
├── Real-Time Intelligence
├── Power BI
└── OneLake
```

Uma característica importante é que a infraestrutura subjacente é gerenciada pela Microsoft.

---

# 14. Microsoft Fabric IQ

O **Microsoft Fabric IQ** busca oferecer um significado comercial consistente para os dados armazenados no OneLake.

A proposta é permitir que diferentes ferramentas, equipes e agentes de IA compartilhem a mesma compreensão dos conceitos empresariais.

Por exemplo:

```text
Customer
Order
Product
```

Esses conceitos podem ter definições compartilhadas dentro do ambiente.

Isso também permite que usuários realizem perguntas em linguagem natural com base na compreensão dos dados corporativos.

---

# 15. Power BI

O **Power BI** é a plataforma de Business Intelligence e visualização de dados da Microsoft.

É utilizado principalmente por analistas de dados para:

* conectar diferentes fontes;
* transformar dados;
* criar modelos analíticos;
* desenvolver relatórios;
* criar visualizações;
* compartilhar insights.

```text
Fonte
  ↓
Power BI
  ↓
Modelo semântico
  ↓
Relatório
  ↓
Dashboard / Insights
```

O Power BI também faz parte do ecossistema do **Microsoft Fabric**.

Dentro do Fabric, pode utilizar **modelos semânticos**, que definem:

* relações;
* medidas;
* lógica de negócio.

---

# 16. Azure Databricks

O **Azure Databricks** é uma plataforma de análise baseada em **Apache Spark**.

É voltado principalmente para:

* engenharia de dados;
* processamento em larga escala;
* ciência de dados;
* análise SQL;
* arquiteturas Lakehouse.

Um dos principais formatos utilizados é o **Delta Lake**.

```text
Azure Databricks
│
├── Apache Spark
├── Engenharia de Dados
├── Data Science
├── SQL Analytics
└── Delta Lake
```

Também possui suporte a notebooks para consulta e exploração de dados.

---

# 17. Azure Stream Analytics

O **Azure Stream Analytics** é utilizado para processamento de dados em tempo real.

Ele trabalha com um fluxo semelhante a:

```text
Entrada
   ↓
Stream Analytics
   ↓
Consulta / Processamento
   ↓
Saída
```

Pode ser utilizado para:

* processar streams;
* analisar eventos;
* transformar dados em tempo real;
* enviar resultados para outros serviços;
* alimentar visualizações em tempo real.

É especialmente relacionado a cenários de **streaming de dados**.

---

# 18. Azure Data Explorer

O **Azure Data Explorer** é uma plataforma totalmente gerenciada para análise de grandes volumes de dados.

É especialmente adequada para:

* logs;
* telemetria;
* dados de IoT;
* informações com timestamp.

```text
Logs
Telemetria
IoT
   ↓
Azure Data Explorer
   ↓
Consulta e análise
```

Tem foco em consultas de alto desempenho sobre grandes volumes de informações.

---

# 19. Microsoft Purview

O **Microsoft Purview** é voltado à governança e descoberta de dados.

Pode ser utilizado para:

* descobrir dados;
* catalogar informações;
* mapear dados;
* acompanhar linhagem;
* aplicar governança;
* encontrar fontes confiáveis.

### Linhagem

A linhagem permite acompanhar o caminho percorrido pelos dados.

```text
Fonte
  ↓
Pipeline
  ↓
Data Lake
  ↓
Warehouse
  ↓
Power BI
```

O Purview ajuda a entender de onde um dado veio e como ele foi transformado ao longo do processo.

---

# 20. Microsoft Foundry

O **Microsoft Foundry** é uma plataforma Azure voltada à criação e operação de soluções de inteligência artificial.

Pode ser utilizada por engenheiros de IA e desenvolvedores para:

* acessar modelos;
* desenvolver aplicações;
* testar soluções;
* implantar aplicações de IA;
* criar fluxos baseados em agentes;
* desenvolver chat sobre dados;
* integrar IA aos serviços de dados Azure.

```text
Dados
  ↓
Microsoft Foundry
  ↓
Modelos de IA
  ↓
Aplicações / Agentes
```

---

# 21. Visão geral dos serviços

| Serviço                       | Principal uso                                   |
| ----------------------------- | ----------------------------------------------- |
| Azure SQL Database            | Banco relacional gerenciado                     |
| Azure SQL Managed Instance    | SQL Server gerenciado com maior compatibilidade |
| SQL Server em Azure VM        | SQL Server com maior controle                   |
| Azure Database for MySQL      | MySQL gerenciado                                |
| Azure Database for PostgreSQL | PostgreSQL gerenciado                           |
| Azure Cosmos DB               | Banco NoSQL                                     |
| Azure Storage                 | Armazenamento de arquivos e objetos             |
| Azure Data Factory            | Pipelines e ETL                                 |
| Microsoft Fabric              | Plataforma integrada de analytics               |
| Fabric IQ                     | Significado empresarial compartilhado dos dados |
| Power BI                      | BI e visualização                               |
| Azure Databricks              | Engenharia e análise em escala                  |
| Azure Stream Analytics        | Streaming e processamento em tempo real         |
| Azure Data Explorer           | Logs, telemetria e análise temporal             |
| Microsoft Purview             | Governança e linhagem                           |
| Microsoft Foundry             | Desenvolvimento de soluções de IA               |

---

# 🧠 Resumo para revisão

```text
PROFISSIONAIS DE DADOS
│
├── DBA
│   └── banco / segurança / backup / performance
│
├── Data Engineer
│   └── pipelines / ETL / transformação
│
├── Data Analyst
│   └── análise / BI / insights
│
└── AI Engineer
    └── IA / modelos / aplicações


SERVIÇOS
│
├── Banco Relacional
│   ├── Azure SQL Database
│   ├── Managed Instance
│   ├── SQL Server VM
│   ├── MySQL
│   └── PostgreSQL
│
├── NoSQL
│   └── Cosmos DB
│
├── Storage
│   └── Azure Storage
│
├── Integração
│   └── Azure Data Factory
│
├── Analytics
│   ├── Microsoft Fabric
│   ├── Azure Databricks
│   └── Azure Data Explorer
│
├── Streaming
│   └── Azure Stream Analytics
│
├── BI
│   └── Power BI
│
├── Governança
│   └── Microsoft Purview
│
└── IA
    └── Microsoft Foundry
```

---

# ✅ Pontos que eu levaria para a prova

* **DBA** → administração, segurança, backup e desempenho.
* **Data Engineer** → pipelines, transformação e movimentação dos dados.
* **Data Analyst** → análise, visualização e geração de insights.
* **AI Engineer** → desenvolvimento e integração de soluções de IA.
* **Azure SQL Database** → banco relacional PaaS totalmente gerenciado.
* **Managed Instance** → maior compatibilidade com SQL Server.
* **SQL Server em VM** → maior controle e maior responsabilidade administrativa.
* **Cosmos DB** → banco de dados NoSQL distribuído globalmente.
* **Azure Storage** → armazenamento de arquivos, blobs e chave-valor.
* **Azure Data Factory** → pipelines, integração e ETL.
* **Microsoft Fabric** → plataforma SaaS unificada de analytics.
* **OneLake** → camada de armazenamento compartilhada do Fabric.
* **Power BI** → análise e visualização.
* **Azure Databricks** → Spark, engenharia de dados e Lakehouse.
* **Stream Analytics** → processamento de streaming em tempo real.
* **Data Explorer** → logs, telemetria e dados temporais.
* **Purview** → governança, catálogo e linhagem.
* **Microsoft Foundry** → desenvolvimento e implantação de soluções de IA.

---

> Material organizado a partir das minhas próprias anotações durante a preparação para a certificação **Microsoft Azure Data Fundamentals (DP-900)**.
