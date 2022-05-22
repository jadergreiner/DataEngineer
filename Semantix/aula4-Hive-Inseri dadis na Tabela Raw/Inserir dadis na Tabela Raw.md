# Exercícios - Inserir Dados na Tabela Raw 

1 . Visualizar a descrição da tabela pop do banco de dados
  
    -- partindo da ideia de já estar conectado ao beeline
    -- listando os databases
    show databases;
    -- usando o nosso banco de dados
    use jader;
    -- listando as tabelas e verificando a tabela pop
    show tables;
    -- verificando a descrição da tabela
    desc pop;
    -- verificando a descriçao com informações completas
    desc formatted pop;

2 . Selecionar os 10 primeiros registros da tabela pop

    -- realizando o select antes de inserir os dados
    select * from pop limit 10;

3 . Carregar o arquivo do HDFS “/user/aluno//data/população/populacaoLA.csv” para a tabela Hive pop
    
    -- carregando o arquivo. poderia colocar o arquivo especificamente, mas vamos mapear o diretório
    -- em PRD geralmente colocamos o diretório para mapear todos os arquivos que estão dentro
    load data inpath '/user/aluno/jader/data/populacao/' overwrite into table pop; 

4 . Selecionar os 10 primeiros registros da tabela pop

    select * from pop limit 10;

5 . Contar a quantidade de registros da tabela pop

    select count(*) from pop;
