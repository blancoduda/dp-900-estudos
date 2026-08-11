# 07 — Análise de dados em tempo real

> Anotações de estudo para a certificação **Microsoft Azure Data Fundamentals (DP-900)**.

A análise em tempo real trabalha com dados que são gerados continuamente e precisam ser processados com baixa latência.

Neste módulo, os principais conceitos estudados são:

* processamento em lote;
* processamento de streaming;
* arquitetura de processamento de fluxo;
* Azure Event Hubs;
* Azure IoT Hub;
* Azure Stream Analytics;
* Microsoft Fabric Real-Time Intelligence;
* Apache Spark Structured Streaming;
* Delta Lake.

---

# 1. Processamento de dados

Processar dados significa transformar dados brutos em informações úteis.

Existem duas formas gerais de processamento:

```text
Processamento de dados
│
├── Batch
└── Streaming
```

---

# 2. Processamento em lote — Batch

No **processamento em lote**, os dados são acumulados antes de serem processados.

```text
Dados
  ↓
Dados
  ↓
Dados
  ↓
Lote acumulado
  ↓
Processamento
```

Em vez de processar cada registro imediatamente, o sistema espera até que determinado conjunto de dados esteja disponível.

O processamento pode ser iniciado:

* em um horário agendado;
* após determinado volume de dados;
* em resposta a algum evento.

---

# 3. Características do processamento em lote

O batch é adequado principalmente quando:

* existem grandes volumes de dados;
* os resultados não precisam ser imediatos;
* o processamento pode ser agendado;
* existe necessidade de análises mais complexas.

Exemplo:

```text
Durante o dia
↓
Transações acumuladas
↓
23:00
↓
Processamento do lote
↓
Relatório diário
```

---

## Vantagens

* processa grandes volumes de maneira eficiente;
* pode executar em horários com menor utilização dos sistemas;
* adequado para processamento histórico;
* permite análises complexas.

---

## Desvantagens

* existe atraso entre a chegada do dado e o resultado;
* o processamento pode depender da preparação de todo o lote;
* erros podem comprometer a execução inteira;
* pode exigir validação antes do reprocessamento.

---

# 4. Processamento de streaming

No **processamento de streaming**, os dados são processados à medida que chegam.

```text
Evento
  ↓
Processamento
  ↓
Resultado

Evento
  ↓
Processamento
  ↓
Resultado
```

Não é necessário esperar a formação de um grande conjunto de dados.

---

# 5. Quando utilizar streaming?

Streaming é adequado quando existem dados sendo produzidos continuamente e o tempo de resposta é importante.

Exemplos:

* sensores IoT;
* telemetria;
* logs;
* monitoramento;
* transações;
* redes sociais;
* alertas;
* eventos de sistemas.

Um exemplo apresentado nas anotações é um sistema de detecção de incêndio, em que esperar horas para processar os dados não seria aceitável.

---

# 6. Batch x Streaming

| Característica         | Batch             | Streaming                          |
| ---------------------- | ----------------- | ---------------------------------- |
| Processamento          | Em grupos         | Contínuo                           |
| Dados                  | Grandes conjuntos | Eventos individuais ou micro-lotes |
| Latência               | Maior             | Baixa                              |
| Histórico              | Forte             | Dados recentes                     |
| Complexidade analítica | Pode ser alta     | Geralmente operações rápidas       |
| Resposta imediata      | Não               | Sim                                |

---

# 7. Escopo dos dados

No processamento em lote, normalmente é possível trabalhar com todo o conjunto de dados disponível.

```text
Batch
↓
Histórico completo
```

No streaming, geralmente trabalhamos com:

* eventos recém-chegados;
* pequenos conjuntos;
* janelas de tempo.

Exemplo:

```text
Últimos 30 segundos
Últimos 5 minutos
Última hora
```

---

# 8. Latência

**Latência** é o tempo entre a chegada do dado e seu processamento.

```text
Dado chega
   ↓
Latência
   ↓
Resultado disponível
```

Em batch, essa latência tende a ser maior.

Em streaming, o objetivo é processar dados com latência de segundos ou milissegundos.

---

# 9. Micro-batches

Algumas soluções de streaming processam pequenos grupos de registros conhecidos como **micro-batches**.

```text
Evento 1
Evento 2
Evento 3
   ↓
Micro-batch
   ↓
Processamento
```

É uma abordagem intermediária entre processar grandes lotes e processar cada evento isoladamente.

---

# 10. Janelas de tempo

Uma operação comum em streaming é analisar dados dentro de um período específico.

Por exemplo:

```text
Janela = últimos 60 segundos

Eventos
│
├── 10:00:01
├── 10:00:08
├── 10:00:30
└── 10:00:55
      ↓
Agregação
      ↓
Eventos por minuto
```

Isso permite calcular:

* contagens;
* médias;
* somas;
* máximos;
* mínimos.

As anotações descrevem esse tipo de processamento como consultas sobre períodos temporais ou **windows**.

---

# 11. Combinação de Batch e Streaming

Muitas arquiteturas utilizam os dois tipos de processamento.

```text
                 ┌── Streaming ──→ Dashboard em tempo real
Dados chegando ──┤
                 └── Storage ────→ Batch / análise histórica
```

Assim é possível analisar:

* o que está acontecendo agora;
* o que aconteceu historicamente.

---

# 12. Exemplo

Imagine dados de trânsito.

O streaming pode responder:

```text
Quantos carros passaram
nos últimos 5 minutos?
```

Enquanto o processamento em lote pode responder:

```text
Qual foi o volume médio
de veículos no último ano?
```

A mesma solução pode utilizar os dois modelos.

---

# 13. Arquiteturas Lambda, Delta e Kappa

As anotações citam algumas arquiteturas utilizadas na combinação de processamento.

### Lambda

Combina uma camada de processamento histórico com uma camada de streaming.

```text
          ┌── Batch
Dados ────┤
          └── Streaming
```

### Kappa

Trata os dados principalmente como um fluxo contínuo.

```text
Dados
 ↓
Streaming
 ↓
Processamento
```

Quando é necessário reprocessar dados históricos, os eventos podem ser reproduzidos novamente.

### Delta

Também aparece como uma arquitetura utilizada em cenários que combinam batch e streaming.

Os detalhes dessas arquiteturas ficaram fora do escopo aprofundado do material estudado.

---

# 14. Arquitetura de processamento de fluxo

Uma arquitetura simples de streaming pode ser representada assim:

```text
Evento
  ↓
Fonte
  ↓
Processamento
  ↓
Coletor / Saída
```

---

# 15. Evento

O fluxo começa quando algum evento gera dados.

Exemplos:

* sensor envia uma leitura;
* usuário publica uma mensagem;
* aplicação gera um log;
* compra é realizada;
* dispositivo IoT envia telemetria.

```text
Evento
↓
Dados digitais
```

---

# 16. Fonte de streaming

Os dados são capturados por uma **streaming source**.

Essa fonte pode ser:

* fila;
* serviço de eventos;
* arquivo;
* banco de dados;
* sistema de mensagens.

```text
Produtor
   ↓
Fonte de streaming
   ↓
Consumidor
```

Filas e serviços de eventos ajudam a controlar questões como ordenação e entrega dos eventos.

---

# 17. Processamento

O dado é processado por uma operação ou consulta que permanece ativa.

As anotações chamam esse conceito de:

**consulta perpétua — perpetual query**

```text
Streaming
   ↓
Consulta sempre ativa
   ↓
Filtrar
Agregar
Transformar
```

Exemplo:

```text
Contar leituras de sensores
por minuto
```

---

# 18. Coletor — Sink

Depois do processamento, o resultado é enviado para uma saída.

Essa saída também pode ser chamada de **sink**.

```text
Streaming
   ↓
Processamento
   ↓
Sink
```

Exemplos:

* arquivo;
* Data Lake;
* tabela SQL;
* dashboard;
* outra fila;
* plataforma analítica.

---

# 19. Serviços de análise em tempo real

Entre os principais serviços e tecnologias estudados estão:

```text
Real-Time Analytics
│
├── Microsoft Fabric Real-Time Intelligence
├── Spark Structured Streaming
└── Azure Stream Analytics
```

---

# 20. Microsoft Fabric Real-Time Intelligence

O **Real-Time Intelligence** é o conjunto de recursos do Microsoft Fabric voltado para dados em tempo real.

Ele cobre etapas como:

```text
Ingestão
   ↓
Processamento
   ↓
Armazenamento
   ↓
Consulta
   ↓
Visualização
   ↓
Ações
```

---

# 21. Componentes do Real-Time Intelligence

Nas anotações aparecem recursos como:

```text
Real-Time Intelligence
│
├── Eventstream
├── Eventhouse
├── Real-Time Dashboards
└── Activator
```

---

# 22. Eventstream

O **Eventstream** é utilizado para:

* receber eventos;
* rotear dados;
* filtrar dados;
* transformar streams;
* encaminhar os eventos para destinos.

```text
Fonte
  ↓
Eventstream
  ↓
Filtrar / transformar
  ↓
Destino
```

---

# 23. Eventhouse

O **Eventhouse** é otimizado para dados de eventos e séries temporais.

É adequado para:

* logs;
* telemetria;
* eventos;
* séries temporais.

Os dados podem ser consultados utilizando:

**KQL — Kusto Query Language**

```text
Logs / Telemetria
       ↓
    Eventhouse
       ↓
       KQL
```

---

# 24. Real-Time Dashboards

Os dashboards em tempo real permitem acompanhar dados enquanto eles estão sendo recebidos.

```text
Eventos
   ↓
Processamento
   ↓
Dashboard
   ↓
Atualização contínua
```

Isso é útil para:

* monitoramento operacional;
* IoT;
* telemetria;
* indicadores em tempo real.

---

# 25. Activator

O **Activator** pode disparar ações automaticamente quando determinadas condições são atendidas.

Exemplo:

```text
Temperatura > limite
        ↓
     Activator
        ↓
      Alerta
```

---

# 26. Real-Time Hub

O **Real-Time Hub** funciona como um catálogo centralizado para fontes de dados de streaming dentro do Microsoft Fabric.

Ele facilita:

* descoberta;
* acesso;
* exploração;
* compartilhamento de streams;
* reutilização entre equipes.

```text
Streams da organização
        ↓
   Real-Time Hub
        ↓
Equipes / Analytics
```

---

# 27. Azure Stream Analytics

O **Azure Stream Analytics** é um serviço PaaS para processamento de streaming.

O fluxo geral é:

```text
Input
  ↓
Azure Stream Analytics
  ↓
Perpetual Query
  ↓
Output
```

Ele permite:

* receber streams;
* executar consultas continuamente;
* filtrar dados;
* agregar valores;
* produzir resultados;
* enviar os resultados para outros serviços.

---

# 28. Quando utilizar Azure Stream Analytics?

É uma opção adequada para cenários de streaming independentes ou híbridos fora do Microsoft Fabric.

Exemplo:

```text
Event Hub
    ↓
Stream Analytics
    ↓
SQL Database
```

ou:

```text
IoT Hub
   ↓
Stream Analytics
   ↓
Power BI
```

---

# 29. Fontes de dados de streaming no Azure

As principais fontes estudadas foram:

```text
Streaming Sources
│
├── Azure Event Hubs
├── Azure IoT Hub
├── ADLS Gen2
└── Apache Kafka
```

---

# 30. Azure Event Hubs

O **Azure Event Hubs** é utilizado para ingestão de grandes volumes de eventos.

```text
Milhares / milhões
de eventos
      ↓
Azure Event Hubs
      ↓
Consumidores
```

Os eventos são organizados em partições.

Dentro de uma partição, os eventos são entregues em ordem.

Nas anotações, o Event Hubs oferece garantia de entrega **at least once**.

---

# 31. Azure IoT Hub

O **Azure IoT Hub** é semelhante ao Event Hubs, porém voltado especialmente para dispositivos IoT.

```text
Sensores
Dispositivos
Máquinas
    ↓
Azure IoT Hub
    ↓
Analytics
```

É adequado para cenários em que é necessário gerenciar comunicação e eventos provenientes de dispositivos.

---

# 32. ADLS Gen2 como fonte

O **Azure Data Lake Storage Gen2** é normalmente associado ao processamento em lote, mas também pode aparecer como fonte em cenários de streaming.

```text
ADLS Gen2
    ↓
Processamento
```

---

# 33. Apache Kafka

O **Apache Kafka** é uma solução open source muito utilizada para ingestão e transporte de eventos.

É frequentemente utilizado em conjunto com tecnologias como Apache Spark.

```text
Produtores
    ↓
  Kafka
    ↓
Consumidores
```

---

# 34. Destinos do processamento de streaming

Os dados processados podem ser enviados para diferentes destinos.

```text
Processamento
     ↓
   Outputs
```

Exemplos:

* Azure Event Hubs;
* ADLS Gen2;
* OneLake;
* Blob Storage;
* Azure SQL Database;
* Azure Databricks;
* Microsoft Fabric;
* Power BI.

---

# 35. Persistência em arquivos

Resultados podem ser armazenados em:

```text
ADLS Gen2
OneLake
Blob Storage
```

Isso permite utilizar os dados posteriormente em análises históricas.

```text
Streaming
   ↓
Storage
   ↓
Histórico
   ↓
Batch Analytics
```

---

# 36. Persistência em tabelas

Resultados também podem ser enviados para:

* Azure SQL Database;
* Azure Databricks;
* Microsoft Fabric.

```text
Stream
  ↓
Processing
  ↓
Tabela
  ↓
SQL / Analytics
```

---

# 37. Power BI

O Power BI pode receber resultados processados para criar:

* visualizações;
* relatórios;
* dashboards em tempo real.

```text
Eventos
  ↓
Processamento
  ↓
Power BI
  ↓
Dashboard
```

---

# 38. Apache Spark

O **Apache Spark** é um mecanismo de processamento distribuído.

Em vez de processar todos os dados em um único computador, ele distribui o trabalho entre vários nós.

```text
Dados
  ↓
Cluster Spark
├── Nó 1
├── Nó 2
├── Nó 3
└── Nó 4
  ↓
Resultado
```

No Azure, as anotações citam Spark em:

* Microsoft Fabric;
* Azure Databricks.

---

# 39. Spark e linguagens

O Spark permite trabalhar com linguagens como:

```text
Python
Scala
Java
```

Além disso, pode executar:

```text
Batch
+
Streaming
```

---

# 40. Spark Structured Streaming

O **Spark Structured Streaming** é uma biblioteca integrada ao Spark para processamento de dados em streaming.

A ideia é tratar um fluxo contínuo de eventos de maneira semelhante a uma tabela que recebe novas linhas constantemente.

```text
Tabela
│
├── Registro 1
├── Registro 2
├── Registro 3
├── Registro 4 ← novo
└── Registro 5 ← novo
```

---

# 41. Quando utilizar Structured Streaming?

É adequado principalmente quando a solução já utiliza Spark e precisa incorporar dados em tempo real.

```text
Spark Batch
    +
Streaming
    ↓
Structured Streaming
```

Pode ser utilizado em:

* Microsoft Fabric;
* Azure Databricks.

---

# 42. Delta Lake em cenários de streaming

O **Delta Lake** adiciona confiabilidade sobre arquivos de um Data Lake.

Entre os benefícios destacados estão:

* confiabilidade;
* imposição de esquema;
* suporte conjunto a batch e streaming.

---

# 43. Batch e Streaming na mesma tabela Delta

Uma mesma tabela Delta pode receber dados em streaming e depois ser utilizada em análises históricas.

```text
Streaming
   ↓
Delta Table
   ↑
Batch
```

Isso evita manter armazenamentos separados para dados históricos e dados em tempo real.

---

# 44. Structured Streaming + Delta Lake

A combinação:

```text
Spark Structured Streaming
           +
       Delta Lake
           ↓
Streaming confiável
+
Análise histórica
```

é útil quando se deseja utilizar uma única camada consistente de dados para processamento em tempo real e batch.

---

# 45. Comparando tecnologias

| Tecnologia                 | Principal função                               |
| -------------------------- | ---------------------------------------------- |
| Azure Event Hubs           | Ingestão de eventos em grande escala           |
| Azure IoT Hub              | Ingestão e gerenciamento de eventos IoT        |
| Apache Kafka               | Plataforma open source de eventos              |
| Azure Stream Analytics     | Processamento de streaming                     |
| Fabric Eventstream         | Ingestão e roteamento no Fabric                |
| Fabric Eventhouse          | Armazenamento e análise de eventos             |
| Real-Time Dashboard        | Visualização em tempo real                     |
| Activator                  | Ações automáticas                              |
| Spark Structured Streaming | Processamento de streaming com Spark           |
| Delta Lake                 | Armazenamento confiável para batch e streaming |
| Power BI                   | Visualização dos resultados                    |

---

# 46. Fluxo de exemplo com Azure

```text
IoT Device
    ↓
Azure IoT Hub
    ↓
Azure Stream Analytics
    ↓
Filtro / agregação
    ↓
    ├── Power BI
    │      ↓
    │   Dashboard
    │
    └── ADLS Gen2
           ↓
      Histórico
```

---

# 47. Fluxo de exemplo com Microsoft Fabric

```text
Event Hubs / Kafka / IoT
          ↓
      Eventstream
          ↓
       Eventhouse
          ↓
          KQL
          ↓
Real-Time Dashboard
          ↓
       Activator
          ↓
        Ação
```

---

# 48. Fluxo com Spark e Delta Lake

```text
Streaming Source
       ↓
Spark Structured Streaming
       ↓
   Delta Lake
       ↓
 ┌─────┴─────┐
 ↓           ↓
Batch      Streaming
Analytics   Analytics
```

---

# 🧠 Mapa mental

```text
ANÁLISE EM TEMPO REAL
│
├── Processamento
│   ├── Batch
│   └── Streaming
│
├── Fontes
│   ├── Event Hubs
│   ├── IoT Hub
│   ├── Kafka
│   └── ADLS Gen2
│
├── Processamento
│   ├── Azure Stream Analytics
│   ├── Fabric Real-Time Intelligence
│   └── Spark Structured Streaming
│
├── Fabric
│   ├── Eventstream
│   ├── Eventhouse
│   ├── Real-Time Dashboard
│   ├── Activator
│   └── Real-Time Hub
│
├── Storage
│   ├── Delta Lake
│   ├── ADLS Gen2
│   ├── OneLake
│   └── Blob Storage
│
└── Consumo
    ├── Power BI
    ├── SQL
    └── Analytics
```

---

# ✅ Pontos que eu levaria para a prova

* **Batch** → dados acumulados e processados em grupo.
* **Streaming** → dados processados conforme chegam.
* **Latência** → tempo entre chegada do dado e resultado.
* **Streaming** → baixa latência.
* **Batch** → adequado para grandes volumes e análises históricas.
* **Micro-batch** → pequeno conjunto de registros processado como unidade.
* **Window** → intervalo de tempo utilizado para agregações de streaming.
* **Source** → origem do fluxo.
* **Perpetual Query** → consulta executada continuamente.
* **Sink** → destino do processamento.
* **Event Hubs** → ingestão de grandes volumes de eventos.
* **IoT Hub** → eventos de dispositivos IoT.
* **Kafka** → plataforma open source de eventos.
* **Azure Stream Analytics** → processamento de streaming como PaaS.
* **Fabric Real-Time Intelligence** → plataforma integrada de tempo real no Fabric.
* **Eventstream** → ingestão, roteamento e transformação.
* **Eventhouse** → eventos e séries temporais consultados com KQL.
* **Activator** → dispara ações baseado em condições.
* **Real-Time Hub** → catálogo central de streams.
* **Apache Spark** → processamento distribuído.
* **Structured Streaming** → streaming dentro do Spark.
* **Delta Lake** → confiabilidade, schema e suporte conjunto a batch e streaming.
* **Power BI** → visualização dos resultados em dashboards.

---

> Material organizado a partir das minhas próprias anotações durante a preparação para a certificação **Microsoft Azure Data Fundamentals (DP-900)**.

