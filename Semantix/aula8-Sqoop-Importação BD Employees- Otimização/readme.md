# Sqoop - Importação BD Employees- Otimização

Realizar com uso do MySQL

    -- iniciamos conectando ao cluster database
    docker exec -it database bash
    
    -- conectando ao MySQL
    -- usuário é root, então não vou informar e a senha é secret
    mysql -psecret

1 . Criar a tabela cp_titles_date, contendo a cópia da tabela titles com os campos title e to_date

    -- como o enunciado do exercício pede, o banco é employees
    use employees;
    
    -- conferindo as tabelas
    show tables;
    
    -- consultando os dados da tabela title
    select * from titles limit 10;
    
    -- criando a tabela cp_titles_date
    create table cp_titles_date select title, to_date from titles;

2 . Pesquisar os 15 primeiros registros da tabela cp_titles_date

    select * from cp_titles_date limit 15;

3 . Alterar os registros do campo to_date para null da tabela cp_titles_date, quando o título for igual a Staff

    update cp_titles_date set to_date = NULL where title = 'Staff'
    
    -- conferindo os dados nulos
    select * from cp_titles_date where to_date is null limit 10;
    
    -- conferindo os dados não nulos
    select * from cp_titles_date where to_date is not null limit 10;

Realizar com uso do Sqoop - Importações no warehouse /user/hive/warehouse/db_test_<numero_questao> e visualizar no HDFS

    -- saindo do MySQL e conectando ao namenode para usar o Sqoop
    CTRL + D (2x)
    docker exex -it namenode bash
    
4 . Importar a tabela titles com 8 mapeadores no formato parquet

    sqoop import --table titles --connect jdbc:mysql://database/employees --username root --password secret -m 8 --as-parquetfile -warehouse-dir /user/hive/warehouse/db_test2_4
    -- conferindo no HDFS
    hdfs dfs -ls -h /user/hive/warehouse/db_test2_4/titles

5 . Importar a tabela titles com 8 mapeadores no formato parquet e compressão snappy

    sqoop import --table titles --connect jdbc:mysql://database/employees --username root --password secret -m 8 --as-parquetfile -warehouse-dir /user/hive/warehouse/db_test2_5 --compress --compression-codec org.apache.hadoop.io.compress.SnappyCodec
    
     -- conferindo no HDFS
    hdfs dfs -ls -h /user/hive/warehouse/db_test2_5/titles

6 . Importar a tabela cp_titles_date com 4 mapeadores (erro)

    sqoop import --table cp_titles_date --connect jdbc:mysql://database/employees --username root --password secret -m 4 --as-parquetfile -warehouse-dir /user/hive/warehouse/db_test2_6    
  
    -- vai gerar erro por que não tem primary key, segurindo especificar um campo de split ou apenas 1 mapeador
    sqoop import --table cp_titles_date --connect jdbc:mysql://database/employees --username root --password secret -m 1 -warehouse-dir /user/hive/warehouse/db_test2_6

Importar a tabela cp_titles_date com 4 mapeadores divididos pelo campo título no warehouse /user/hive/warehouse/db_test2_title

    -- observar que foi necessário incluir um parâmetro após o import para permitir um a coluna text como split
    sqoop import -Dorg.apache.sqoop.splitter.allow_text_splitter=true --table cp_titles_date --connect jdbc:mysql://database/employees --username root --password secret -m 4 --warehouse-dir /user/hive/warehouse/db_test2_title --split-by title
  
Importar a tabela cp_titles_date com 4 mapeadores divididos pelo campo data no warehouse /user/hive/warehouse/db_test2_date

    sqoop import -Dorg.apache.sqoop.splitter.allow_text_splitter=true --table cp_titles_date --connect jdbc:mysql://database/employees --username root --password secret -m 4 --warehouse-dir /user/hive/warehouse/db_test2_date --split-by to_date
  
Qual a diferença dos registros nulos entre as duas importações?

    -- se comparar o tamanho e o número de arquivos
    hdfs dfs -count -h /user/hive/warehouse/db_test2_date
    hdfs dfs -count -h /user/hive/warehouse/db_test2_title
    -- e listar os diretórios
    hdfs dfs -ls -h -R /user/hive/warehouse/db_test2_date
    hdfs dfs -ls -h -R /user/hive/warehouse/db_test2_title
    
    -- verificamos que os arquivos com split por date tem menos registros e ficou com tamanhos desbalanceados.
    -- se lermos os registros do table date, notamos que os titles Staff , que contém data nulo, foi igonorado na importação
    -- este é um ponto de atenção que precisa ser validado antes
    hdfs dfs -cat /user/hive/warehouse/db_test2_date/cp_titles_date/part-m-00000 | head -n 10
