# Sqoop - Importação para o Hive e Exportação - BD Employees

 
1 . Importar a tabela employees.titles do MySQL para o diretório /user/aluno/<nome>/data com 1 mapeador.

    sqoop import --table titles --connect jdbc:mysql://database/employees --username root --password secret --warehouse-dir /user/aluno/jader/data -m 1
 
    -- conferir a importação no HDFS
    hdfs dfs -ls -h -R /user/aluno/jader/data/titles
 
2 . Importar a tabela employees.titles do MySQL para uma tabela Hive no banco de dados seu nome com 1 mapeador.
   
    sqoop import --table titles --connect jdbc:mysql://database/employees --username root --password secret -m 1 --hive-import --hive-table jader.titles
 
    - conferindo os dados no HDFS
    hdfs dfs -ls /user/hive/warehouse/jader.db

3 . Selecionar os 10 primeiros registros da tabela titles no Hive.
 
    -- poderíamos dar um cat no arquivo. Mas não saberíamos se o Hive está interpretando como uma tabela
    hdfs dfs -cat /user/hive/warehouse/jader.db/titles/part-m-00000 | head -n 10
 
    -- vamos sair e acessar o hive-server
    docker exec -it hive-server bash
 
    -- conectando ao beeline
    beeline -u jdbc:hive2://localhost:10000
 
    -- setando o banco jader
    use jader;
 
    -- query consultando os 10 primeiros registros da tabela titles
    select * from titles limit 10;

4 . Deletar os registros da tabela employees.titles do MySQL e verificar se foram apagados, através do Sqoop
 
    -- sair do hive-server e conectar ao namenode
    -- query para verificar os dados no employees
    sqoop eval --connect jdbc:mysql://database/employees --username root --password secret --query "select * from titles limit 10"
 
    -- deletantanto os registros - (truncate table)
    sqoop eval --connect jdbc:mysql://database/employees --username root --password secret --query "truncate table titles" 
 
    -- consultando se os dados foram apagados
    sqoop eval --connect jdbc:mysql://database/employees --username root --password secret --query "select * from titles limit 10"
    
5 . Exportar os dados do diretório /user/hive/warehouse/<nome>.db/data/titles para a tabela do MySQL  employees.titles.
 
    -- estaremos exportando os dados do exercício 1 para o RDBMS MySQL
    sqoop export --table titles --connect jdbc:mysql://database/employees --username root --password secret --export-dir /user/aluno/jader/data/titles
 
6 . Selecionar os 10 primeiros registros registros da tabela employees.titles do MySQL.
   
    -- repetir a query
    sqoop eval --connect jdbc:mysql://database/employees --username root --password secret --query "select * from titles limit 10"
