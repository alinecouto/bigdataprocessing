# Big Data Processing
Big Data Processing- Mackenzie

MBA Engenharia de Dados

# Grupo:
| Nomes              | RA |
| -------------     | ------------- |
| Aline Couto       | 10206399   |
| Cristian Barros   | 10444616  |
| Vinícius Batista  | 10444150   |
| Alex Assis        | 10444718  |
| Renato Mori       | 10444622  |



_________________________________________

para subir o spark no Ubuntu
Download do pacotewget https://dlcdn.apache.org/spark/spark-3.4.1/spark-3.4.1-bin-hadoop3.tgzDescompactei tar -xvf spark-3.5.3-bin-hadoop3.tgz Movi o arquivo para o opt sudo mv spark-3.5.3-bin-hadoop3 /opt/sparkSubir o serviço master /opt/spark/sbin/start-slave.sh Subir o serviço slave 1421 /opt/spark/sbin/start-worker.sh spark://localhost:7077Criei uma pastamkdir projeto_quartaCriei o script mapreduce.py e coloquei no diretorio projeto_quarta# -*- coding: utf-8 -*-import sysfrom pyspark import SparkContext, SparkConffrom pyspark.sql import SQLContextfrom pyspark.sql import SparkSessionfrom pyspark.sql import functions as Fmaster_url = "spark://renato-Latitude-5400:7077"# 1. Criar uma SparkSessionspark = SparkSession.builder \ .appName("MapReduceNumerosCSV") \ .master(master_url)\ .getOrCreate()# 2. Carregar o arquivo CSV em um DataFramedf = spark.read.csv("/home/renato/Downloads/projeto_quarta/dataset.csv", header=True, inferSchema=True)# 3. Remover valores NaN da coluna numéricadf_clean = df.dropna(subset=["Low"])# 4. Exemplo de operação Map (selecionar a coluna numérica)df_map = df_clean.select("Low")# 5. Exemplo de operação Reduce (soma todos os valores da coluna numérica)#df_reduce = df_map.agg(F.sum("Low").alias("soma_total"))# 6. Exemplo de operação Reduce (calcular a média dos valores da coluna numérica)df_reduce = df_map.agg(F.avg("Low").alias("media_total"))# 7. Mostrar o resultado da somadf_reduce.show()# 8. Guardar a saída em um arquivo CSVdf_reduce.coalesce(1).write.csv("/home/renato/Downloads/projeto_quarta/saida", header=True)# 9. Encerrar a SparkSessionspark.stop()E submetir ele no Spark com o comandospark-submit mapreduce.py
