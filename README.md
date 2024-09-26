# Big Data Processing
Big Data Processing- Mackenzie

# MBA Engenharia de Dados

# Grupo:
| Nomes              | RA |
| -------------     | ------------- |
| Aline Couto       | 10206399   |
| Cristian Barros   | 10444616  |
| Vinícius Batista  | 10444150   |
| Alex Assis        | 10444718  |
| Renato Mori       | 10444622  |



# Introdução
Este guia fornece instruções detalhadas sobre como configurar e executar o Apache Spark no Ubuntu. Ele abrange desde o download e instalação até a execução de um script de exemplo utilizando PySpark.

# Pré-requisitos
Ubuntu instalado e atualizado
Acesso ao terminal com permissões de superusuário
Java instalado (Apache Spark é baseado em Java)

# Passo a Passo
* 1. Download do Pacote Spark
Baixe o pacote do Apache Spark usando o comando wget:

`wget https://dlcdn.apache.org/spark/spark-3.4.1/spark-3.4.1-bin-hadoop3.tgz`

* 2. Descompactar o Pacote
Descompacte o arquivo baixado:

`tar -xvf spark-3.4.1-bin-hadoop3.tgz`

* 3. Mover o Arquivo para o Diretório /opt
Mova o diretório descompactado para /opt:

`sudo mv spark-3.4.1-bin-hadoop3 /opt/spark`

* 4. Subir o Serviço Master
Inicie o serviço master do Spark:

`/opt/spark/sbin/start-master.sh`

* 5. Subir o Serviço Worker
Inicie o serviço worker do Spark:

`opt/spark/sbin/start-worker.sh spark://localhost:7077`

* 6. Criar Diretório do Projeto
Crie um diretório para o projeto:

`mkdir projeto_quarta`

* 7. Criar o Script mapreduce.py
Crie o script mapreduce.py no diretório projeto_quarta com o seguinte conteúdo:

```
#Python
```

```
-*- coding: utf-8 -*-
import sys
from pyspark import SparkContext, SparkConf
from pyspark.sql import SQLContext
from pyspark.sql import SparkSession
from pyspark.sql import functions as F

master_url = "spark://renato-Latitude-5400:7077"`

1. Criar uma SparkSession
`spark = SparkSession.builder \
    .appName("MapReduceNumerosCSV") \
    .master(master_url) \
    .getOrCreate()`

2. Carregar o arquivo CSV em um DataFrame
df = spark.read.csv("/home/renato/Downloads/projeto_quarta/dataset.csv", header=True, inferSchema=True)`

3. Remover valores NaN da coluna numérica
df_clean = df.dropna(subset=["Low"])`

4. Exemplo de operação Map (selecionar a coluna numérica)
df_map = df_clean.select("Low")`

5. Exemplo de operação Reduce (soma todos os valores da coluna numérica)
df_reduce = df_map.agg(F.sum("Low").alias("soma_total"))`

6. Exemplo de operação Reduce (calcular a média dos valores da coluna numérica)
df_reduce = df_map.agg(F.avg("Low").alias("media_total"))`

7. Mostrar o resultado da soma
df_reduce.show()`

8. Guardar a saída em um arquivo CSV
df_reduce.coalesce(1).write.csv("/home/renato/Downloads/projeto_quarta/saida", header=True)`

9. Encerrar a SparkSession
spark.stop()`
```

* 8. Submeter o Script no Spark
Execute o script mapreduce.py utilizando o comando spark-submit:

`spark-submit projeto_quarta/mapreduce.py`















![Screenshot of a comment on a GitHub issue showing an image, added in the Markdown, of an Octocat smiling and raising a tentacle.](https://myoctocat.com/assets/images/base-octocat.svg)


