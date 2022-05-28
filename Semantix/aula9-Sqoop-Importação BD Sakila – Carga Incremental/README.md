# Sqoop - Importação BD Sakila – Carga Incremental

Realizar com uso do MySQL

1 . Criar a tabela cp_rental_append, contendo a cópia da tabela rental com os campos rental_id e rental_date

2 . Criar a tabela cp_rental_id e cp_rental_date, contendo a cópia da tabela cp_rental_append

 

Realizar com uso do Sqoop - Importações no warehouse /user/hive/warehouse/db_test3 e visualizar no HDFS

3 . Importar as tabelas cp_rental_append, cp_rental_id e cp_rental_date com 1 mapeador

 

Realizar com uso do MySQL

4 . Executar o sql /db-sql/sakila/insert_rental.sql no container do database

$ docker exec -it database bash

$ cd /db-sql/sakila

$ mysql -psecret < insert_rental.sql

 

Realizar com uso do Sqoop - Importações no warehouse /user/hive/warehouse/db_test3 e visualizar no HDFS

5 . Atualizar a tabela cp_rental_append no HDFS anexando os novos arquivos

6 . Atualizar a tabela cp_rental_id no HDFS de acordo com o último registro de rental_id, adicionando apenas os novos dados.

7 . Atualizar a tabela cp_rental_date no HDFS de acordo com o último registro de rental_date, atualizando os registros a partir desta data.
