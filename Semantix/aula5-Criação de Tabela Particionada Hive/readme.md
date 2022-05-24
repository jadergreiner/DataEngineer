# Exercícios - Criação de Tabela Particionada Hive


1 . Criar o diretório “/user/aluno/<nome>/data/nascimento” no HDFS
  
    -- inicialmente vamos listar os diretórios no hdfs
    docker exec -it namenode hdfs dfs -ls /
    -- lembrando que no namenome temos os arquivos locais e o sistema do hdfs
    -- os arquivos do hdfs obtemos com o comando acima. 
  
    -- mas se quisermos os arquivos locais? neste caso, não usamos o comando hdfs
    docker exec -it namenode ls /
  
    -- Optamos em  criar o diretório diretamente pelo console no hdfs
    docker exec -it namenode hdfs dfs -mkdir /user/aluno/jader/data/nascimento
  
    -- listando o diretório para conferência
    docker exec -it namenode hdfs dfs -ls /user/aluno/jader/data/

2 . Criar e usar o Banco de dados <nome>
  
    -- este banco de dados já foi criado nas aulas anteriores

3 . Criar uma tabela externa no Hive com os parâmetros:

  a) Tabela: nascimento

  b) Campos: nome (String), sexo (String) e frequencia (int)

  c) Partição: ano

  d) Delimitadores:

   * i) Campo ‘,’

   * ii)  Linha ‘\n’

  e) Salvar

   * i) Tipo do arquivo: texto

   * ii) HDFS: '/user/aluno/<nome>/data/nascimento’
  
    -- Poderíamos criar no console, mas vamos entrar no bash
    -- como usamos o beeline, para colocar em uma única linha, o comando ficaria muito grande
    
    -- conectando ao bash do hive
    docker exec -it hive-server bash
    
    -- pelo hive entramos no beeline
    beeline -u jdbc:hive2://localhost:10000
  
    -- primeiramente vamos visualizar os bancos de dados
    show databases;
    -- o banco de dados em meu nome já está listado. Vamos iniciar a sua utililização
    use jader;
    -- listando as tabelas
    show tables;
  
    -- comando para criar a tabela
    create external table nascimento (nome string, sexo string, frequencia int) partitioned by (ano int) row format delimited fields terminated by ',' lines terminated by '\n' stored as textfile location '/user/aluno/jader/data/nascimento';
    
    -- no location poderia ser assim 
    location 'hdfs://namenome:8020/user/aluno/jader/data/nascimento';
    -- como nosso ambiente já está configurado, ele já direciona para o hdfs. Em ambos vai funcionar
  
4 . Adicionar partição ano=2015
  
    -- como já temos a partição, vamos usar alter table para criar o ano
    alter table nascimento add partition(ano=2015);

5 . Enviar o arquivo local “input/exercises-data/names/yob2015.txt” para o HDFS no diretório /user/aluno/<nome>/data/nascimento/ano=2015
  
    -- primeiramente vamos sair do beeline
    CTRL + D
    -- estamos no Hive. Vamos sair e voltar ao terminal
    CTRL + D
    -- agova vamos acessar o bash do namenode
    docker exec -it namenode bash
  
    -- primeiro vamos listar o diretório no HDFS e verificar se existe o diretório ano=2015
    hdfs dfs -ls /user/aluno/jader/data/nascimento
    
    -- enviando o arquivo
    hdfs dfs -put /input/exercises-data/names/yob2015.txt /user/aluno/jader/data/nascimento/ano=2015
  
    -- se a estrutura do HDFS e do Hive está pronta, já será possível ler os registros no beeline
  
6 . Selecionar os 10 primeiros registros da tabela nascimento no Hive
  
    -- acessando o Hive e o beeline
    -- saindo do namenode e voltando ao console
    CTRL +D
    -- acesso ao bash do hive
    docker exec -it hive-server bash
    -- acesso ao beeline
    beeline -u jdbc:hive2://localhost:10000
  
    -- executando a consulta
    select * from jader.nascimento limit 10;

7 . Repita o processo do 4 ao 6 para os anos de 2016 e 2017.
  
    -- Passo 1
    -- criando as partições no Hive com beeline
    alter table nascimento add partition(ano=2016);
    alter table nascimento add partition(ano=2017);

    -- Passo 2
    -- enviando os arquivos para as partições no HDFS
    hdfs dfs -put /input/exercises-data/names/yob2016.txt /user/aluno/jader/data/nascimento/ano=2016
    hdfs dfs -put /input/exercises-data/names/yob2017.txt /user/aluno/jader/data/nascimento/ano=2017
  
    -- Passo 3
    -- realizando a consulta no beeline para conferência
    select * from jader.nascimento where ano = 2017 limit 10;
    select * from jader.nascimento where ano = 2016 limit 10;
    select * from jader.nascimento where ano = 2015 limit 10;
    
