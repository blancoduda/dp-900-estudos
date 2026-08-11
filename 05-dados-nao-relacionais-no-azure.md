# 05 — Dados não relacionais no Azure

> Anotações de estudo para a certificação **Microsoft Azure Data Fundamentals (DP-900)**.

O Azure oferece diferentes opções para armazenar e processar **dados não relacionais**, desde arquivos e objetos binários até estruturas NoSQL distribuídas globalmente.

Neste módulo, os principais serviços estudados são:

* Azure Blob Storage;
* Azure Data Lake Storage Gen2;
* Microsoft OneLake;
* Azure Files;
* Azure Table Storage;
* Azure Cosmos DB.

---

# 1. Azure Blob Storage

O **Azure Blob Storage** é um serviço para armazenar grandes volumes de dados não estruturados na nuvem.

Blob significa:

**Binary Large Object**

É adequado para armazenar arquivos como:

* imagens;
* vídeos;
* documentos;
* backups;
* arquivos binários;
* conjuntos de dados.

Os blobs são armazenados dentro de **contêineres** em uma conta de armazenamento do Azure.

```text
Azure Storage Account
        ↓
    Container
        ↓
      Blobs
```

---

# 2. Contêineres

Um **container** é utilizado para agrupar blobs relacionados.

Exemplo:

```text
Storage Account
│
├── imagens
│   ├── produto-01.jpg
│   └── produto-02.jpg
│
├── videos
│   └── treinamento.mp4
│
└── documentos
    └── contrato.pdf
```

Também é possível controlar permissões de acesso no nível do contêiner.

Nas anotações, o **Microsoft Entra ID** é apresentado como método recomendado de autenticação, permitindo utilizar o Azure RBAC para controlar permissões.

---

# 3. Tipos de Blob

O Azure oferece diferentes tipos de blobs.

```text
Blob Storage
│
├── Block Blob
├── Page Blob
└── Append Blob
```

---

## Block Blob

O **Block Blob** armazena dados em blocos.

É adequado principalmente para objetos grandes que não são modificados constantemente.

Exemplos:

* imagens;
* vídeos;
* documentos;
* backups;
* arquivos de dados.

```text
Arquivo
│
├── Bloco 1
├── Bloco 2
├── Bloco 3
└── Bloco 4
```

---

## Page Blob

O **Page Blob** é organizado em páginas de tamanho fixo.

É otimizado para operações de **leitura e gravação aleatória**.

Um uso importante é o armazenamento de discos virtuais utilizados por máquinas virtuais do Azure.

```text
Page Blob
    ↓
Virtual Disk
    ↓
Azure VM
```

---

## Append Blob

O **Append Blob** é otimizado para operações em que novos dados são continuamente adicionados ao final do arquivo.

```text
Dados existentes
      +
Novo bloco
      +
Novo bloco
      +
Novo bloco
```

É adequado para cenários como registros sequenciais e logs.

---

# 4. Camadas de acesso do Blob Storage

O Azure Blob Storage possui diferentes **access tiers**, permitindo equilibrar custo de armazenamento e frequência de acesso.

```text
Mais acesso
    ↑

Hot
Cool
Cold
Archive

    ↓
Menos acesso
```

---

## Hot

A camada **Hot** é adequada para dados acessados frequentemente.

Características:

* maior custo de armazenamento;
* menor custo de acesso;
* acesso rápido.

```text
Hot
→ uso frequente
```

---

## Cool

A camada **Cool** é indicada para dados acessados com menor frequência.

Características:

* armazenamento mais barato que Hot;
* acesso mais caro;
* indicada para dados utilizados ocasionalmente.

Nas anotações, os dados devem permanecer nessa camada por pelo menos **30 dias** para evitar penalidades de exclusão antecipada.

---

## Cold

A camada **Cold** é indicada para dados raramente acessados, mas que ainda precisam estar disponíveis com relativa rapidez.

Exemplos:

* backups;
* recuperação de desastre;
* conjuntos de dados pouco consultados.

Nas anotações, o período mínimo apresentado é de **90 dias**.

---

## Archive

A camada **Archive** possui o menor custo de armazenamento.

É utilizada para dados históricos acessados raramente.

Porém, os dados ficam praticamente offline e precisam passar por um processo de **rehydration** antes de serem utilizados.

Nas anotações:

```text
Archive
→ armazenamento barato
→ maior latência
→ dados offline
→ rehydration para acessar
```

O período mínimo apresentado é de **180 dias**, e a recuperação pode levar várias horas.

---

# 5. Lifecycle Management

É possível utilizar políticas de **gerenciamento de ciclo de vida** para mover automaticamente dados entre as camadas.

Exemplo:

```text
Arquivo criado
    ↓
Hot
    ↓
Cool
    ↓
Cold
    ↓
Archive
    ↓
Exclusão
```

A movimentação pode acontecer conforme:

* idade do arquivo;
* data da última modificação;
* frequência de utilização.

Também é possível configurar exclusão automática de blobs antigos.

---

# 6. Redundância de armazenamento

O Azure permite manter cópias dos dados para aumentar disponibilidade e resiliência.

Os principais modelos estudados foram:

```text
LRS
ZRS
GRS
GZRS
```

---

## LRS — Locally Redundant Storage

Mantém múltiplas cópias dos dados dentro de um único datacenter.

```text
Região
└── Datacenter
    ├── Cópia
    ├── Cópia
    └── Cópia
```

---

## ZRS — Zone-Redundant Storage

Distribui cópias entre diferentes **Availability Zones** da mesma região.

```text
Região
│
├── Zona 1
├── Zona 2
└── Zona 3
```

Isso ajuda a manter os dados disponíveis mesmo se uma zona falhar.

---

## GRS — Geo-Redundant Storage

Replica os dados também para uma **região secundária**.

```text
Região principal
       ↓
Replicação
       ↓
Região secundária
```

É útil para proteção contra falhas regionais.

---

## GZRS — Geo-Zone-Redundant Storage

Combina:

```text
ZRS
+
replicação geográfica
```

Ou seja, utiliza zonas de disponibilidade na região principal e replica dados para outra região.

Também existem opções de leitura da região secundária:

```text
RA-GRS
RA-GZRS
```

---

# 7. Azure Data Lake Storage Gen2

O **Azure Data Lake Storage Gen2 — ADLS Gen2** é uma solução de Data Lake integrada ao Azure Storage.

Ele combina:

* escalabilidade do Blob Storage;
* controle de custos;
* gerenciamento de ciclo de vida;
* estrutura hierárquica de arquivos.

```text
Azure Blob Storage
       +
Hierarchical Namespace
       ↓
Azure Data Lake Storage Gen2
```

---

# 8. Hierarchical Namespace

Para utilizar os recursos de Data Lake Storage Gen2, é necessário habilitar o **Hierarchical Namespace**.

Ele permite organizar os dados de forma semelhante a um sistema tradicional de arquivos:

```text
Data Lake
│
├── bronze/
│   └── vendas/
│
├── silver/
│   └── vendas/
│
└── gold/
    └── vendas/
```

Isso difere das pastas virtuais do Blob Storage tradicional.

Nas anotações, a ativação do namespace hierárquico é apresentada como uma alteração **unidirecional**.

---

# 9. ADLS Gen2 e Analytics

O ADLS Gen2 pode ser utilizado por ferramentas analíticas para processar grandes volumes de dados.

Um exemplo citado é:

```text
Azure Data Lake Storage Gen2
            ↓
      Azure Databricks
            ↓
    Processamento
            ↓
        Analytics
```

---

# 10. Microsoft OneLake

O **OneLake** é o Data Lake unificado do Microsoft Fabric.

Ele é provisionado automaticamente para tenants do Fabric e é baseado no **Azure Data Lake Storage Gen2**.

```text
Microsoft Fabric
       ↓
    OneLake
       ↓
Dados da organização
```

---

# 11. Conceito de OneLake

O objetivo do OneLake é oferecer um único Data Lake lógico para toda a organização.

```text
Empresa
│
├── Financeiro
├── Marketing
├── Tecnologia
└── Operações
        ↓
      OneLake
```

Em vez de cada área manter seu próprio Data Lake isolado, diferentes workspaces podem utilizar a mesma camada central de armazenamento.

---

## Características do OneLake

Entre os principais conceitos estão:

* Data Lake único para a organização;
* suporte a dados estruturados e não estruturados;
* workspaces independentes;
* colaboração;
* governança;
* compatibilidade com ADLS Gen2;
* armazenamento baseado em formatos abertos.

Nas anotações, o OneLake utiliza **Delta Parquet** como formato para dados analíticos.

---

# 12. Azure Files

O **Azure Files** oferece compartilhamentos de arquivos baseados em nuvem.

Ele funciona de maneira semelhante a compartilhamentos de rede tradicionais utilizados em empresas.

```text
Usuário A
     \
Usuário B → Azure Files
     /
Usuário C
```

Isso permite substituir ou complementar servidores locais de arquivos.

---

# 13. Protocolos do Azure Files

O Azure Files oferece suporte a dois protocolos principais:

```text
Azure Files
│
├── SMB
└── NFS
```

---

## SMB — Server Message Block

O protocolo **SMB** é amplamente utilizado para compartilhamento de arquivos.

Pode ser utilizado em sistemas como:

* Windows;
* Linux;
* macOS.

---

## NFS — Network File System

O protocolo **NFS** é utilizado principalmente em ambientes Linux.

Nas anotações, os compartilhamentos NFS do Azure não são apresentados como compatíveis com Windows ou macOS.

---

# 14. Azure Table Storage

O **Azure Table Storage** é um serviço de armazenamento **NoSQL chave-valor**.

Apesar do nome "Table", ele não funciona como uma tabela de banco de dados relacional.

```text
Azure Table
│
├── PartitionKey
├── RowKey
└── propriedades
```

---

# 15. Dados semiestruturados no Table Storage

As linhas não precisam possuir exatamente as mesmas colunas.

Exemplo:

```text
Cliente 1
├── Nome
├── Email
└── Telefone

Cliente 2
├── Nome
├── Email
├── Telefone
└── Endereço
```

Isso é diferente de uma tabela relacional, onde normalmente existe um esquema fixo.

O Azure Table Storage também não utiliza conceitos relacionais como:

* foreign keys;
* joins;
* stored procedures;
* views.

---

# 16. PartitionKey e RowKey

Cada linha possui uma chave composta por:

```text
PartitionKey
     +
RowKey
```

A combinação identifica uma linha.

---

## PartitionKey

A **PartitionKey** define em qual partição os dados serão armazenados.

Exemplo:

```text
PartitionKey = "RS"

├── Cliente A
├── Cliente B
└── Cliente C
```

Uma boa estratégia de particionamento ajuda a melhorar:

* escalabilidade;
* desempenho;
* velocidade das consultas.

---

## RowKey

A **RowKey** identifica exclusivamente uma linha dentro da partição.

```text
PartitionKey = RS

RowKey = 001
RowKey = 002
RowKey = 003
```

---

# 17. Azure Cosmos DB

O **Azure Cosmos DB** é um banco de dados **NoSQL totalmente gerenciado** oferecido como PaaS no Azure.

A Microsoft gerencia a infraestrutura subjacente, incluindo:

* servidores;
* atualizações;
* patches;
* backups.

---

# 18. Schema independence

O Cosmos DB é **independente de esquema**.

Isso significa que itens dentro do mesmo contêiner não precisam ter exatamente a mesma estrutura.

```json
{
  "id": "1",
  "nome": "Ana"
}
```

Outro item pode possuir:

```json
{
  "id": "2",
  "nome": "João",
  "cidade": "Porto Alegre",
  "telefone": "99999-9999"
}
```

Essa flexibilidade torna o Cosmos DB adequado para aplicações em que a estrutura dos dados pode variar com o tempo.

---

# 19. Hierarquia do Cosmos DB

O Cosmos DB organiza seus recursos em quatro níveis.

```text
Account
   ↓
Database
   ↓
Container
   ↓
Item
```

---

## Account

É o recurso principal criado no Azure.

Pode conter diferentes bancos de dados.

---

## Database

É um agrupamento lógico de containers relacionados.

---

## Container

É a principal unidade de armazenamento e escalabilidade.

Nele podem ser configurados recursos como:

* partition key;
* throughput;
* política de indexação;
* TTL.

---

## Item

É o registro individual armazenado.

Dependendo da API utilizada, pode ser chamado de:

* documento;
* linha;
* nó;
* aresta.

---

# 20. Partition Key no Cosmos DB

O Cosmos DB utiliza **partition keys** para distribuir os dados.

```text
Cosmos DB
│
├── Partition A
├── Partition B
├── Partition C
└── Partition D
```

Uma boa chave de partição deve permitir distribuir os dados de maneira equilibrada.

---

# 21. Indexação automática

Por padrão, o Cosmos DB cria e mantém índices automaticamente para as propriedades dos itens.

Isso reduz a necessidade de administrar índices manualmente.

```text
Novo item
   ↓
Cosmos DB
   ↓
Indexação automática
```

---

# 22. Distribuição global

O Cosmos DB foi desenvolvido para cenários distribuídos globalmente.

É possível adicionar diferentes regiões do Azure a uma conta.

```text
Cosmos DB
│
├── Brazil South
├── East US
└── West Europe
```

Os dados podem ser replicados entre essas regiões.

O objetivo é permitir:

* baixa latência;
* alta disponibilidade;
* acesso aos dados próximo dos usuários.

---

# 23. Níveis de consistência

Quando existem réplicas em diferentes regiões, é necessário definir como essas réplicas se mantêm consistentes.

O Cosmos DB oferece cinco níveis.

| Nível             | Característica                         |
| ----------------- | -------------------------------------- |
| Strong            | Sempre retorna a gravação mais recente |
| Bounded Staleness | Permite atraso controlado              |
| Session           | Consistência dentro de uma sessão      |
| Consistent Prefix | Mantém a ordem das gravações           |
| Eventual          | Réplicas convergem ao longo do tempo   |

---

## Forma rápida de lembrar

```text
Mais consistência
      ↑

Strong
Bounded Staleness
Session
Consistent Prefix
Eventual

      ↓
Mais flexibilidade
```

---

# 24. Request Units — RU/s

O Cosmos DB utiliza **Request Units — RU/s** para medir capacidade.

Operações como:

* leitura;
* gravação;
* consulta;
* exclusão;

consomem unidades de solicitação.

```text
Operação
   ↓
Consome RU
   ↓
Capacidade / custo
```

---

# 25. Modelos de throughput

Nas anotações aparecem três formas principais:

### Dedicated

Capacidade reservada para um único container.

### Shared

Throughput provisionado no nível do database e compartilhado entre containers.

### Serverless

Não existe capacidade provisionada previamente.

O pagamento ocorre conforme as solicitações.

---

# 26. Autoscale

Também é possível definir um limite máximo de RU/s e permitir que o Cosmos DB ajuste automaticamente a capacidade conforme a demanda.

```text
Baixa demanda
   ↓
menos RU/s

Alta demanda
   ↓
mais RU/s
```

---

# 27. Casos de uso do Cosmos DB

O Cosmos DB é adequado para aplicações que precisam de:

* esquema flexível;
* distribuição global;
* baixa latência;
* grande escalabilidade.

Exemplos citados nas anotações:

* IoT;
* telemetria;
* jogos;
* varejo;
* e-commerce;
* aplicações web;
* aplicações mobile.

Para cenários dependentes de joins complexos entre múltiplas tabelas, um banco relacional pode ser mais adequado.

---

# 28. APIs do Azure Cosmos DB

Uma característica importante do Cosmos DB é o suporte a diferentes APIs.

```text
Cosmos DB
│
├── NoSQL
├── MongoDB
├── Table
├── Apache Cassandra
└── Apache Gremlin
```

A escolha da API determina:

* formato dos dados;
* linguagem de consulta;
* bibliotecas utilizadas pela aplicação.

---

# 29. Cosmos DB for NoSQL

É a API **nativa do Cosmos DB**.

Armazena dados como documentos JSON.

```json
{
  "id": "123",
  "produto": "Notebook",
  "preco": 3500
}
```

As consultas utilizam uma sintaxe semelhante a SQL.

Nas anotações, essa API é indicada como recomendada para novos aplicativos.

---

# 30. Cosmos DB for MongoDB

Permite que aplicações baseadas em **MongoDB** utilizem o Cosmos DB com poucas alterações.

Características estudadas:

* compatibilidade com drivers MongoDB;
* bibliotecas já existentes;
* dados em BSON;
* consultas utilizando MQL.

```text
Aplicação MongoDB
       ↓
Cosmos DB for MongoDB
```

---

# 31. Cosmos DB for Table

Utiliza um modelo de armazenamento chave-valor semelhante ao Azure Table Storage.

```text
PartitionKey + RowKey
```

É adequado para aplicações que já utilizam Azure Table Storage.

Entre as vantagens apresentadas em comparação ao Table Storage estão:

* maior escalabilidade;
* distribuição global;
* indexação secundária automática;
* autoscale.

Nas anotações, o Cosmos DB for Table aparece como a opção recomendada para novas cargas de trabalho desse tipo.

---

# 32. Cosmos DB for Apache Cassandra

Essa API oferece compatibilidade com **Apache Cassandra**.

O Cassandra utiliza um modelo de:

```text
Column Family
```

Nesse modelo, diferentes linhas não precisam possuir exatamente as mesmas colunas.

As consultas utilizam:

```text
CQL
→ Cassandra Query Language
```

Sua sintaxe é semelhante a SQL.

---

# 33. Cosmos DB for Apache Gremlin

Essa API é voltada para **bancos de dados em grafo**.

Os dados são representados utilizando:

```text
Vertices
   +
Edges
```

Ou:

```text
Nós
 +
Relações
```

---

## Exemplos de uso

* redes sociais;
* sistemas de recomendação;
* detecção de fraude;
* hierarquias organizacionais.

A linguagem utilizada é **Gremlin**.

---

# 34. Comparação das APIs do Cosmos DB

| API                     | Modelo principal        |
| ----------------------- | ----------------------- |
| Cosmos DB for NoSQL     | Documentos JSON         |
| Cosmos DB for MongoDB   | Documentos MongoDB/BSON |
| Cosmos DB for Table     | Chave-valor             |
| Cosmos DB for Cassandra | Família de colunas      |
| Cosmos DB for Gremlin   | Grafos                  |

---

# 35. Comparação Azure Table Storage x Cosmos DB for Table

| Característica      | Azure Table Storage | Cosmos DB for Table       |
| ------------------- | ------------------- | ------------------------- |
| Modelo              | Chave-valor         | Chave-valor               |
| PartitionKey        | Sim                 | Sim                       |
| RowKey              | Sim                 | Sim                       |
| NoSQL               | Sim                 | Sim                       |
| Distribuição global | Mais limitada       | Sim                       |
| Escalabilidade      | Alta                | Maior                     |
| Indexação avançada  | Mais limitada       | Automática                |
| Novas cargas        | Disponível          | Recomendado nas anotações |

---

# 36. Comparação geral dos serviços

| Necessidade                         | Serviço                      |
| ----------------------------------- | ---------------------------- |
| Objetos e arquivos não estruturados | Azure Blob Storage           |
| Data Lake                           | Azure Data Lake Storage Gen2 |
| Data Lake do Microsoft Fabric       | OneLake                      |
| Compartilhamento de arquivos        | Azure Files                  |
| Chave-valor simples                 | Azure Table Storage          |
| NoSQL distribuído globalmente       | Azure Cosmos DB              |
| Documentos JSON                     | Cosmos DB for NoSQL          |
| MongoDB                             | Cosmos DB for MongoDB        |
| Família de colunas                  | Cosmos DB for Cassandra      |
| Grafos                              | Cosmos DB for Gremlin        |

---

# 🧠 Mapa mental

```text
DADOS NÃO RELACIONAIS NO AZURE
│
├── Azure Storage
│   │
│   ├── Blob Storage
│   │   ├── Block Blob
│   │   ├── Page Blob
│   │   └── Append Blob
│   │
│   ├── Access Tiers
│   │   ├── Hot
│   │   ├── Cool
│   │   ├── Cold
│   │   └── Archive
│   │
│   ├── ADLS Gen2
│   │   └── Hierarchical Namespace
│   │
│   ├── Azure Files
│   │   ├── SMB
│   │   └── NFS
│   │
│   └── Table Storage
│       ├── PartitionKey
│       └── RowKey
│
├── Microsoft Fabric
│   └── OneLake
│
└── Azure Cosmos DB
    │
    ├── NoSQL
    ├── MongoDB
    ├── Table
    ├── Cassandra
    └── Gremlin
```

---

# ✅ Pontos que eu levaria para a prova

* **Blob Storage** → armazenamento de objetos e dados não estruturados.
* **Block Blob** → arquivos e objetos grandes.
* **Page Blob** → leitura/gravação aleatória e discos de VMs.
* **Append Blob** → dados adicionados sequencialmente.
* **Hot** → acesso frequente.
* **Cool** → acesso menos frequente.
* **Cold** → acesso raro.
* **Archive** → menor custo e maior latência.
* **Lifecycle Management** → movimenta dados automaticamente entre tiers.
* **LRS** → redundância local.
* **ZRS** → redundância entre zonas.
* **GRS** → redundância geográfica.
* **GZRS** → zonas + região secundária.
* **ADLS Gen2** → Blob Storage + namespace hierárquico.
* **OneLake** → Data Lake unificado do Microsoft Fabric.
* **Azure Files** → compartilhamentos de arquivos.
* **SMB** → compartilhamento de arquivos amplamente suportado.
* **NFS** → utilizado principalmente em Linux.
* **Azure Table Storage** → NoSQL chave-valor.
* **PartitionKey + RowKey** → identificam registros no Table Storage.
* **Cosmos DB** → banco NoSQL PaaS totalmente gerenciado.
* **Cosmos DB** → esquema flexível e distribuição global.
* **RU/s** → unidade utilizada para medir capacidade do Cosmos DB.
* **Strong, Bounded Staleness, Session, Consistent Prefix e Eventual** → níveis de consistência.
* **Cosmos DB for NoSQL** → documentos JSON e API nativa.
* **MongoDB** → compatibilidade com aplicações MongoDB.
* **Table** → chave-valor.
* **Cassandra** → família de colunas.
* **Gremlin** → grafos.

---

> Material organizado a partir das minhas próprias anotações durante a preparação para a certificação **Microsoft Azure Data Fundamentals (DP-900)**.

