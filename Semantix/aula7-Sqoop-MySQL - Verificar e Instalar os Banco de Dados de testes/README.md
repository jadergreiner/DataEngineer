# MySQL - Verificar e Instalar os Banco de Dados de testes

1 . Copiar os dados do local para o contêiner database

    $ docker cp input/exercises-data/db-sql/ database:/

2 . Acessar o contêiner database

    $ docker exec -it database bash

3 . Instalar Banco de Dados de testes

    -- como acessar o mysql que já está instalado neste docker database
    -h > é a conexão
    -u > é o usuário
    -p > é a senha (padrão deste datanode 
    mysql -h localhost -u root 
    
    Diretório /db-sql - BD employees (Já existe)
      $ cd /db-sql  

      $ mysql -psecret < employees.sql

      Diretório /db-sql/sakila - BD sakila
      $ cd /db-sql/sakila/

      $ mysql -psecret < sakila-mv-schema.sql
      $ mysql -psecret < sakila-mv-data.sql
