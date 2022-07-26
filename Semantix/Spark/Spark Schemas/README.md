# Exercício – Spark Schemas

1. Criar o DataFrame names_us_sem_schema para ler os arquivos no HDFS “/user/<nome>/data/names”

        -- Inicialmente vamos ler os dados no HSFS
        !hdfs dfs -ls /user/jader/data/names/
        -- veja os arquivos, podemos ler o conteúdo de um  arquivo com o cat
        !hdfs dfs -cat /user/jader/data/names/yob1880.txt
        
    Realizando a leitura dos arquivos no diretório.
    
        names_us_sem_schema = spark.read.csv("/user/jader/data/names")
    

2. Visualizar o Schema e os 5 primeiros registos do names_us_sem_schema

        print(names_us_sem_schema.printSchema())
        names_us_sem_schema.show(5)

3. Criar o DataFrame names_us para ler os arquivos no HDFS “/user/<nome>/data/names” com o seguinte schema:

nome: String
sexo: String
quantidade: Inteiro

        -- primeiro passo vamos importar a biblioteca sql para inferir schemas
        from pyspark.sql.types import *
        
        -- aqui criamos uma lista com o Schema
        estrutura_lista = [
            StructField("nome", StringType()),
            StructField("sexo", StringType()),
            StructField("quantidade", IntegerType())
        ]

        -- aqui estamos inferindo o schema
        schema_names = StructType(estrutura_lista)
        
        -- observação. Não é obrigatório executar em dois passos. Poderia ter inserido o schema com o dado da lista diretamente no StructType
        
        -- para inserir os dados no DF com Schema, pode fazer no mesmo comando de leitura dos dados. O read_csv já dá suporte para schemas
        names_us = spark.read.csv("/user/jader/data/names",schema=schema_names)
        
4. Visualizar o Schema e os 5 primeiros registos do names_us

        print(names_us.printSchema())
        names_us.show(5)

5. Salvar o DataFrame names_us no formato orc no hdfs “/user/<nome>/names_us_orc”

        names_us.write.orc("/user/jader/names_us_orc")
        
        -- conferir os dados no HDFS[
        !hdfs dfs -ls /user/jader/names_us_orc
