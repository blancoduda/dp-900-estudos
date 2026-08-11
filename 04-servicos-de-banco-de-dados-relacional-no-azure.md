# 04 — Serviços de banco de dados relacional no Azure

> Anotações de estudo para a certificação **Microsoft Azure Data Fundamentals (DP-900)**.

O Microsoft Azure oferece diferentes serviços para executar bancos de dados relacionais na nuvem, incluindo soluções baseadas em **SQL Server, MySQL e PostgreSQL**.

Grande parte desses serviços é gerenciada pelo Azure, reduzindo a necessidade de administrar diretamente infraestrutura, atualizações, backups e disponibilidade.

---

# 1. Azure SQL

**Azure SQL** é o nome dado à família de serviços de banco de dados baseados no mecanismo do **Microsoft SQL Server**.

As principais opções são:

```text
Azure SQL
│
├── SQL Server em Azure VM
│   └── IaaS
│
├── Azure SQL Managed Instance
│   └── PaaS
│
└── Azure SQL Database
    └── PaaS
```

Cada opção oferece um nível diferente de:

* controle;
* gerenciamento;
* compatibilidade com SQL Server;
* responsabilidade administrativa.

---

# 2. IaaS x PaaS

Antes de comparar os serviços, é importante entender a diferença entre os modelos.

## IaaS — Infrastructure as a Service

A infraestrutura é disponibilizada na nuvem, mas grande parte da administração continua sob responsabilidade do cliente.

Exemplo:

```text
SQL Server em Azure VM
        ↓
       IaaS
```

Nesse modelo, existe maior controle sobre:

* sistema operacional;
* SQL Server;
* configurações;
* atualizações;
* backups;
* recursos da máquina virtual.

---

## PaaS — Platform as a Service

O Azure assume uma parte maior da administração da infraestrutura e da plataforma.

Exemplos:

```text
Azure SQL Managed Instance
Azure SQL Database
        ↓
       PaaS
```

Tarefas como atualizações, backups e recuperação podem ser automatizadas pelo próprio serviço.

---

# 3. SQL Server em Máquinas Virtuais do Azure

O **SQL Server em Azure Virtual Machines** permite executar uma instalação completa do SQL Server dentro de uma máquina virtual hospedada no Azure.

É uma solução **IaaS**.

```text
Azure
   ↓
Virtual Machine
   ↓
Sistema Operacional
   ↓
SQL Server
   ↓
Bancos de dados
```

Essa opção oferece alto nível de controle sobre o ambiente.

O cliente continua responsável pela administração do:

* sistema operacional;
* SQL Server;
* configurações;
* atualizações;
* backups;
* manutenção.

---

## Quando usar SQL Server em VM?

É especialmente adequado quando:

* é necessário manter alto nível de compatibilidade com um ambiente existente;
* o aplicativo depende de recursos específicos do sistema operacional;
* é necessário controle administrativo completo;
* a organização deseja realizar uma migração com poucas alterações.

Um cenário comum é o chamado:

### Lift-and-shift

```text
SQL Server local
        ↓
      Migração
        ↓
SQL Server em Azure VM
```

A ideia é mover a aplicação e o banco para a nuvem realizando o menor número possível de alterações.

---

## Vantagens

* grande compatibilidade com SQL Server existente;
* controle sobre o sistema operacional;
* controle sobre o DBMS;
* possibilidade de utilizar recursos específicos;
* adequado para ambientes híbridos;
* útil para desenvolvimento e testes.

---

## Ponto de atenção

Maior controle também significa **maior responsabilidade administrativa**.

```text
Mais controle
     ↓
Mais administração
```

---

# 4. Azure SQL Managed Instance

O **Azure SQL Managed Instance** é uma solução **PaaS** que oferece alta compatibilidade com instalações tradicionais do SQL Server.

Ele permite hospedar vários bancos de dados dentro de uma mesma instância.

```text
Azure SQL Managed Instance
│
├── Banco A
├── Banco B
└── Banco C
```

O serviço automatiza diversas tarefas administrativas, como:

* backups;
* aplicação de patches;
* monitoramento;
* manutenção;
* configuração de alta disponibilidade.

Ao mesmo tempo, ainda oferece bastante controle sobre segurança e recursos dos bancos.

---

## Compatibilidade

Uma das principais vantagens do Managed Instance é a alta compatibilidade com SQL Server existente.

```text
SQL Server local
       ↓
poucas alterações
       ↓
Managed Instance
```

Por isso, é uma opção importante para organizações que desejam migrar bancos SQL Server para a nuvem sem assumir toda a administração de uma máquina virtual.

---

## Quando usar?

Considere **Azure SQL Managed Instance** quando:

* existe uma solução SQL Server já implementada;
* é necessário manter alta compatibilidade;
* deseja-se reduzir o trabalho administrativo;
* a aplicação depende de recursos avançados do SQL Server;
* é desejável realizar uma migração com poucas alterações.

---

# 5. Azure SQL Database

O **Azure SQL Database** é uma solução de banco de dados **PaaS totalmente gerenciada**.

É especialmente adequada para aplicações desenvolvidas diretamente para a nuvem.

```text
Aplicação
    ↓
Azure SQL Database
    ↓
Infraestrutura gerenciada
pela Microsoft
```

Nesse modelo, a Microsoft cuida da maior parte da infraestrutura e manutenção do banco.

---

# 6. Banco de dados individual

Uma das formas de utilizar o Azure SQL Database é por meio de um **Single Database**.

```text
Servidor lógico
      ↓
Banco de dados
```

O Azure gerencia a infraestrutura necessária, enquanto o usuário trabalha principalmente com:

* estrutura do banco;
* tabelas;
* dados;
* consultas;
* configuração de recursos.

O banco também pode ser escalado conforme a necessidade de:

* CPU;
* memória;
* armazenamento.

---

# 7. Pool Elástico

Um **Elastic Pool** permite que vários bancos de dados compartilhem um conjunto de recursos.

```text
Elastic Pool
│
├── Banco A
├── Banco B
├── Banco C
└── Banco D
```

Esses bancos podem compartilhar recursos como:

* processamento;
* memória;
* armazenamento.

É útil quando diferentes bancos possuem picos de utilização em momentos distintos.

---

## Exemplo

Imagine dois bancos:

```text
Folha de pagamento
→ grande uso no final do mês

Relatórios
→ grande uso no meio do mês
```

Em vez de reservar uma grande quantidade de recursos permanentemente para cada banco, eles podem utilizar recursos compartilhados de um pool.

---

# 8. Hyperscale

A camada **Hyperscale** é voltada para bancos de dados muito grandes.

Nas anotações estudadas, ela é apresentada como capaz de suportar bancos de até **100 TB**, além de oferecer:

* dimensionamento rápido;
* backup rápido;
* restauração independente do tamanho total dos dados.

---

# 9. Características do Azure SQL Database

O Azure SQL Database possui recursos gerenciados relacionados a:

### Escalabilidade

Os recursos podem ser aumentados conforme a demanda.

### Alta disponibilidade

O serviço foi projetado para manter os bancos disponíveis mesmo diante de falhas.

### Atualizações automáticas

A Microsoft gerencia atualizações e patches do SQL Server utilizado pelo serviço.

### Backup e recuperação

Possui recursos de restauração para pontos anteriores no tempo.

### Resiliência

Bancos podem ser replicados entre diferentes regiões.

### Segurança

Inclui recursos como:

* criptografia em repouso;
* criptografia em trânsito;
* monitoramento;
* detecção de ameaças;
* auditoria.

---

# 10. Comparando as três opções Azure SQL

| Característica                 | SQL Server em VM                  | Managed Instance | Azure SQL Database        |
| ------------------------------ | --------------------------------- | ---------------- | ------------------------- |
| Modelo                         | IaaS                              | PaaS             | PaaS                      |
| Controle                       | Alto                              | Intermediário    | Menor                     |
| Administração                  | Alta                              | Reduzida         | Mínima                    |
| Compatibilidade com SQL Server | Muito alta                        | Quase completa   | Menor                     |
| Vários bancos por instância    | Sim                               | Sim              | Modelo orientado ao banco |
| Lift-and-shift                 | Excelente                         | Excelente        | Menos indicado            |
| Cloud-native                   | Menos                             | Intermediário    | Excelente                 |
| Atualizações gerenciadas       | Não totalmente                    | Sim              | Sim                       |
| Backups gerenciados            | Responsabilidade maior do cliente | Sim              | Sim                       |

---

# 11. Como escolher?

Uma forma simples de pensar:

```text
Preciso de controle total
ou recursos específicos do SO?
        ↓
SQL Server em VM
```

```text
Tenho SQL Server existente
e quero alta compatibilidade
com menos administração?
        ↓
Managed Instance
```

```text
Estou criando uma aplicação
moderna para nuvem e quero
o mínimo de administração?
        ↓
Azure SQL Database
```

---

# 12. Relação entre controle e gerenciamento

Uma forma útil de visualizar:

```text
MAIS CONTROLE
     ↑

SQL Server em VM

Managed Instance

Azure SQL Database

     ↓
MAIS GERENCIAMENTO
PELO AZURE
```

---

# 13. Bancos relacionais de código aberto no Azure

Além das soluções baseadas em SQL Server, o Azure também oferece serviços gerenciados para bancos de dados relacionais de código aberto.

Os principais estudados foram:

```text
Azure Database
│
├── for MySQL
│
└── for PostgreSQL
```

Esses serviços permitem migrar aplicações que já utilizam essas tecnologias para o Azure sem necessariamente alterar completamente sua arquitetura.

---

# 14. MySQL

O **MySQL** é um sistema de gerenciamento de banco de dados relacional de código aberto.

É historicamente bastante utilizado em aplicações web.

Um exemplo clássico é a stack:

```text
LAMP

Linux
Apache
MySQL
PHP
```

---

# 15. Azure Database for MySQL

O **Azure Database for MySQL** disponibiliza o MySQL como um serviço **PaaS** no Azure.

Ele é baseado na Community Edition do MySQL.

Entre os recursos estudados estão:

* alta disponibilidade;
* escalabilidade;
* backups automáticos;
* restauração point-in-time;
* segurança de conexão;
* regras de firewall;
* suporte a SSL;
* monitoramento;
* métricas;
* logs;
* pagamento conforme utilização.

Como a infraestrutura é gerenciada pelo Azure, não é necessário administrar diretamente servidores, hardware e patches do sistema subjacente.

---

# 16. Flexible Server — MySQL

A opção **Flexible Server** permite maior flexibilidade sobre configurações do servidor.

Ela oferece:

* maior controle de configuração;
* opções de otimização de custos;
* serviço totalmente gerenciado.

Nas anotações utilizadas para esta preparação, essa é apresentada como a opção recomendada para novas cargas de trabalho com MySQL.

---

# 17. PostgreSQL

O **PostgreSQL** é um sistema de banco de dados relacional com recursos objeto-relacionais.

Além de tabelas relacionais tradicionais, ele permite utilizar:

* tipos de dados personalizados;
* extensões;
* recursos especializados;
* dados geométricos.

```text
PostgreSQL
│
├── Relacional
└── Recursos objeto-relacionais
```

---

# 18. Azure Database for PostgreSQL

O **Azure Database for PostgreSQL** oferece PostgreSQL como serviço **PaaS** no Azure.

Entre os benefícios estão:

* alta disponibilidade;
* desempenho;
* escalabilidade;
* segurança;
* administração gerenciada;
* detecção de falhas;
* failover.

---

# 19. Flexible Server — PostgreSQL

O **Flexible Server** também está disponível para PostgreSQL.

Ele oferece maior controle sobre:

* configuração;
* parâmetros do servidor;
* otimização de custos.

Ao mesmo tempo, continua sendo um serviço totalmente gerenciado.

---

# 20. pgAdmin

Usuários de PostgreSQL podem continuar utilizando o **pgAdmin** para administrar e monitorar bancos hospedados no Azure.

Porém, algumas operações relacionadas diretamente ao servidor não ficam disponíveis, porque a infraestrutura é administrada pela Microsoft.

---

# 21. Comparação geral

| Serviço                       | Tecnologia | Modelo | Melhor cenário                    |
| ----------------------------- | ---------- | ------ | --------------------------------- |
| SQL Server em Azure VM        | SQL Server | IaaS   | Controle máximo e lift-and-shift  |
| Azure SQL Managed Instance    | SQL Server | PaaS   | Migração com alta compatibilidade |
| Azure SQL Database            | SQL Server | PaaS   | Aplicações cloud-native           |
| Azure Database for MySQL      | MySQL      | PaaS   | Aplicações baseadas em MySQL      |
| Azure Database for PostgreSQL | PostgreSQL | PaaS   | Aplicações baseadas em PostgreSQL |

---

# 🧠 Mapa mental

```text
BANCOS RELACIONAIS NO AZURE
│
├── Microsoft SQL Server
│   │
│   ├── SQL Server em VM
│   │   ├── IaaS
│   │   ├── controle máximo
│   │   └── lift-and-shift
│   │
│   ├── Managed Instance
│   │   ├── PaaS
│   │   ├── alta compatibilidade
│   │   └── menos administração
│   │
│   └── Azure SQL Database
│       ├── PaaS
│       ├── totalmente gerenciado
│       ├── Single Database
│       ├── Elastic Pool
│       └── Hyperscale
│
├── MySQL
│   └── Azure Database for MySQL
│
└── PostgreSQL
    └── Azure Database for PostgreSQL
```

---

# ✅ Pontos que eu levaria para a prova

* **Azure SQL** → família de serviços baseados no Microsoft SQL Server.
* **SQL Server em Azure VM** → IaaS.
* **SQL Server em VM** → maior controle e maior responsabilidade administrativa.
* **Lift-and-shift** → migração com poucas alterações.
* **Azure SQL Managed Instance** → PaaS com alta compatibilidade com SQL Server.
* **Managed Instance** → boa opção para migrar SQL Server existente reduzindo administração.
* **Azure SQL Database** → PaaS totalmente gerenciado.
* **Azure SQL Database** → especialmente adequado para aplicações modernas em nuvem.
* **Single Database** → banco individual com recursos próprios.
* **Elastic Pool** → vários bancos compartilham recursos.
* **Hyperscale** → voltado para bancos muito grandes.
* **PaaS** → Azure assume mais tarefas de infraestrutura e manutenção.
* **IaaS** → cliente mantém maior controle e responsabilidade.
* **Azure Database for MySQL** → MySQL gerenciado como PaaS.
* **Azure Database for PostgreSQL** → PostgreSQL gerenciado como PaaS.
* **MySQL** → muito associado historicamente à stack LAMP.
* **PostgreSQL** → banco relacional com recursos objeto-relacionais.
* **Flexible Server** → maior flexibilidade de configuração mantendo o serviço gerenciado.

---

> Material organizado a partir das minhas próprias anotações durante a preparação para a certificação **Microsoft Azure Data Fundamentals (DP-900)**.

