# Exercícios - WithColumn 1/2

1. Criar um dataframe para ler o arquivo no HDFS /user/<nome/data/juros_selic/juros_selic

        -- iniciamos dando um cat para ver o conteúdo do arquivo
        !hdfs dfs -cat /user/jader/data/juros_selic/juros_selic
    
    importando o arquivo e armazenando no dataset
    
        juros_selic = spark.read.csv("/user/jader/data/juros_selic/juros_selic", sep=";", header="true")

2. Alterar o formato do campo data para “MM/dd/yyyy”

        -- primeiro vamos visualizar alguns registros
        juros_selic.show(5)
           
    resultado:
    
        +----------+-----+
        |      data|valor|
        +----------+-----+
        |01/06/1986| 1,27|
        |01/07/1986| 1,95|
        |01/08/1986| 2,57|
        |01/09/1986| 2,94|
        |01/10/1986| 1,96|
        +----------+-----+
        only showing top 5 rows
        
    importar as functions para no Notebook
        from pyspark.sql.functions import *
        
    primeiro convertemos a coluna data para timestamp
    
        juros_selic_data_timestamp = juros_selic.withColumn("data", unix_timestamp(col("data"), "dd/MM/yyyy"))
    
    agora convertemos de timestamp para o formato desejado usando from_unixtime
    
        juros_selic_data_format_us = juros_selic_data_timestamp.withColumn("data", from_unixtime("data","MM/dd/yyyy"))
        
    visualizando o resultado
    
        juros_selic_data_format_us.show(5)
    
    resultado após a conversão
    
        +----------+-----+
        |      data|valor|
        +----------+-----+
        |06/01/1986| 1,27|
        |07/01/1986| 1,95|
        |08/01/1986| 2,57|
        |09/01/1986| 2,94|
        |10/01/1986| 1,96|
        +----------+-----+
        only showing top 5 rows

3. Com uso da função from_unixtime crie o campo “ano_unix”, com a informação do ano do campo data

        -- mesma lógica acima. Converter em timestamp e depois usamos o from_unixtime
        -- aqui executamos em uma úncia linha
        
        juros_selic_year = juros_selic.withColumn("ano_unix", from_unixtime(unix_timestamp(col("data"), "dd/MM/yyyy"),"yyyy"))
        
    visualizando o resultado
    
        juros_selic_year = juros_selic.withColumn("ano_unix", from_unixtime(unix_timestamp(col("data"), "dd/MM/yyyy"),"yyyy"))
        
    resultado
        
        +----------+-----+--------+
        |      data|valor|ano_unix|
        +----------+-----+--------+
        |01/06/1986| 1,27|    1986|
        |01/07/1986| 1,95|    1986|
        |01/08/1986| 2,57|    1986|
        |01/09/1986| 2,94|    1986|
        |01/10/1986| 1,96|    1986|
        +----------+-----+--------+
        only showing top 5 rows 

4. Com uso de substring crie o campo “ano_str”, com a informação do ano do campo data

        juros_selic_year_substring = juros_selic_year.withColumn("ano_str", substring("data",7,4 ))

    consultando
    
        juros_selic_year_substring.show(5)
        
    resultado
    
        +----------+-----+--------+-------+
        |      data|valor|ano_unix|ano_str|
        +----------+-----+--------+-------+
        |01/06/1986| 1,27|    1986|   1986|
        |01/07/1986| 1,95|    1986|   1986|
        |01/08/1986| 2,57|    1986|   1986|
        |01/09/1986| 2,94|    1986|   1986|
        |01/10/1986| 1,96|    1986|   1986|
        +----------+-----+--------+-------+
        only showing top 5 rows     

5. Com uso da função split crie o campo “ano_str_split”, com a informação do ano do campo data

        -- o split monta um array a cada "/". Já o getItem estamos pegando apenas o item específico da lista
        juros_selic_year_split = juros_selic_year_substring.withColumn("ano_str_split", split("data", "/").getItem(2))
        
    consultando
    
        juros_selic_year_split.show(5)
        
    resultado
    
        +----------+-----+--------+-------+-------------+
        |      data|valor|ano_unix|ano_str|ano_str_split|
        +----------+-----+--------+-------+-------------+
        |01/06/1986| 1,27|    1986|   1986|         1986|
        |01/07/1986| 1,95|    1986|   1986|         1986|
        |01/08/1986| 2,57|    1986|   1986|         1986|
        |01/09/1986| 2,94|    1986|   1986|         1986|
        |01/10/1986| 1,96|    1986|   1986|         1986|
        +----------+-----+--------+-------+-------------+
        only showing top 5 rows
    
    só para mostrar a diferença. O resultado se executar sem o getItem()
    
        juros_selic_year_split = juros_selic_year_substring.withColumn("ano_str_split", split("data", "/"))
    
    ficaria assim
    
        +----------+-----+--------+-------+--------------+
        |      data|valor|ano_unix|ano_str| ano_str_split|
        +----------+-----+--------+-------+--------------+
        |01/06/1986| 1,27|    1986|   1986|[01, 06, 1986]|
        |01/07/1986| 1,95|    1986|   1986|[01, 07, 1986]|
        |01/08/1986| 2,57|    1986|   1986|[01, 08, 1986]|
        |01/09/1986| 2,94|    1986|   1986|[01, 09, 1986]|
        |01/10/1986| 1,96|    1986|   1986|[01, 10, 1986]|
        +----------+-----+--------+-------+--------------+
        only showing top 5 rows

6. Salvar no hdfs /user/rodrigo/juros_selic_americano no formato CSV, incluindo o cabeçalho

        juros_selic_year_split.write.csv("/user/jader/juros_selic", header="true")
