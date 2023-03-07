# PROJETO FINAL 2 - FORMAÇÃO ENGENHEIRO DE DADOS - UDEMY

### Tópicos do Projeto

:small_blue_diamond: [Enunciado do projeto](#enunciado-do-projeto)

:small_blue_diamond: [Etapas](#etapas)

:small_blue_diamond: [Pré-requisitos](#pré-requisitos)

:small_blue_diamond: [Execução](#execução)


## Enunciado do projeto
Este projeto consiste na criação de uma solução que simula um Parque Eólico com a produção de dados de sensores por meio de aplicações Python usando os serviços da AWS. 
O objetivo é monitorar os dados produzidos e ver se correspondem com o esperado, de modo a garantir a qualidade da produção de energia no Parque Eólico. 

## Etapas
O projeto consiste nos seguintes passos:
  * Criar um Data Stream no Kinesis Data Stream
  * Criar aplicações Python para gerar os dados
  * Criar um bucket no S3 para receber os dados
  * Criar um Kinesis Data Firehouse para entregar os dados
  * Criar uma database no Glue Data Catalog
  * Criar um crawler no Glue 
  * Criar um job ETL no Glue para transformar os dados gerados de JSON para Parquet
  * Criar um outro crawler no Glue para inferir o schema dos dados transformados
  * Criar consultas no Athena


## Pré requisitos
Para executar esse projeto é necessário ter o Jupyter Notebook instalado localmente ou uma conta Google para acessar o Google [Colab](https://colab.research.google.com/) e uma conta na nuvem AWS.

## Execução

### Criar um Data Stream No Kinesis Data Stream

Essa primeira etapa consiste em acessar o serviço Kinesis e gerar fluxos de dados (data streams) de nome "Stream2", por exemplo, que será usado pela aplicação python geradora de dados para transmitir os dados como streaming. 

A imagem abaixo demonstra o fluxo de dados criado.

![kinesis data stream](https://user-images.githubusercontent.com/83982164/223455586-30472590-c2f9-494b-b255-e0f795fdccba.jpg)

### Criar Aplicações Python

Nessa segunda etapa, geram-se as aplicações python que simulam os sensores de um parque eólico e que produzem os dados que serão, posteriormente, usados pelos serviços da AWS.
São criadas 3 aplicações python, simulando 3 sensores conforme abaixo:
 * Sensor de fator de potência gerando potências em torno de 1
 * Sensor de temperatura gerando temperaturas em torno de 23°C
 * Sensor de pressão hidráulica gerando pressão em torno de 70 BAR

As aplicações produzem dados a cada 10 segundos no formato JSON contendo os seguintes campos:
 * id - identificador do registro
 * data - o dado em si
 * type - o tipo de dado, podendo ser 'powerfactor', 'temperature' ou 'hydraulicpressure'
 * timestamp - data e hora que o registro foi gerado
 
### Criar um bucket no S3
O terceiro passo consiste em acessar o serviço S3 e criar um bucket para receber os dados vindos do Kinesis Data Firehouse, conforme mostra a image abaixo:





### Criar um Kinesis Data Firehouse
A quarta etapa é criar um stream de entrega 


### Criar uma database no Glue Data Catalog


### Criar um crawler no Glue 

### Criar um job ETL no Glue


### Criar um outro crawler no Glue


### Criar consultas no Athena



OBS: Os serviços Kinesis Data Stream, Kinesis Data Firehouse, Glue crawler e Glue Jobs são pagos e podem gerar custos!
