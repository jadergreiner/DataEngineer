# REDIS - Exercícios - Listas

1. Criar a chave “views:ultimo_usuario" e insira nesta ordem os seguintes valores como lista:

Final da lista “Joao”
Final da lista “Ana”
Inicio da lista “Carlos”
Final da lista “Carol”

    rpush views:ultimo_usuario Joao
    rpush views:ultimo_usuario Ana
    lpush views:ultimo_usuario Carlos
    rpush views:ultimo_usuario Carol
    
    
2. Visualizar todos os elementos da lista

        lrange views:ultimo_usuario 0 -1

3. Visualizar todos os elementos da lista, com exceção do último

        lrange views:ultimo_usuario 0 -2

4. Visualizar o tamanho da lista

        llen views:ultimo_usuario

5. Redefinir o tamanho da lista, removendo o primeiro elemento (Sem usar o pop)

        ltrim 1 2

6. Visualizar o tamanho da lista

        llen views:ultimo_usuario

7. Recuperar os elementos da lista da seguinte ordem:

Primeiro

        lpop views:ultimo_usuario
            
Último

        rpop views:ultimo_usuario
        
Primeiro com bloqueio de 5 segundos se a lista estiver vazia

        -- primeiro vamos gerar o erro pois a lista está vazia
        lpop views:ultimo_usuario
        
        -- para aguardar usamos o "b" na frente e o tempo
        blpop views:ultimo_usuario 5 
        
Primeiro com bloqueio de 5 segundos se a lista estiver vazia
