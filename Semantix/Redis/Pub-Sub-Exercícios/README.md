# Exercícios - Pub/Sub

#### Como um Publica a outro subscreve, vamos precisar manter dois terminais abertos.

Um terminal irá publicar e o outro irá consumir.

1 . Criar um assinante para receber as mensagens do canal noticias:sp

        -- terminal 1 
        subscribe noticias:sp

2 . Criar um editor para enviar as seguintes mensagens no canal noticias:sp

Msg 1
Msg 2
Msg 3

        -- terminal 2
        publish noticias:sp 'Msg 1'
        
        publish noticias:sp 'Msg 2'
        
        publish noticias:sp 'Msg 3'

3 . Cancelar o assinante do canal noticias:sp

    -- terminal 1
    CTRL + C
    
    -- este comando cancela a subscrição
    -- via código é unsubscribe

4 . Criar um assinante para receber as mensagens dos canais com o padrão noticias:*

    -- terminal 1
    publish noticias:*
    
    -- o asterisco serve como geral

5 . Criar um editor para enviar as seguintes mensagens no canal noticias:rj

Msg 4
Msg 5
Msg 6

    -- terminal 2
    publish noticias:rj 'Msg 4'
    
    publish noticias:rj 'Msg 5'
    
    publish noticias:rj 'Msg 6'
