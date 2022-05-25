# Hive - Seleção de Tabelas

1 . Selecionar os 10 primeiros registros da tabela nascimento pelo ano de 2016

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
    
    -- executando a consulta
    select * from jader.nascimento where ano = 2016 limit 10;

2 . Contar a quantidade de nomes de crianças nascidas em 2017

    select count(nome) from jader.nascimento where ano = 2017;

3 . Contar a quantidade de crianças nascidas em 2017
  
    select sum(frequencia) from jader.nascimento where ano = 2017;

4 . Contar a quantidade de crianças nascidas por sexo no ano de 2015
  
    select sexo, sum(frequencia) as qtd from jader.nascimento where ano = 2015 group by sexo;

5 . Mostrar por ordem de ano decrescente a quantidade de crianças nascidas por sexo

    select ano, sexo, sum(frequencia) as qtd from jader.nascimento group by ano, sexo order by ano desc;

6 . Mostrar por ordem de ano decrescente a quantidade de crianças nascidas por sexo com o nome iniciado com ‘A’

    -- opção 1 com substring
    select ano, sexo, sum(frequencia) as qtd from jader.nascimento where (substring(nome,1,1) ='A') group by ano, sexo order by ano desc;
    -- opção 2 com like
    select ano, sexo, sum(frequencia) as qtd from jader.nascimento where nome like 'A%' group by ano, sexo order by ano desc;

7 . Qual nome e quantidade das 5 crianças mais nascidas em 2016

    -- opção 1 com o sum
    select nome, sum(frequencia) as qtd from jader.nascimento where ano = 2016 group by nome order by qtd desc limit 5;
    -- opção 2 com o max
    select nome, max(frequencia) as qtd from jader.nascimento where ano = 2016 group by nome order by qtd desc limit 5;

8 . Qual nome e quantidade das 5 crianças mais nascidas em 2016 do sexo masculino e feminino

    select nome, max(frequencia) as qtd, sexo from jader.nascimento where ano = 2016 group by nome, sexo  order by qtd desc limit 5;
