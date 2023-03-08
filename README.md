# PROJETO FINAL 2 - FORMAÇÃO ENGENHEIRO DE DADOS - UDEMY

### Tópicos do Projeto

:small_blue_diamond: [Enunciado do projeto](#enunciado-do-projeto)

:small_blue_diamond: [Etapas](#etapas)

:small_blue_diamond: [Arquitetura dos dados](#arquitetura-dos-dados)

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
  * Criar um crawler no Glue Data Catalog
  * Criar um job ETL no Glue para transformar os dados gerados de JSON para Parquet
  * Criar um outro crawler no Glue para inferir o schema dos dados transformados
  * Criar consultas no Athena


## Arquitetura dos dados
Esse é um projeto end-to-end, desde a produção dos dados até a disponibilização dos mesmos para consulta, usando os serviços da AWS. A arquitetura completa pode ser visualizada a seguir:



## Pré requisitos
Para executar esse projeto é necessário ter o Jupyter Notebook instalado localmente ou uma conta Google para acessar o [Colab](https://colab.research.google.com/) e uma conta na nuvem AWS.

## Execução

### Criar um Data Stream no Kinesis Data Stream

Essa primeira etapa consiste em acessar o serviço Kinesis e gerar fluxos de dados (data streams) de nome *Stream2*, por exemplo, que será usado pela aplicação python geradora de dados para transmitir os dados como streaming. 

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
 * type - o tipo de dado, podendo ser *powerfactor*, *temperature* ou *hydraulicpressure*
 * timestamp - data e hora que o registro foi gerado
 
 Para transmitir os dados para o data stream *Stream2* criado no Kinesis Data Stream, deve-se, primeiramente, iniciar uma conexão cliente com o Kinesis através da biblioteca boto3. Em seguida, deve-se preencher os campos *aws_access_key_id* e *aws_secret_access_key* com a chave secreta gerada na sua conta da AWS, e *region_name* com o nome da região onde o bucket da etapa anterior foi criado. Além disso, precisa também especificar o campo *StreamName* com o nome do data scream criado na primeira etapa e o campo *PartitionKey* com o valor da chave que será usada para identificar o shard do Kinesis Data Stream para o qual os registros serão enviados.
 
 
### Criar um bucket no S3
O terceiro passo consiste em acessar o serviço S3 e criar um bucket de nome *projeto2-aws-engdados*, por exemplo, para receber os dados vindos do Kinesis Data Firehouse, conforme mostra a imagem abaixo:

![bucket para dados da aplicação python](https://user-images.githubusercontent.com/83982164/223613153-6dc22d18-523d-45e1-96fb-fc26be1c9905.jpg)


### Criar um Kinesis Data Firehouse
A quarta etapa é criar um fluxo de entrega no Kinesis Data Firehouse que entregará os dados particionado por ano, mês e dia ao bucket no S3. Ao criar o fluxo, precisa-se configurar a origem e o destino dos dados como sendo, respectivamente, o Kinesis Data Stream e o bucket criado na etapa anterior. Precisa-se também estabelecer o tempo de latência (da entrega dos dados ao bucket) como 60 segundos. A figura abaixo mostra o Data Firehouse gerado:

![kinesis firehose](https://user-images.githubusercontent.com/83982164/223737642-cbe54edc-e5d7-48b5-8362-f8dd4bf1e21c.jpg)


### Criar uma database no Glue Data Catalog
Na quinta etapa, é necessário acessar o Glue Data Catalog e criar uma database, que é repositório de dados, no qual ficarão armazenadas as tabelas que tiveram o seu schema inferido pelo crawler, que será gerado no próximo passo. Nesse projeto foi criada a database *dados_sensores*, conforme mostra a imagem abaixo:

![image](https://user-images.githubusercontent.com/83982164/223740858-51740425-a288-4ad3-9187-ce09e2850bee.png)


### Criar um crawler no Glue Data Catalog
A sexta etapa consiste em criar um crawler no Glue Data Catalog, que inferirá o schema dos objetos armazenados no bucket S3. No caso, esses objetos são os dados gerados pelas aplicações python armazenados no bucket *projeto2-aws-engdados*, transformando-os em tabelas. Ao criar um crawler, precisa-se associar os dados a uma database, que no caso será a *dados_sensores*, gerada na etapa anterior. Além disso, é precisa-se configurar uma IAM role que tenha acesso ao bucket S3. O crawler gerado é mostrado na imagem abaixo:

![crawler_dados_sensores_atualizado](https://user-images.githubusercontent.com/83982164/223744714-7730642a-7758-4d4d-b7f4-cf0ef3ff0518.jpg)

Ao executar o crawler, é criada a tabela *projeto2-aws-engdados*, a partir do bucket de mesmo nome, associada a database *dados_sensores, conforme pode ser visto na figura a seguir:

![table_1](https://user-images.githubusercontent.com/83982164/223743465-74bc9701-7057-45be-bce7-7e6632a2eb32.jpg)


### Criar um job ETL no Glue


### Criar um outro crawler no Glue


### Criar consultas no Athena



OBS: Os serviços Kinesis Data Stream, Kinesis Data Firehouse, Glue crawler e Glue Jobs são pagos e podem gerar custos!
