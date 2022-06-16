# Exercícios - Strings


    -- No exercício trabalhei com Docker na VM Linux
    -- após importar a imagem e acessar o bash do redis
    -- executar redis-cli para entrar no console e executar os comandos
    
1. Criar a chave "usuario:nome" e atribua o valor do seu nome

        set usuario:nome jader

2. Criar a chave "usuario:sobrenome" e atribua o valor do seu sobrenome

        set usuario:sobrenome greiner

3. Busque a chave "usuario:nome“

        get usuario:nome

4. Verificar o tamanho da chave "usuario:nome“

        strlen usuario:nome

5. Verificar o tipo da chave "usuario:sobrenome"

        type usuario:nome

6. Criar a chave "views:qtd" e atribua o valor 100

        set views:qtd 100

7. Incremente o valor em 10 da chave "views:qtd"

        incrby views:qtd 10

8. Busque a chave "views:qtd"

        get views:qtd

9. Deletar a chave "usuario:sobrenome"

        del usuario:sobrenome

10. Verificar se a chave "usuario:sobrenome" existe

        exists usuario:sobrenome

11. Definir um tempo de 3600 segundos para a chave "views:qtd" ser removida

        expire views:qtd 3600

12. Verificar quanto tempo falta para a chave "views:qtd" ser removida

        ttl views:qtd

13. Verificar a persistência da chave "usuario:nome"

        ttl usuario:nome

14. Definir para a chave "views:qtd" ter persistência para sempre

        persist views:qtd

15. Clicar no botão de Enviar Tarefa, e enviar o texto: ok
