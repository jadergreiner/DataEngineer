# Spark - Exercícios da API Catalog

Realizar os exercícios usando a API Catalog.

    --acessar o ambiente do Spark
    -- as orientações estão nas aulas anteriores

1 . Visualizar todos os banco de dados

    -- uma primeira dica: Quando digitamos spark. e damos um tab, ele vai mostrando todos os comandos disponíveis. 
    -- essa dica do tab vale a qualquer momento do uso
    spark.catalog.listDatabases.show(false)

2 . Definir o banco de dados “seu-nome” como principal

    spark.catalog.setCurrentDatabase("jader")

3 . Visualizar todas as tabelas do banco de dados “seu-nome”

    spark.catalog.listTables.show(false)

4 . Visualizar as colunas da tabela tab_alunos

    spark.catalog.listColumns("tab_alunos").show(false)

5 .  Visualizar os 10 primeiros registos da tabela "tab_alunos" com uso do spark.sql

    -- para comparar os dados, pode ver primeiro no read table
    spark.read.table("tab_alunos").show(10)
    
    --agora com SQL
    spark.sql("select * from tab_alunos limit 10").show()

