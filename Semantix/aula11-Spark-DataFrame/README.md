# Spark - Exercícios de DataFrame

1 . Enviar o diretório local “/input/exercises-data/juros_selic” para o HDFS em “/user/aluno/<nome>/data”
  
    -- acessar o namenode
    docker exec -it namenode bash
  
    hdfs dfs -put /input/exercises-data/juros_selic/ /user/aluno/jader/data
  
    -- consultando os arquivos
    hdfs dfs -ls /user/aluno/jader/data/juros_selic

2 . Criar o DataFrame jurosDF para ler o arquivo no HDFS “/user/aluno/<nome>/data/juros_selic/juros_selic.json”
  
    -- saindo do ambiente (CTRL+D) e acessando o spark
    docker exec -it spark bash
  
    -- console spark
    spark-shell
  
    val jurosDF = spark.read.json("/user/aluno/jader/data/juros_selic/juros_selic.json")

3 . Visualizar o Schema do jurosDF
  
    jurosDF.printSchema
    
    root
    |-- data: string (nullable = true)
    |-- valor: string (nullable = true)


4 . Mostrar os 5 primeiros registros do jutosDF
  
    -- não é obrigatório usar o parêntese
    jurosDF.show(5)
  
    -- dica de usar o parâmetro false, caso tenha uma coluna diferente ele sempre mostra todo o valor
    jurosDF.show(5,false)

5 . Contar a quantidade de registros do jurosDF
  
    -- não é obrigatório usar o parêntese
    jurosDF.count()

6 . Criar o DataFrame jurosDF10 para filtrar apenas os registros com o campo “valor” maior que 10
  
    val jurosDF10 = jurosDF.where("valor > 10")
    -- será criado um dataset

7 . Salvar o DataFrame jurosDF10  como tabela Hive “<nome>.tab_juros_selic”
  
    -- para salvar usa o write
    -- tabela do Hive saveAsTable
    -- jader é o nome do banco de dados
    -- e depois do ponto o nome da tabela
    jurosDF10.write.saveAsTable("jader.tab_juros_selic")

8 . Criar o DataFrame jurosHiveDF para ler a tabela “<nome>.tab_juros_selic”
  
    -- eu poderia sair do Spark e ir direto no metastore fazer o sql no hive
    -- mas como o Spark tem acesso, vamos fazer a consulta por dentro dele
    val jurosHiveDF = spark.read.table("jader.tab_juros_selic")
    
9 . Visualizar o Schema do jurosHiveDF
  
    jurosHiveDF.printSchema

10 . Mostrar os 5 primeiros registros do jurosHiveDF
  
    jurosHiveDF.show(5)  

11 . Salvar o DataFrame jurosHiveDF no HDFS no diretório “/user/aluno/nome/data/save_juros” no formato parquet
  
    -- para formato parquet, podemos usar o parquet ou até mesmo o save
    -- o save pega o padrão e nosso ambiente já é padrão parquet
    -- a diferença aqui é que precisamos colocar o caminho completo com diretório
    -- ele não cria um diretóro automático como faz o Hive ou Sqoop
    -- outro ponto é que ele só consegue criar um diretório
    jurosHiveDF.write.parquet("/user/aluno/jader/data/save_juros")

12 . Visualizar o save_juros no HDFS
    
    -- saindo do spark (CTRL+D) e voltando ao console original
    -- conectando ao namenode
    hdfs dfs -ls -R /user/aluno/jader/data/save_juros
  
    -- o spark já salva otimizado no HDFS e no Hive
    -- particionado e comprimido

13 . Criar o DataFrame jurosHDFS para ler o diretório do “save_juros” da questão 8
  
    -- retorna ao spark shell
    -- como por padrão nosso ambiente é parquet
    -- posso fazer a leitura usando load ou parquet. O resultado é o mesmo
    val jurosHDFS = spark.read.load("/user/aluno/jader/data/save_juros")

14 . Visualizar o Schema do jurosHDFS
    
    jurosHDFS.printSchema

15 . Mostrar os 5 primeiros registros do jurosHDFS
  
    jurosHDFS.show(5)
