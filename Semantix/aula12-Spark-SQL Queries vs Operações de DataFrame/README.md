# Spark - Exercícios de SQL Queries vs Operações de DataFrame

Realizar as seguintes consultas usando SQL queries e transformações de DataFrame na tabela “tab_alunos” no banco de dados <nome>
  
    -- Inicialmente acessar o cluster spark
    -- comandos estão nas aulas anteriores

1. Visualizar o id e nome dos 5 primeiros registros
  
        spark.sql("select id_discente, nome from tab_alunos limit 5").show()

        -- vamos fazer em etapas para melhor tratamento dos dados e organização
        -- primeiro salvamos em um dataframe
        val alunosHiveDF = spark.read.table("tab_alunos")

        -- agora usamos o select e o limit chamando o Dataframe criado
        alunosHiveDF.select("id_discente","nome").limit(5).show
  
2. Visualizar o id, nome e ano quando o ano de ingresso for maior ou igual a 2018
  
        spark.sql("select id_discente, nome, ano_ingresso from tab_alunos where ano_ingresso >= 2018").show()
  
        --começa a vantagem de salvar em Dataframe. Agora só chamamos o Dataframe criado anteriormente
        alunosHiveDF.select("id_discente","nome","ano_ingresso").where("ano_ingresso >= 2018").show

3. Visualizar por ordem alfabética do nome o id, nome e ano quando o ano de ingresso for maior ou igual a 2018
  
        spark.sql("select id_discente, nome, ano_ingresso from tab_alunos where ano_ingresso >= 2018 order by nome desc").show()
  
        alunosHiveDF.select("id_discente","nome","ano_ingresso").where("ano_ingresso >= 2018").orderBy($"nome".desc).show()

4. Contar a quantidade de registros do item anterior
  
        park.sql("select count(id_discente) from tab_alunos where ano_ingresso >= 2018").show()
        +------------------+
        |count(id_discente)|
        +------------------+
        |              4266|
        +------------------+
                                                           
  
        alunosHiveDF.select("id_discente","nome","ano_ingresso").where("ano_ingresso >= 2018").orderBy($"nome".desc).count()
        res29: Long = 4266    

