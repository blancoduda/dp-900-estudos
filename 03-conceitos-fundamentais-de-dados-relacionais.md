# 03 — Conceitos fundamentais de dados relacionais

> Anotações de estudo para a certificação **Microsoft Azure Data Fundamentals (DP-900)**.

Os bancos de dados relacionais fornecem um padrão para **representar, organizar e consultar dados estruturados**.

Uma das principais características desse modelo é o uso de **tabelas**, que oferecem uma maneira estruturada e consistente de armazenar informações relacionadas.

---

# 1. Modelo relacional

Um banco de dados relacional é adequado quando os dados possuem relações entre si e precisam seguir uma estrutura consistente.

Os dados são organizados em:

```text
Banco de dados
    ↓
Tabelas
    ↓
Linhas
    ↓
Colunas
```

### Entidade

Uma **entidade** representa algo sobre o qual queremos armazenar informações.

Exemplos:

```text
Cliente
Produto
Pedido
Funcionário
```

Uma tabela normalmente representa uma entidade.

### Linha

Cada linha representa uma **instância da entidade**.

Exemplo:

| id_cliente | nome | cidade       |
| ---------- | ---- | ------------ |
| 1          | Ana  | Porto Alegre |
| 2          | João | São Paulo    |

Nesse caso:

```text
Tabela → Cliente

Linha 1 → Ana
Linha 2 → João
```

### Coluna

Cada coluna representa um **atributo** da entidade.

```text
Cliente
│
├── id_cliente
├── nome
└── cidade
```

Cada coluna também possui um **tipo de dado específico**.

Exemplos:

```text
INT      → números inteiros
DECIMAL  → números decimais
VARCHAR  → textos
```

Os tipos disponíveis podem variar entre os diferentes sistemas de gerenciamento de banco de dados.

---

# 2. Normalização

A **normalização** é um processo utilizado no design de bancos relacionais para:

* reduzir duplicação de dados;
* melhorar a organização;
* manter a integridade das informações.

Uma forma simplificada de entender a normalização é seguir quatro princípios:

1. separar cada **entidade** em sua própria tabela;
2. separar cada **atributo** em sua própria coluna;
3. identificar cada registro utilizando uma **chave primária**;
4. relacionar tabelas utilizando **chaves estrangeiras**.

---

## Exemplo sem normalização

Imagine uma tabela:

| pedido | cliente | email_cliente                         | produto  | valor |
| ------ | ------- | ------------------------------------- | -------- | ----- |
| 1001   | Ana     | [ana@email.com](mailto:ana@email.com) | Notebook | 3500  |
| 1002   | Ana     | [ana@email.com](mailto:ana@email.com) | Mouse    | 150   |

Os dados da cliente Ana estão repetidos.

---

## Exemplo normalizado

Podemos separar as entidades.

### Cliente

| id_cliente | nome | email                                 |
| ---------- | ---- | ------------------------------------- |
| 1          | Ana  | [ana@email.com](mailto:ana@email.com) |

### Pedido

| id_pedido | id_cliente | produto  | valor |
| --------- | ---------- | -------- | ----- |
| 1001      | 1          | Notebook | 3500  |
| 1002      | 1          | Mouse    | 150   |

Agora:

```text
CLIENTE
id_cliente (PK)
      │
      └─────────────┐
                    ↓
PEDIDO
id_cliente (FK)
```

Dessa forma, os dados da cliente não precisam ser repetidos em cada pedido.

---

# 3. Chave primária

A **Primary Key — PK** identifica exclusivamente cada linha de uma tabela.

Exemplo:

```text
CLIENTE

id_cliente → Primary Key
nome
email
```

| id_cliente | nome |
| ---------- | ---- |
| 1          | Ana  |
| 2          | João |

O valor de `id_cliente` identifica cada cliente de maneira única.

---

# 4. Chave estrangeira

A **Foreign Key — FK** é utilizada para criar relações entre tabelas.

Exemplo:

```text
CLIENTE
id_cliente (PK)
     │
     │
     ↓
PEDIDO
id_cliente (FK)
```

A chave estrangeira armazena a chave primária da entidade relacionada.

---

# 5. Chave composta

Em alguns casos, uma chave pode ser formada pela combinação de **mais de uma coluna**.

Exemplo:

```text
ITEM_PEDIDO

id_pedido
id_produto
```

Podemos utilizar:

```text
id_pedido + id_produto
```

como uma chave composta para identificar exclusivamente um item.

---

# 6. SQL

**SQL — Structured Query Language** é a linguagem padrão utilizada para comunicação com bancos de dados relacionais.

Ela permite:

* consultar dados;
* inserir registros;
* alterar registros;
* excluir registros;
* criar objetos;
* modificar estruturas;
* administrar permissões.

Entre os sistemas que utilizam SQL estão:

* Microsoft SQL Server;
* Azure SQL Database;
* Azure SQL Managed Instance;
* SQL Server em Azure VMs;
* MySQL;
* PostgreSQL;
* Oracle.

---

# 7. Dialetos SQL

Embora exista um padrão SQL, diferentes bancos podem adicionar suas próprias extensões.

## Transact-SQL — T-SQL

Utilizado pelo ecossistema Microsoft:

```text
Microsoft SQL Server
Azure SQL Database
Azure SQL Managed Instance
SQL Server em Azure VM
```

---

## pgSQL

Dialeto e extensões utilizadas pelo PostgreSQL.

---

## PL/SQL

Utilizado pelo Oracle.

```text
SQL padrão
│
├── T-SQL → Microsoft
├── pgSQL → PostgreSQL
└── PL/SQL → Oracle
```

---

# 8. Categorias de instruções SQL

As instruções SQL podem ser divididas de acordo com sua finalidade.

Neste módulo aparecem três grupos principais:

```text
SQL
│
├── DDL
├── DCL
└── DML
```

---

# 9. DDL — Data Definition Language

A **Linguagem de Definição de Dados** é utilizada para criar e modificar a estrutura do banco de dados.

| Comando  | Função             |
| -------- | ------------------ |
| `CREATE` | Criar um objeto    |
| `ALTER`  | Alterar um objeto  |
| `DROP`   | Remover um objeto  |
| `RENAME` | Renomear um objeto |

### CREATE

Cria um objeto.

```sql
CREATE TABLE Clientes (
    id INT,
    nome VARCHAR(100)
);
```

---

### ALTER

Modifica a estrutura de um objeto existente.

```sql
ALTER TABLE Clientes
ADD email VARCHAR(150);
```

---

### DROP

Remove um objeto.

```sql
DROP TABLE Clientes;
```

---

## Forma rápida de lembrar

```text
DDL
→ estrutura

CREATE
ALTER
DROP
RENAME
```

---

# 10. DCL — Data Control Language

A **Linguagem de Controle de Dados** está relacionada ao controle de permissões e acesso aos objetos do banco.

| Comando  | Função                          |
| -------- | ------------------------------- |
| `GRANT`  | Conceder uma permissão          |
| `DENY`   | Negar uma permissão             |
| `REVOKE` | Remover uma permissão concedida |

### Exemplo conceitual

```text
Usuário
   ↓
GRANT
   ↓
Permissão concedida
```

```text
Usuário
   ↓
REVOKE
   ↓
Permissão removida
```

---

## Forma rápida de lembrar

```text
DCL
→ controle de acesso

GRANT
DENY
REVOKE
```

---

# 11. DML — Data Manipulation Language

A **Linguagem de Manipulação de Dados** trabalha diretamente com os registros armazenados nas tabelas.

Os principais comandos são:

| Comando  | Função              |
| -------- | ------------------- |
| `SELECT` | Ler dados           |
| `INSERT` | Inserir registros   |
| `UPDATE` | Atualizar registros |
| `DELETE` | Excluir registros   |

---

# 12. SELECT

Utilizado para consultar dados.

```sql
SELECT nome, cidade
FROM Clientes;
```

Também podemos selecionar todas as colunas:

```sql
SELECT *
FROM Clientes;
```

---

# 13. WHERE

A cláusula `WHERE` permite aplicar um filtro.

```sql
SELECT *
FROM Clientes
WHERE cidade = 'Porto Alegre';
```

Ela também é muito importante em comandos de alteração e exclusão.

### UPDATE

```sql
UPDATE Clientes
SET cidade = 'Canoas'
WHERE id_cliente = 1;
```

Sem `WHERE`, o comando pode alterar **todas as linhas da tabela**.

---

### DELETE

```sql
DELETE FROM Clientes
WHERE id_cliente = 1;
```

Da mesma forma, sem `WHERE`:

```sql
DELETE FROM Clientes;
```

pode remover todas as linhas da tabela.

---

# 14. INSERT

Utilizado para adicionar novos registros.

```sql
INSERT INTO Clientes (id_cliente, nome, cidade)
VALUES (1, 'Ana', 'Porto Alegre');
```

---

# 15. ORDER BY

A cláusula `ORDER BY` permite ordenar o resultado de uma consulta.

```sql
SELECT *
FROM Clientes
ORDER BY nome;
```

---

# 16. JOIN

O `JOIN` permite consultar informações de **mais de uma tabela**.

Normalmente, o relacionamento ocorre entre:

```text
Primary Key
     ↕
Foreign Key
```

Exemplo:

```sql
SELECT
    Cliente.nome,
    Pedido.valor
FROM Cliente
JOIN Pedido
    ON Cliente.id_cliente = Pedido.id_cliente;
```

O relacionamento entre PK e FK permite descobrir quais registros de uma tabela estão relacionados aos registros da outra.

---

# 17. Aliases

Aliases podem ser utilizados para criar nomes menores para tabelas durante a consulta.

```sql
SELECT
    c.nome,
    p.valor
FROM Cliente AS c
JOIN Pedido AS p
    ON c.id_cliente = p.id_cliente;
```

Nesse exemplo:

```text
c → Cliente
p → Pedido
```

---

# 18. Views

Uma **View** ou **exibição** é uma tabela virtual baseada no resultado de uma consulta `SELECT`.

```text
Tabela
   ↓
SELECT
   ↓
VIEW
```

Ela pode ser consultada e filtrada de maneira semelhante a uma tabela.

### Exemplo conceitual

```sql
CREATE VIEW ClientesPortoAlegre AS

SELECT *
FROM Clientes
WHERE cidade = 'Porto Alegre';
```

Depois:

```sql
SELECT *
FROM ClientesPortoAlegre;
```

---

# 19. Stored Procedures

Um **Stored Procedure — procedimento armazenado** reúne instruções SQL que podem ser executadas quando necessário.

Ele permite encapsular lógica utilizada frequentemente pelas aplicações.

Também pode receber parâmetros.

Exemplo conceitual:

```text
Aplicação
    ↓
Stored Procedure
    ↓
Comandos SQL
    ↓
Banco de dados
```

Isso permite centralizar determinadas operações no próprio banco.

---

# 20. Índices

Um **índice** ajuda o banco de dados a localizar informações com maior eficiência.

Uma analogia simples é o índice de um livro:

```text
Sem índice
→ procurar página por página

Com índice
→ localizar referência
→ ir diretamente para a página
```

No banco:

```text
Consulta
   ↓
Índice
   ↓
Localização das linhas
   ↓
Resultado
```

Um índice pode conter valores de uma determinada coluna organizados juntamente com referências para as linhas correspondentes.

---

## Índices e performance

Em tabelas grandes, índices podem melhorar significativamente o desempenho das consultas.

Mas existe um custo.

Os índices:

* ocupam espaço;
* precisam ser atualizados;
* adicionam trabalho às operações de `INSERT`;
* adicionam trabalho às operações de `UPDATE`;
* adicionam trabalho às operações de `DELETE`.

Por isso, existe um equilíbrio entre:

```text
Mais índices
     ↓
SELECT mais rápido

MAS

INSERT / UPDATE / DELETE
podem ficar mais custosos
```

Em tabelas pequenas, o próprio otimizador pode decidir que ler a tabela inteira é mais eficiente do que utilizar um índice.

---

# 21. Resumo das estruturas relacionais

```text
BANCO RELACIONAL
│
├── Tabela
│   ├── Linhas
│   └── Colunas
│
├── Chaves
│   ├── Primary Key
│   ├── Foreign Key
│   └── Chave composta
│
├── Normalização
│   ├── Separar entidades
│   ├── Separar atributos
│   ├── Reduzir duplicação
│   └── Manter integridade
│
└── SQL
```

---

# 🧠 Mapa mental de SQL

```text
SQL
│
├── DDL → estrutura
│   ├── CREATE
│   ├── ALTER
│   ├── DROP
│   └── RENAME
│
├── DCL → permissões
│   ├── GRANT
│   ├── DENY
│   └── REVOKE
│
└── DML → dados
    ├── SELECT
    ├── INSERT
    ├── UPDATE
    └── DELETE
```

---

# 🧠 Objetos e recursos importantes

```text
VIEW
→ tabela virtual baseada em SELECT

STORED PROCEDURE
→ conjunto de instruções SQL executáveis

INDEX
→ melhora a localização dos registros

PRIMARY KEY
→ identifica uma linha

FOREIGN KEY
→ relaciona tabelas
```

---

# ✅ Pontos que eu levaria para a prova

* **Banco relacional** → dados estruturados organizados em tabelas.
* **Linha** → instância de uma entidade.
* **Coluna** → atributo da entidade.
* **Primary Key** → identifica exclusivamente um registro.
* **Foreign Key** → cria relacionamento entre tabelas.
* **Chave composta** → formada pela combinação de mais de uma coluna.
* **Normalização** → reduz duplicação e ajuda a manter integridade.
* **SQL** → linguagem utilizada para trabalhar com bancos relacionais.
* **T-SQL** → dialeto SQL utilizado pelos produtos Microsoft SQL.
* **DDL** → definição da estrutura.
* **DCL** → controle de permissões.
* **DML** → manipulação dos dados.
* **SELECT** → leitura.
* **INSERT** → inserção.
* **UPDATE** → atualização.
* **DELETE** → exclusão.
* **WHERE** → define quais registros serão afetados.
* **ORDER BY** → ordena os resultados.
* **JOIN** → relaciona dados de tabelas diferentes.
* **View** → tabela virtual baseada em uma consulta.
* **Stored Procedure** → encapsula instruções SQL.
* **Index** → pode acelerar consultas, mas possui custo de manutenção.

---

> Material organizado a partir das minhas próprias anotações durante a preparação para a certificação **Microsoft Azure Data Fundamentals (DP-900)**.
