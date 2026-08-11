# 08 — Visualização e análise com Power BI

> Anotações de estudo para a certificação **Microsoft Azure Data Fundamentals (DP-900)**.

A visualização de dados permite transformar informações em representações visuais que facilitam a identificação de padrões, tendências, comparações e indicadores.

Para cenários empresariais, o **Microsoft Power BI** oferece recursos para:

* conexão com fontes de dados;
* modelagem;
* análise;
* criação de relatórios;
* dashboards;
* visualizações interativas;
* compartilhamento de informações.

---

# 1. Microsoft Power BI

O **Microsoft Power BI** é uma plataforma de Business Intelligence e visualização de dados integrada ao ecossistema Microsoft.

Um fluxo típico de trabalho pode ser representado assim:

```text
Fontes de dados
      ↓
Power BI Desktop
      ↓
Modelo de dados
      ↓
Relatório
      ↓
Power BI Service
      ↓
Compartilhamento
```

---

# 2. Power BI Desktop

O **Power BI Desktop** é uma aplicação utilizada para desenvolver modelos e relatórios.

Nele é possível:

* conectar fontes de dados;
* importar dados;
* combinar dados;
* organizar os dados;
* criar modelos analíticos;
* desenvolver relatórios;
* criar visualizações interativas.

```text
Power BI Desktop
│
├── Conectar
├── Transformar
├── Modelar
└── Visualizar
```

---

# 3. Power BI Service

Depois de criar um relatório, ele pode ser publicado no **Power BI Service**.

O serviço em nuvem permite:

* publicar relatórios;
* compartilhar conteúdo;
* consumir relatórios pelo navegador;
* agendar atualizações;
* criar dashboards;
* organizar aplicativos;
* colaborar com outros usuários.

```text
Power BI Desktop
      ↓
    Publish
      ↓
Power BI Service
```

---

# 4. Consumo dos relatórios

Os usuários podem consumir o conteúdo por:

```text
Power BI Service
│
├── Navegador
└── Aplicativo móvel
```

Isso permite disponibilizar informações para usuários empresariais sem que eles precisem utilizar o Power BI Desktop.

---

# 5. Power BI no Microsoft Fabric

O Power BI também é uma carga de trabalho integrada ao **Microsoft Fabric**.

Dentro do Fabric, relatórios e modelos podem coexistir com recursos de:

* engenharia de dados;
* Data Warehouse;
* Lakehouse;
* OneLake;
* pipelines;
* analytics.

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

# 6. Workspaces

Os **workspaces** são ambientes compartilhados utilizados para colaboração.

Dentro deles, as equipes podem trabalhar com:

* relatórios;
* modelos semânticos;
* outros itens do Microsoft Fabric.

```text
Workspace
│
├── Semantic Model
├── Report
├── Lakehouse
├── Warehouse
└── Outros itens
```

---

# 7. Modelo semântico

Um **modelo semântico** organiza e estrutura os dados utilizados na análise.

Ele pode definir:

* tabelas;
* relacionamentos;
* medidas;
* hierarquias;
* lógica de negócio.

```text
Dados
  ↓
Modelo semântico
│
├── Tabelas
├── Relações
├── Medidas
└── Hierarquias
  ↓
Relatórios
```

Um mesmo modelo semântico pode servir de base para vários relatórios.

---

# 8. Direct Lake

O **Direct Lake** é um modo de armazenamento utilizado pelo Power BI dentro do Microsoft Fabric.

Ele permite consultar dados diretamente no **OneLake**.

```text
OneLake
   ↓
Delta Tables
   ↓
Direct Lake
   ↓
Modelo semântico
   ↓
Power BI
```

A principal ideia é evitar um processo separado de importação e atualização dos dados.

---

# 9. Modelagem analítica

Um modelo analítico organiza dados para facilitar a análise.

Os dois conceitos principais são:

```text
Modelo analítico
│
├── Measures
└── Dimensions
```

---

# 10. Medidas

As **medidas** são valores numéricos utilizados na análise.

Exemplos:

```text
Receita
Quantidade vendida
Lucro
Custo
Número de pedidos
```

Uma medida normalmente responde:

```text
Quanto?
Quantos?
Qual valor?
```

---

# 11. Dimensões

As **dimensões** representam entidades pelas quais as medidas podem ser analisadas.

Exemplos:

```text
Produto
Cliente
Tempo
Loja
Região
```

Assim, podemos responder perguntas como:

```text
Receita por produto
Receita por cliente
Receita por mês
Receita por região
```

---

# 12. Tabelas fato

As **fact tables** armazenam valores relacionados a eventos de negócio.

Exemplo:

```text
FATO_VENDAS

id_produto
id_cliente
id_data
quantidade
receita
```

Cada linha pode representar uma transação ou outro evento registrado.

---

# 13. Tabelas dimensão

As **dimension tables** descrevem entidades utilizadas para filtrar ou agrupar as informações.

Exemplo:

```text
DIM_PRODUTO

id_produto
nome_produto
categoria
marca
```

Outro exemplo:

```text
DIM_CLIENTE

id_cliente
nome
cidade
estado
```

---

# 14. Dimensão Tempo

Modelos analíticos frequentemente possuem uma dimensão específica para datas.

```text
DIM_TEMPO
│
├── Data
├── Dia
├── Mês
├── Trimestre
└── Ano
```

Isso permite analisar medidas ao longo do tempo.

Exemplo:

```text
Receita
  ↓
Ano
  ↓
Trimestre
  ↓
Mês
  ↓
Dia
```

---

# 15. Star Schema

Quando uma tabela fato se relaciona diretamente com várias dimensões, temos um **esquema estrela**.

```text
             DIM_CLIENTE
                  |
DIM_TEMPO — FATO_VENDAS — DIM_PRODUTO
                  |
               DIM_LOJA
```

A tabela fato fica no centro.

As dimensões ficam ao redor.

---

# 16. Snowflake Schema

No **Snowflake Schema**, uma dimensão pode se relacionar com outras tabelas.

```text
FATO_VENDAS
     |
 DIM_PRODUTO
     |
DIM_CATEGORIA
```

Isso cria estruturas mais normalizadas em torno das dimensões.

---

# 17. Star Schema x Snowflake Schema

| Star Schema               | Snowflake Schema                   |
| ------------------------- | ---------------------------------- |
| Estrutura mais simples    | Estrutura mais detalhada           |
| Dimensões ligadas ao fato | Dimensões podem ter outras tabelas |
| Menos relacionamentos     | Mais relacionamentos               |
| Formato de estrela        | Estrutura ramificada               |

---

# 18. VertiPaq

Quando dados são carregados em um modelo semântico do Power BI, eles podem ser armazenados pelo mecanismo **VertiPaq**.

O VertiPaq utiliza armazenamento:

```text
Columnar
+
In-memory
```

Isso permite processamento analítico eficiente.

---

# 19. Armazenamento colunar

Em vez de armazenar os dados principalmente por linha, sistemas analíticos podem utilizar armazenamento baseado em colunas.

```text
Linha tradicional

Cliente | Produto | Receita


Colunar

Cliente
Cliente
Cliente

Produto
Produto
Produto

Receita
Receita
Receita
```

Isso é especialmente eficiente para análises que precisam calcular valores de determinadas colunas em grandes volumes de registros.

---

# 20. Hierarquias

As **hierarquias** permitem navegar entre diferentes níveis de detalhe.

Exemplo de tempo:

```text
Ano
 ↓
Mês
 ↓
Dia
```

Exemplo de produto:

```text
Categoria
    ↓
Produto
```

Exemplo geográfico:

```text
Estado
  ↓
Cidade
```

---

# 21. Drill-down

O **drill-down** permite sair de uma visão mais agregada para uma visão mais detalhada.

```text
2026
 ↓
Agosto
 ↓
11 de agosto
```

Outro exemplo:

```text
Brasil
 ↓
Rio Grande do Sul
 ↓
Porto Alegre
```

---

# 22. Model View

No Power BI Desktop, a **Model View** permite trabalhar com a estrutura do modelo.

Nela é possível:

* criar relacionamentos;
* visualizar tabelas;
* configurar propriedades;
* definir tipos;
* organizar hierarquias;
* configurar formatos.

```text
Model View
│
├── Fact Tables
├── Dimensions
├── Relationships
└── Hierarchies
```

---

# 23. Escolha de visualizações

Uma boa visualização depende do tipo de informação que precisa ser comunicada.

Os principais tipos estudados foram:

```text
Visualizações
│
├── Tabelas
├── Cards
├── Barras
├── Colunas
├── Linhas
├── Pizza
├── Dispersão
└── Mapas
```

---

# 24. Tabelas

Tabelas são adequadas quando é necessário apresentar vários valores detalhados.

Exemplo:

| Produto  | Quantidade | Receita |
| -------- | ---------: | ------: |
| Notebook |        150 | 525.000 |
| Monitor  |        200 | 180.000 |
| Mouse    |        450 |  67.500 |

São úteis quando o usuário precisa consultar valores específicos.

---

# 25. Cards

Cards são úteis para destacar uma única métrica importante.

Exemplo:

```text
┌───────────────────┐
│ Receita Total     │
│                   │
│ R$ 12,5 milhões   │
└───────────────────┘
```

Podem representar:

* receita;
* usuários;
* vendas;
* margem;
* quantidade;
* KPIs.

---

# 26. Gráficos de barras

Os gráficos de barras são adequados para comparar valores entre categorias.

```text
Produto A ██████████
Produto B ███████
Produto C ████
```

Exemplos:

* vendas por produto;
* receita por região;
* chamados por categoria.

---

# 27. Gráficos de colunas

Também são utilizados para comparação entre categorias.

```text
      █
  █   █
  █   █       █
  █   █   █   █
────────────────
 A   B   C   D
```

A diferença principal está na orientação visual.

---

# 28. Gráficos de linha

Os gráficos de linha são especialmente adequados para mostrar **tendências ao longo do tempo**.

```text
Receita
   |
   |             ●
   |         ●
   |     ●
   | ●
   └────────────────
      Jan Fev Mar Abr
```

Exemplos:

* receita mensal;
* usuários ao longo do tempo;
* evolução do custo;
* temperatura diária.

---

# 29. Gráfico de pizza

O gráfico de pizza é utilizado para representar categorias como proporções de um total.

```text
Total = 100%

Produto A → 50%
Produto B → 30%
Produto C → 20%
```

---

# 30. Gráfico de dispersão

O **scatter plot** é útil para analisar a relação entre duas medidas numéricas.

Exemplo:

```text
Receita
  |
  |         •
  |    •       •
  |  •    •
  |      •
  └────────────────
        Investimento
```

Pode ajudar a identificar:

* correlação;
* agrupamentos;
* padrões;
* outliers.

---

# 31. Mapas

Mapas são adequados quando os dados possuem componente geográfico.

Exemplos:

* receita por estado;
* clientes por cidade;
* vendas por região;
* chamados por unidade.

```text
Brasil
│
├── RS → 120 vendas
├── SP → 350 vendas
└── RJ → 210 vendas
```

---

# 32. Relatórios interativos

Uma característica importante do Power BI é a interação entre os visuais.

Ao selecionar um elemento em uma visualização, outras visualizações podem ser:

* filtradas;
* destacadas;
* recalculadas.

```text
Selecionar "Porto Alegre"
          ↓
Gráfico A filtrado
Gráfico B filtrado
Card atualizado
Mapa atualizado
```

---

# 33. IA no Power BI

O Power BI possui recursos de Inteligência Artificial que ajudam na exploração e interpretação dos dados.

Entre os recursos estudados estão:

```text
Power BI + IA
│
├── Copilot
├── Smart Narrative
├── Q&A
├── Key Influencers
└── Decomposition Tree
```

---

# 34. Copilot no Power BI

O **Copilot** permite utilizar linguagem natural para auxiliar na criação e análise de conteúdo.

Nas anotações, aparecem capacidades como:

* resumir relatórios;
* criar páginas de relatório;
* selecionar visuais;
* gerar medidas DAX.

```text
Usuário
   ↓
"Crie uma medida de receita acumulada"
   ↓
Copilot
   ↓
DAX
```

---

# 35. Smart Narrative

A **Smart Narrative** gera automaticamente descrições textuais sobre os dados.

```text
Visualização
     ↓
Smart Narrative
     ↓
Resumo textual
```

O texto pode mudar automaticamente conforme os dados ou filtros do relatório são alterados.

---

# 36. Visual de Q&A

O visual de **Q&A** permite realizar perguntas em linguagem natural.

Exemplo:

```text
"Qual foi a receita por região em 2026?"
```

O Power BI utiliza o modelo semântico para gerar uma resposta visual.

```text
Pergunta
  ↓
Modelo semântico
  ↓
Visualização
```

---

# 37. Key Influencers

O visual **Key Influencers** busca identificar os fatores que mais influenciam uma determinada métrica.

Exemplo:

```text
O que mais influencia
o cancelamento?
        ↓
Preço
Região
Tempo de contrato
Tipo de cliente
```

---

# 38. Decomposition Tree

A **Decomposition Tree** permite decompor uma métrica por diferentes dimensões.

Exemplo:

```text
Receita
  ↓
Região
  ↓
Estado
  ↓
Cidade
  ↓
Produto
```

É útil para investigar quais fatores estão contribuindo para determinado resultado.

---

# 39. Visualização x objetivo

| Objetivo                 | Visual indicado    |
| ------------------------ | ------------------ |
| Mostrar um único KPI     | Card               |
| Mostrar dados detalhados | Tabela             |
| Comparar categorias      | Barras ou colunas  |
| Analisar tendência       | Linha              |
| Mostrar proporção        | Pizza              |
| Comparar duas medidas    | Dispersão          |
| Comparar localidades     | Mapa               |
| Investigar fatores       | Key Influencers    |
| Explorar hierarquias     | Decomposition Tree |

---

# 40. Fluxo completo de análise no Power BI

```text
Fontes
  ↓
Power BI Desktop
  ↓
Transformação
  ↓
Modelo semântico
  ↓
Medidas + Dimensões
  ↓
Visualizações
  ↓
Relatório
  ↓
Power BI Service / Fabric
  ↓
Compartilhamento
  ↓
Decisão
```

---

# 🧠 Mapa mental

```text
POWER BI
│
├── Desenvolvimento
│   ├── Power BI Desktop
│   └── Power BI Service
│
├── Microsoft Fabric
│   ├── Workspace
│   ├── OneLake
│   └── Direct Lake
│
├── Modelo semântico
│   ├── Measures
│   ├── Dimensions
│   ├── Fact Tables
│   ├── Relationships
│   └── Hierarchies
│
├── Modelagem
│   ├── Star Schema
│   └── Snowflake Schema
│
├── Visualizações
│   ├── Table
│   ├── Card
│   ├── Bar
│   ├── Column
│   ├── Line
│   ├── Pie
│   ├── Scatter
│   └── Map
│
└── IA
    ├── Copilot
    ├── Smart Narrative
    ├── Q&A
    ├── Key Influencers
    └── Decomposition Tree
```

---

# ✅ Pontos que eu levaria para a prova

* **Power BI Desktop** → criação de modelos e relatórios.
* **Power BI Service** → publicação, compartilhamento e consumo.
* **Power BI** → integrado ao Microsoft Fabric.
* **Workspace** → ambiente colaborativo.
* **Modelo semântico** → define medidas, relações e hierarquias.
* **Direct Lake** → consulta dados do OneLake sem processo tradicional de importação.
* **Measure** → valor numérico analisado.
* **Dimension** → entidade usada para filtrar ou agrupar medidas.
* **Fact Table** → eventos e métricas.
* **Dimension Table** → atributos para análise.
* **Star Schema** → fato central ligada às dimensões.
* **Snowflake Schema** → dimensões relacionadas a outras tabelas.
* **VertiPaq** → mecanismo colunar em memória utilizado pelo Power BI.
* **Hierarchy** → diferentes níveis de agregação.
* **Drill-down** → navegar para maior detalhe.
* **Tabela** → valores detalhados.
* **Card** → KPI individual.
* **Bar/Column** → comparação de categorias.
* **Line** → tendências no tempo.
* **Pie** → proporções de um total.
* **Scatter** → relação entre duas medidas.
* **Map** → análise geográfica.
* **Relatórios Power BI** → visuais relacionados interagem entre si.
* **Copilot** → assistência com linguagem natural.
* **Smart Narrative** → resumo textual automático.
* **Q&A** → perguntas em linguagem natural.
* **Key Influencers** → fatores que influenciam uma métrica.
* **Decomposition Tree** → análise detalhada por diferentes dimensões.

---

> Material organizado a partir das minhas próprias anotações durante a preparação para a certificação **Microsoft Azure Data Fundamentals (DP-900)**.

