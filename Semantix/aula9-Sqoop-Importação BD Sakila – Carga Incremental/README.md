# Sqoop - Importação BD Sakila – Carga Incremental

Realizar com uso do MySQL

1 . Criar a tabela cp_rental_append, contendo a cópia da tabela rental com os campos rental_id e rental_date

    create table cp_rental_append select rental_id, rental_date from rental;

2 . Criar a tabela cp_rental_id e cp_rental_date, contendo a cópia da tabela cp_rental_append

    create table cp_rental_id select * from cp_rental_append;
    create table cp_rental_date select * from cp_rental_append;

Realizar com uso do Sqoop - Importações no warehouse /user/hive/warehouse/db_test3 e visualizar no HDFS

    -- saindo do MySQL e do cluster database
    -- conectando ao cluster namenode para usar o Sqoop

3 . Importar as tabelas cp_rental_append, cp_rental_id e cp_rental_date com 1 mapeador

       sqoop import --table cp_rental_append --connect jdbc:mysql://database/sakila --username root --password secret -m 1 --warehouse-dir /user/hive/warehouse/db_test3

       sqoop import --table cp_rental_id --connect jdbc:mysql://database/sakila --username root --password secret -m 1 --warehouse-dir /user/hive/warehouse/db_test3

       sqoop import --table cp_rental_date --connect jdbc:mysql://database/sakila --username root --password secret -m 1 --warehouse-dir /user/hive/warehouse/db_test3

       -- consultando os dados no HDFS
       hdfs dfs -ls -h -R /user/hive/warehouse/db_test3

Realizar com uso do MySQL

4 . Executar o sql /db-sql/sakila/insert_rental.sql no container do database

    $ docker exec -it database bash

    $ cd /db-sql/sakila

    -- verificar o script
    cat insert_rental.sql

    $ mysql -psecret < insert_rental.sql
    
    -- se ocorrer erro, verificar e editar o arquivo no vim ou nano
    -- no meu caso, o select est
 

Realizar com uso do Sqoop - Importações no warehouse /user/hive/warehouse/db_test3 e visualizar no HDFS

5 . Atualizar a tabela cp_rental_append no HDFS anexando os novos arquivos

    -- acessar o namenode
    sqoop import --table cp_rental_append --connect jdbc:mysql://database/sakila --username root --password secret --warehouse-dir /user/hive/warehouse/db_test3 -m 1 --append

6 . Atualizar a tabela cp_rental_id no HDFS de acordo com o último registro de rental_id, adicionando apenas os novos dados.

   -- primeiramente vamos ver os últimos registros
   sqoop eval --connect jdbc:mysql://database/sakila --username root --password secret --query "select * from cp_rental_append order by rental_id desc limit 10"
   
    -- idenficado como último registro
      rental_id   | rental_date         | 
     -------------------------------------
     | 16049       | 2005-08-23 22:50:12.0 |
     
     sqoop import --table cp_rental_id --connect jdbc:mysql://database/sakila --username root --password secret --warehouse-dir /user/hive/warehouse/db_test3 -m 1 --incremental append --check-column rental_id --last-value 16049


7 . Atualizar a tabela cp_rental_date no HDFS de acordo com o último registro de rental_date, atualizando os registros a partir desta data.

    sqoop import --table cp_rental_date --connect jdbc:mysql://database/sakila --username root --password secret --warehouse-dir /user/hive/warehouse/db_test3 -m 1 --incremental lastmodified --merge-key rental_id --check-column rental_date --last-value '2005-08-23 22:50:12.0'
   

   -- verificando no HDFS
   hdfs dfs -ls -h -R /user/hive/warehouse/db_test3
   
   -- comparando a difereça. Quando usamos o append, ele "duplicou" o arquivo. Ele adiciona o novo arquivo e monta um novo arquivo junto com o anterior.

