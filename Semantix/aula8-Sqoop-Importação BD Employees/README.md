# Sqoop - Importação BD Employees

1 . Pesquisar os 10 primeiros registros da tabela employees do banco de dados employees

2 . Realizar as importações referentes a tabela employees e para validar cada questão,  é necessário visualizar no HDFS*

* A) Importar a tabela employees, no warehouse  /user/hive/warehouse/db_test_a
   
      -- teste
      selec
    
  * b) Importar todos os funcionários do gênero masculino, no warehouse  /user/hive/warehouse/db_test_b
  * c) importar o primeiro e o último nome dos funcionários com os campos separados por tabulação, no warehouse  /user/hive/warehouse/db_test_c
  * d) Importar o primeiro e o último nome dos funcionários com as linhas separadas por “ : ” e salvar no mesmo diretório da questão 2.C

Dica para visualizar no HDFS:

      $ hdfs dfs -cat /.../db_test/nomeTabela/part-m-00000 | head -n 5
