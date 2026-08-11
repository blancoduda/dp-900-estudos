# 01 — Explorando os principais conceitos de dados

> Anotações de estudo para a certificação **Microsoft Azure Data Fundamentals (DP-900)**.

Os dados são coleções de fatos, como números, descrições e observações, utilizados para registrar informações.

Normalmente, os dados representam **entidades** importantes para uma organização. Cada entidade possui atributos ou características que ajudam a descrevê-la.

**Exemplo:**

```text
Entidade: Cliente

Atributos:
- Nome
- Endereço
- Telefone
```

---

## 1. Tipos de dados

### Dados estruturados

Dados estruturados possuem um **esquema definido** e normalmente seguem a mesma estrutura para todas as instâncias.

Características:

* possuem esquema fixo;
* utilizam os mesmos campos ou propriedades;
* geralmente são representados em tabelas;
* linhas representam registros ou instâncias;
* colunas representam atributos;
* normalmente são armazenados em bancos de dados;
* tabelas podem se relacionar por meio de chaves.

**Exemplo:**

| id_cliente | nome | cidade       | email                                   |
| ---------- | ---- | ------------ | --------------------------------------- |
| 1          | Ana  | Porto Alegre | [ana@email.com](mailto:ana@email.com)   |
| 2          | João | São Paulo    | [joao@email.com](mailto:joao@email.com) |

---

### Dados semiestruturados

Dados semiestruturados possuem alguma organização, mas **não exigem que todas as entidades tenham exatamente os mesmos atributos**.

Um exemplo comum é o **JSON**.

Um cliente pode possuir telefone e e-mail, enquanto outro pode possuir apenas e-mail.

```json
{
  "firstName": "Joe",
  "lastName": "Jones",
  "contact": [
    {
      "type": "email",
      "address": "joe@example.com"
    }
  ]
}
```

Essa flexibilidade torna o formato adequado para situações em que os registros podem apresentar estruturas ligeiramente diferentes.

---

### Dados não estruturados

Não possuem uma estrutura ou esquema tabular específico.

Exemplos:

* documentos;
* imagens;
* áudios;
* vídeos;
* arquivos binários;
* dados vetoriais utilizados em aplicações de IA.

---

## 2. Armazenamento de dados

Existem duas categorias principais de armazenamento abordadas neste módulo:

1. **Armazenamento de arquivos**
2. **Banco de dados**

---

## 3. Armazenamento de arquivos

Arquivos podem ser armazenados localmente ou em sistemas centralizados.

Em ambientes corporativos, é comum utilizar armazenamento compartilhado ou em nuvem, permitindo armazenar grandes volumes de dados de maneira centralizada.

A escolha do formato depende de fatores como:

* tipo dos dados;
* aplicações que irão consumir os dados;
* necessidade de leitura humana;
* eficiência de armazenamento;
* eficiência de processamento.

---

## 4. Formatos de arquivos

### CSV e arquivos delimitados

Arquivos delimitados armazenam dados em texto utilizando caracteres específicos para separar os campos.

Os formatos mais conhecidos são:

**CSV — Comma-Separated Values**

```csv
FirstName,LastName,Email
Joe,Jones,joe@example.com
Samir,Nadoy,samir@example.com
```

**TSV — Tab-Separated Values**

Utiliza tabulação como separador entre os valores.

Arquivos delimitados são úteis quando dados estruturados precisam ser utilizados por diferentes aplicações em um formato simples e legível.

---

### JSON

**JSON — JavaScript Object Notation**

É um formato hierárquico bastante utilizado para representar dados estruturados e semiestruturados.

Características:

* objetos são delimitados por `{ }`;
* coleções são delimitadas por `[ ]`;
* atributos são representados por pares `nome: valor`;
* atributos podem conter outros objetos ou coleções.

Exemplo:

```json
{
  "customers": [
    {
      "firstName": "Joe",
      "lastName": "Jones",
      "contact": [
        {
          "type": "email",
          "address": "joe@example.com"
        }
      ]
    }
  ]
}
```

---

### XML

**XML — Extensible Markup Language**

Foi muito utilizado nos anos 1990 e 2000 e ainda pode ser encontrado principalmente em sistemas legados.

Utiliza tags para representar elementos e atributos.

```xml
<Customers>
    <Customer name="Joe" lastName="Jones">
        <ContactDetails>
            <Contact type="email" address="joe@example.com"/>
        </ContactDetails>
    </Customer>
</Customers>
```

---

### BLOB

**BLOB — Binary Large Object**

Utilizado para armazenar grandes objetos binários.

Exemplos:

* imagens;
* áudio;
* vídeos;
* documentos;
* arquivos específicos de aplicações.

O conteúdo normalmente precisa ser interpretado por uma aplicação apropriada.

---

## 5. Formatos otimizados para processamento

Alguns formatos são projetados para melhorar:

* compactação;
* armazenamento;
* indexação;
* velocidade de processamento.

### Apache Parquet

Formato de armazenamento **orientado a colunas**.

É amplamente utilizado em ambientes analíticos e data lakehouses.

Características:

* projeto Apache;
* armazenamento colunar;
* possui metadados;
* eficiente para consultas que utilizam apenas determinadas colunas;
* suporta estruturas de dados aninhadas;
* favorece compactação e processamento analítico.

**Resumo mental:**

```text
Parquet → colunar → analytics
```

---

### Apache Avro

Formato de armazenamento **orientado a linhas**.

Características:

* projeto Apache;
* estrutura dos dados descrita no cabeçalho;
* cabeçalho armazenado como JSON;
* registros armazenados em formato binário;
* boa compactação;
* reduz requisitos de armazenamento e transferência pela rede.

**Resumo mental:**

```text
Avro → linhas → serialização e transporte eficiente
```

---

### Delta Lake

Delta Lake é um formato de armazenamento baseado em **Parquet**, adicionando uma camada de controle transacional.

Adiciona recursos como:

* transações ACID;
* versionamento dos dados;
* atualizações confiáveis;
* log de transações.

```text
Delta Lake
   ↓
Parquet
+
Transaction Log
```

---

# 6. Bancos de dados

Um banco de dados é um sistema utilizado para armazenar, gerenciar e consultar registros de dados.

Podemos dividi-los principalmente em:

* bancos de dados relacionais;
* bancos de dados não relacionais.

---

## 7. Bancos de dados relacionais

São utilizados principalmente para dados estruturados.

Os dados são armazenados em **tabelas que representam entidades**.

Cada registro pode possuir uma **chave primária**, que identifica aquela instância de maneira única.

As chaves também permitem estabelecer relacionamentos entre tabelas.

Exemplo:

```text
CLIENTE
id_cliente (PK)
nome

PEDIDO
id_pedido (PK)
id_cliente (FK)
valor
```

O uso de relacionamentos ajuda na **normalização**, evitando duplicação desnecessária de informações.

Os bancos relacionais normalmente são manipulados utilizando **SQL — Structured Query Language**.

---

## 8. Bancos de dados não relacionais

Também chamados de **NoSQL**, não exigem a utilização de um modelo relacional tradicional.

Entre os principais tipos estão:

### Chave-valor

Cada registro possui:

```text
CHAVE → VALOR
```

A chave identifica de maneira exclusiva o valor armazenado.

---

### Documentos

Uma especialização do modelo chave-valor em que o valor geralmente é representado por um documento JSON.

```json
{
  "id": 1,
  "nome": "Ana",
  "cidade": "Porto Alegre"
}
```

---

### Família de colunas

Organizam informações em linhas e colunas, permitindo agrupar colunas relacionadas em **famílias de colunas**.

---

### Grafos

Representam entidades utilizando:

```text
Nós + Relações
```

São adequados para dados nos quais as relações entre entidades possuem grande importância.

---

# 9. Processamento transacional — OLTP

Um sistema transacional registra eventos ou transações específicas.

Exemplos:

* compra realizada;
* transferência bancária;
* cadastro de cliente;
* pedido efetuado.

Esse tipo de carga de trabalho é conhecido como:

**OLTP — Online Transaction Processing**

Os sistemas OLTP são otimizados para operações frequentes de leitura e escrita.

Normalmente envolvem operações:

```text
C → Create
R → Read
U → Update
D → Delete
```

Ou simplesmente:

**CRUD**

---

## Propriedades ACID

As transações precisam preservar a integridade dos dados.

### Atomicidade

Uma transação acontece completamente ou não acontece.

```text
100% sucesso
     OU
100% rollback
```

### Consistência

Uma transação deve levar o banco de um estado válido para outro estado válido.

### Isolamento

Transações executadas simultaneamente não devem interferir umas nas outras.

### Durabilidade

Depois que uma transação é confirmada, a alteração deve permanecer armazenada.

---

## OLTP em uma frase

> Muitos registros pequenos sendo criados, atualizados e consultados constantemente.

---

# 10. Processamento analítico

Sistemas analíticos normalmente trabalham com grandes volumes de **dados históricos** e métricas de negócio.

Eles são utilizados para:

* análises;
* relatórios;
* dashboards;
* identificação de tendências;
* apoio à tomada de decisão.

Diferentemente dos sistemas transacionais, esses ambientes geralmente possuem uma característica **read-mostly**, ou seja, são muito mais consultados do que alterados.

---

# 11. ETL e ELT

### ETL

```text
Extract
   ↓
Transform
   ↓
Load
```

Os dados são extraídos, transformados e depois carregados no destino.

### ELT

```text
Extract
   ↓
Load
   ↓
Transform
```

Os dados são carregados inicialmente e as transformações são realizadas posteriormente.

Esse padrão é comum em arquiteturas modernas de dados.

---

# 12. Data Lake

Um **Data Lake** armazena grandes volumes de dados, geralmente baseados em arquivos.

Pode armazenar diferentes tipos de dados e formatos.

No Azure, um serviço utilizado para essa finalidade é:

**Azure Data Lake Storage Gen2**

```text
Data Lake
↓
Grande volume
↓
Arquivos
↓
Dados brutos
```

---

# 13. Data Warehouse

Um **Data Warehouse** armazena dados estruturados utilizando tabelas relacionais.

É otimizado principalmente para operações de leitura e consultas analíticas.

Utilizado para:

* BI;
* relatórios;
* dashboards;
* consultas analíticas.

No ecossistema Azure/Microsoft, exemplos incluem:

* Azure Synapse Analytics;
* Microsoft Fabric Warehouse.

---

# 14. Data Lakehouse

O **Data Lakehouse** combina características de:

```text
Data Lake
   +
Data Warehouse
```

Busca oferecer:

* armazenamento flexível;
* grande escalabilidade;
* estrutura tabular;
* semântica de consulta relacional.

Exemplos:

* Microsoft Fabric Lakehouse;
* Azure Databricks Lakehouse.

---

## Lake x Warehouse x Lakehouse

| Característica       | Data Lake | Data Warehouse | Lakehouse |
| -------------------- | --------- | -------------- | --------- |
| Dados brutos         | ✅         | ❌              | ✅         |
| Arquivos             | ✅         | ❌              | ✅         |
| Estrutura relacional | Limitada  | ✅              | ✅         |
| Analytics            | ✅         | ✅              | ✅         |
| Flexibilidade        | Alta      | Menor          | Alta      |
| Consultas tabulares  | Possível  | ✅              | ✅         |

---

# 15. OLAP e modelos semânticos

**OLAP — Online Analytical Processing**

É voltado para cargas de trabalho analíticas.

Os dados podem ser pré-agregados por diferentes dimensões.

Exemplo:

```text
Receita
├── Ano
│   ├── Trimestre
│   │   └── Mês
├── Produto
└── Cliente
```

Isso permite operações como **drill-down** e **drill-up**, navegando entre diferentes níveis de detalhe.

Atualmente, é comum trabalhar com **modelos semânticos**, como os utilizados pelo Power BI.

---

# 16. Plataformas modernas de análise

## Microsoft Fabric

Plataforma de análise **SaaS** unificada que reúne diferentes componentes de uma solução de dados.

Pode incluir recursos relacionados a:

* armazenamento;
* engenharia de dados;
* data warehouse;
* análise;
* relatórios.

Tudo dentro de um ambiente integrado.

---

## Azure Databricks

Plataforma voltada principalmente para:

* engenharia de dados;
* processamento em grande escala;
* analytics;
* ciência de dados.

Utiliza tecnologias como **Delta Lake** para armazenamento.

---

## Microsoft Purview

Voltado para:

* governança de dados;
* segurança;
* conformidade;
* descoberta;
* classificação;
* gerenciamento dos dados.

**Resumo:**

```text
Fabric      → plataforma analítica integrada

Databricks  → engenharia e processamento de dados em escala

Purview     → governança e segurança dos dados
```

---

# 17. Arquitetura Medalhão

A arquitetura medalhão divide o processamento dos dados em camadas.

## 🥉 Bronze

Dados brutos provenientes dos sistemas de origem.

```text
Origem → Bronze
```

Pouca ou nenhuma transformação.

Serve também para preservar os registros originais para possível reprocessamento.

---

## 🥈 Silver

Dados tratados e padronizados.

Exemplos de operações:

* remoção de duplicidades;
* correção de tipos;
* limpeza;
* padronização.

```text
Bronze
  ↓
Limpeza
  ↓
Silver
```

---

## 🥇 Gold

Dados preparados para consumo de negócio.

Podem conter:

* agregações;
* indicadores;
* métricas;
* estruturas específicas para relatórios.

```text
Bronze
   ↓
Silver
   ↓
Gold
   ↓
BI / Analytics
```

---

# 🧠 Resumo para revisão

```text
DADOS
│
├── Estruturados
│   └── tabelas / esquema fixo
│
├── Semiestruturados
│   └── JSON
│
└── Não estruturados
    └── imagem / áudio / vídeo / documentos


ARQUIVOS
│
├── CSV
├── JSON
├── XML
├── BLOB
├── Parquet
├── Avro
└── Delta Lake


BANCO DE DADOS
│
├── Relacional
│   └── SQL
│
└── NoSQL
    ├── Chave-valor
    ├── Documento
    ├── Família de colunas
    └── Grafo


WORKLOADS
│
├── OLTP
│   ├── transações
│   ├── CRUD
│   └── ACID
│
└── Analytics
    ├── ETL / ELT
    ├── Data Lake
    ├── Data Warehouse
    ├── Lakehouse
    └── OLAP


AZURE / MICROSOFT
│
├── Azure Data Lake Storage Gen2
├── Azure Synapse Analytics
├── Microsoft Fabric
├── Azure Databricks
└── Microsoft Purview


ARQUITETURA MEDALHÃO
│
├── Bronze → bruto
├── Silver → tratado
└── Gold → negócio
```

---

## ✅ Pontos que eu levaria para a prova

* **OLTP** → transações, CRUD e muitas operações de leitura/escrita.
* **ACID** → Atomicidade, Consistência, Isolamento e Durabilidade.
* **OLAP** → análise e agregação de dados.
* **Parquet** → armazenamento colunar.
* **Avro** → armazenamento orientado a linhas.
* **Delta Lake** → Parquet + log de transações.
* **Data Lake** → grande volume de arquivos e dados brutos.
* **Data Warehouse** → dados estruturados e consultas analíticas.
* **Lakehouse** → combina características de Lake e Warehouse.
* **Bronze** → dados brutos.
* **Silver** → dados limpos e padronizados.
* **Gold** → dados preparados para consumo de negócio.
* **Fabric** → plataforma analítica integrada.
* **Databricks** → engenharia e análise de dados em escala.
* **Purview** → governança, segurança e conformidade de dados.

---

> Material baseado nas minhas anotações durante a preparação para a certificação **Microsoft Azure Data Fundamentals (DP-900)**.
