# Exercícios - Dataset com DataFrame

    -- estes exercícios serão executados no terminal com Spark Shell
    -- Dataset tem que rodar em Scala ou Java
    
    -- acesso ao ambiente
    docker exec -it jupyter-spark bash
    
    - acessar o spark-shell
    spark-shell
    

1. Criar o DataFrame names_us para ler os arquivos no HDFS “/user/<nome>/data/names”

        scala> val names_us = spark.read.csv("/user/jader/data/names")

2. Visualizar o Schema do names_us

        names_us.printSchema
        
      -- resultado
      
        root
        |-- _c0: string (nullable = true)
        |-- _c1: string (nullable = true)
        |-- _c2: string (nullable = true)


3. Mostras os 5 primeiros registros do names_us

        scala> names_us.show(5)

4. Criar um case class Nascimento para os dados do names_us

        scala> case class Nascimento(nome: String, sexo: String, quantidade: Int)

5. Criar o Dataset names_ds para ler os dados do HDFS “/user/<nome>/data/names”, com uso do case class Nascimento

        -- primeiro importar o Encoders para inferir Schema 
        scala> import org.apache.spark.sql.Encoders
        
        -- crindo o schema
        scala> val schema_names = Encoders.product[Nascimento].schema
        
        -- imoportando e associoando ao schema
        val names_ds = spark.read.schema(schema_names).csv("/user/jader/data/names").as[Nascimento]

6. Visualizar o Schema do names_ds

        scala> names_ds.printSchema
        
    -- resultado
    
        root
        |-- nome: string (nullable = true)
        |-- sexo: string (nullable = true)
        |-- quantidade: integer (nullable = true)


7. Mostras os 5 primeiros registros do names_ds

        names_ds.show(5)
        
    -- resultado
    
        +--------+----+----------+
        |    nome|sexo|quantidade|
        +--------+----+----------+
        |    Emma|   F|     18809|
        |Isabella|   F|     18612|
        |   Emily|   F|     17429|
        |  Olivia|   F|     17078|
        |     Ava|   F|     17035|
        +--------+----+----------+
        only showing top 5 rows


8. Salvar o Dataset names_ds no hdfs “/user/<nome>/ names_us_parquet” no formato parquet com compressão snappy

        scala> names_ds.write.save("/user/jader/names_us_parquet")
