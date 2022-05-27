# Sqoop - Importação BD Employees

1 . Pesquisar os 10 primeiros registros da tabela employees do banco de dados employees

      -- começa acessando o namenode
      docker exec -it namenode bash
      
      -- executando a query no Sqoop
      sqoop eval --connect jdbc:mysql://database/employees --username root --password secret --query "select * from employees limit 10"

2 . Realizar as importações referentes a tabela employees e para validar cada questão,  é necessário visualizar no HDFS*

* A) Importar a tabela employees, no warehouse  /user/hive/warehouse/db_test_a
   
      -- teste
      sqoop import --table employees --connect jdbc:mysql://database/employees --username root --password secret --warehouse-dir /user/hive/warehouse/db_test_a 
      
      -- visualizar os dados no HDFS (confereência)
      hdfs dfs -ls /user/hive/warehouse/db_test_a
      
      -- repare que ele dividiu em quatro arquivos
      hdfs dfs -ls /user/hive/warehouse/db_test_a/employees
      
      -- vamos ler o primeiro arquivo
      hdfs dfs -cat /user/hive/warehouse/db_test_a/employees/part-m-00000 | head -n 5
      
      
* b) Importar todos os funcionários do gênero masculino, no warehouse  /user/hive/warehouse/db_test_b

      sqoop import --table employees --connect jdbc:mysql://database/employees --username root --password secret --where "gender='M'" --warehouse-dir /user/hive/warehouse/db_test_b
      
      -- se quiser fazer as leituras de conferência, pode repetir os comandos HDFS do exercício 2


* c) importar o primeiro e o último nome dos funcionários com os campos separados por tabulação, no warehouse  /user/hive/warehouse/db_test_c
      
      sqoop import --table employees --connect jdbc:mysql://database/employees --username root --password secret --columns "first_name,last_name" --fields-terminated-by '\t' --warehouse-dir /user/hive/warehouse/db_test_c

  
* d) Importar o primeiro e o último nome dos funcionários com as linhas separadas por “ : ” e salvar no mesmo diretório da questão 2.C

      -- como já existe o diretório, se tentarmos salvar no mesmo destino vai gerar erro
      -- a tomada de decisão pode ser de substituir os dados ou adicionar
      -- para adicionar, ao fim, podemos usar o -apend
      -- mas como o formato dos dados é  diferente, a opção foi de remover os dados anteriores usando o -delete
      
      sqoop import --table employees --connect jdbc:mysql://database/employees --username root --password secret --columns "first_name,last_name" --lines-terminated-by ':' --warehouse-dir /user/hive/warehouse/db_test_c -delete-target-dir

Dica para visualizar no HDFS:

      $ hdfs dfs -cat /.../db_test/nomeTabela/part-m-00000 | head -n 5
