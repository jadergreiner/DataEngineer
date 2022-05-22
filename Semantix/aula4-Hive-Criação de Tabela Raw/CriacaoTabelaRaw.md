# Resolução exercícios

1 . Enviar o arquivo local “/input/exercises-data/populacaoLA/populacaoLA.csv” para o diretório no HDFS “/user/aluno/<nome>/data/populacao”
  
    -- criando o diretório e depois enviando o arquivo
    hdfs dfs -mkdir /user/aluno/jader/data/populacao
    -- enviando o arquivo
    hdfs dfs -put /input/exercises-data/populacaoLA/populacaoLA.csv /user/aluno/jader/data/populacao
    -- verificando o conteúdo do arquivo
    hdfs dfs -cat /user/aluno/jader/data/populacao/populacaoLA.csv | head -n 3
  
2 . Listar os bancos de dados no Hive
  
    -- saindo do namenode, pressionando CTRL + D
    -- conectando ao hive
    docker exec -it hive-server bash
    -- para conectar aos bancos do hive, acessar o beeline. 
    -- Na dúvida sobre o comando, pode usar o help
    beeline --help
    -- conectando ao banco local
    beeline -u jdbc:hive2://localhost:10000
    -- listando os bancos de dados do Hive
    show databases;
  
3 . Criar o banco de dados <nome>
  
    -- criando o banco
    create database jader;
  
4 . Criar a Tabela Hive no BD <nome>
  
  Tabela interna: pop
    Campos:
        zip_code - int
        total_population - int
        median_age - float
        total_males - int
        total_females - int
        total_households - int
        average_household_size - float
    Propriedades
        Delimitadores: Campo ‘,’ | Linha ‘\n’
        Sem Partição
        Tipo do arquivo: Texto
        tblproperties("skip.header.line.count"="1")’
  
    -- primeiramento vamos nosso banco de dados
    use jader;
    -- criando a tabela
    create table pop(zip_code int, total_population int, median_age float, total_males int, total_females int, total_households int,  average_household_size float) row format delimited fields terminated by ',' lines terminated by '\n' stored as textfile tblproperties("skip.header.line.count"="1");
  
5 . Visualizar a descrição da tabela pop
  
    -- pode ser feito de duas formas. O desc mostra as colunas e o tipo
    desc pop; 
    -- se quiser ver informações adicionais e parâmetros/configurações, usar o desc formatted
    desc formatted pop;
