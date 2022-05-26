# Hive - Criação de Tabelas Otimizadas

1 . Usar o banco de dados <nome>
  
    -- após acessar o Hive e conectar ao beeline (instruçẽos nas aulas anteriores)
    use jader;

2 . Selecionar os 10 primeiros registros da tabela pop
    
    select * from pop limit 10;

3 . Criar a tabela pop_parquet no formato parquet para ler os dados da tabela pop
  
    create table pop_parquet(zip_code int, total_population int, median_age float, total_males int, total_females int, total_households int, average_household_size float) stored as parquet;

4 . Inserir os dados da tabela pop na pop_parquet
  
    -- como criamos os mesmos atributos nas tabelas, o select * vai funcionar
    insert into pop_parquet select * from pop;

5 . Contar os registros da tabela pop_parquet
  
    select count (*) from pop_parquet;

6 . Selecionar os 10 primeiros registros da tabela pop_parquet
  
    select * from pop_parquet limit 10;

7 . Criar a tabela pop_parquet_snappy no formato parquet com compressão Snappy para ler os dados da tabela pop
  
    create table pop_parquet_snappy(zip_code int, total_population int, median_age float, total_males int, total_females int, total_households int, average_household_size float) stored as parquet tblproperties('parquet.compress'='SNAPPY');
  
    -- se quiser verificar na descrição da tabela
    desc formatted pop_parquet_snappy;

8 . Inserir os dados da tabela pop na pop_parquet_snappy
  
    insert into pop_parquet_snappy select * from pop;

9 . Contar os registros da tabela pop_parquet_snappy
  
    select count (*) from pop_parquet_snappy;

10 . Selecionar os 10 primeiros registros da tabela pop_parquet_snappy
  
    select * from pop_parquet_snappy limit 10;

11 . Comparar as tabelas pop, pop_parquet e pop_parquet_snappy no HDFS.
  
    -- aqui podemos olhar o armazenamento
    -- saímos do beelilne e do hive
    CTRL + D ( 2 vezes)
  
    -- voltamos ao console e conectamos ao namenode
    docker exec -it namenode bash
  
    -- listamos os diretórios do hdfs
    hdfs dfs -ls /user/hive/warehouse/jader.db
  
    -- consultamos de forma reversa para mostrar maiores informações
    hdfs dfs -ls -R /user/hive/warehouse/jader.db
  
    -- enriquecendo com dados de armazenamento
    hdfs dfs -ls -R -h user/hive/warehouse/jader.db
    
    hdfs dfs -du -h /user/hive/warehouse/jader.db

