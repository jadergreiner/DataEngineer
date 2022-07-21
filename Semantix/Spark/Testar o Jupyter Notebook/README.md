# Cluster de Big Data para o curso e treinamento

1. Instalação do docker e docker-compose.

2. Executar os seguintes comandos, para baixar as imagens do Cluster de Big Data:

        git clone https://github.com/rodrigo-reboucas/docker-bigdata.git spark

        cd spark

        docker-compose –f docker-compose-parcial.yml pull

3. Iniciar o cluster Hadoop através do docker-compose

        docker-compose –f docker-compose-parcial.yml up -d
      
4. Listas as imagens em execução

5. Verificar os logs dos containers do docker-compose em execução

6. Verificar os logs do container jupyter-spark

7. Acessar pelo browser o Jupyter, através do link:

        http://localhost:8889
        
# Exercícios – Testar o Jupyter Notebook

1. Criar o arquivo do notebook com o nome teste_spark.ipynb

2. Obter as informações da sessão de spark (spark)

        spark

3. Obter as informações do contexto do spark (sc)

        sc

4. Setar o log como INFO.

        spark.sparkContext.setLogLevel("INFO")

5. Visualizar todos os banco de dados com o catalog

        spark.catalog.listDatabases()

6. Ler os dados "hdfs://namenode:8020/user/rodrigo/data/juros_selic/juros_selic.json“ com uso de Dataframe

        leitura_juros = spark.read.json("hdfs://namenode:8020/user/jader/data/juros_selic/juros_selic.json")
        leitura_juros.show(5)
        
Uma observação. Como o namenode já está mapeado em nosso cluster, poderia ser feita a leitura assim.

        leitura_juros = spark.read.json("hdfs:///user/jader/data/juros_selic/juros_selic.json")
        
Outra característica, nosso ambiente está como Default o HDFS. Poderia ser assim também

        leitura_juros = spark.read.json("/user/jader/data/juros_selic/juros_selic.json")

7. Salvar o Dataframe como juros no formato de tabela Hive

        leitura_juros.write.saveAsTable("juros")
        
Em nosso ambiente não é encessário especificar todo o caminho do diretório hive, pois já configurado em nosso cluster.

8. Visualizar todas as tabelas com o catalog

        spark.catalog.listTables()

9. Visualizar no hdfs o formato e compressão que está a tabela juros do Hive

        -- conseguimos acessar aos arquivos diretamente pelo Pyspark usando "!" na frente do comando. Usa comandos Linux
        !hdfs dfs -ls /user/hive/warehouse/juros

10. Ler e visualizar os dados da tabela juros, com uso de Dataframe no formato de Tabela Hive

        spark.read.table("juros").show(5)

11. Ler e visualizar os dados da tabela juros , com uso de Dataframe no formato Parquet

        spark.read.parquet("/user/hive/warehouse/juros/").show(5)
