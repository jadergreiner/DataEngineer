# Kafka por Linha de Comando

    -- para testar se a conexão e o Kakka está rodando podemos listar os tópicos
    -- depois de entrar no broker digitar
    kafka-topics --bootstrap-server localhost:9092 --list

1 . Criar o tópico msg-cli com 2 partições e 1 réplica
    
    kafka-topics --bootstrap-server localhost:9092 --topic msg-cli --create --partitions 2 --replication-factor 1

2 . Descrever o tópico msg-cli

    kafka-topics --bootstrap-server localhost:9092 --topic msg-cli --describe

3 . Criar o consumidor do grupo app-cli

    kafka-console-consumer --bootstrap-server localhost:9092 --topic msg-cli --group app-cli

4 . Enviar as seguintes mensagens do produtor

- Msg 1    
- Msg 2

        -- abrir em outro terminal o console producer
    
        kafka-console-producer --broker-list localhost:9092 --topic msg-cli
    
        -- ele vai deixar o terminal aguardando mensagem
        -- digite a primeira mensagem e de enter
        -- depois a segunda e digite enter
        -- visualize as mensagens no terminal de consumer

5 . Criar outro consumidor do grupo app-cli

    kafka-console-consumer --bootstrap-server localhost:9092 --topic msg-cli --group app-cli

6 . Enviar as seguintes mensagens do produtor

Msg 4
Msg 5
Msg 6
Msg 7

    -- observar com os dois terminais abertos
    -- como temosdusa partições, as mensagens serão alternadas entre os terminais
    
7. Criar outro consumidor do grupo app2-cli

    kafka-console-consumer --bootstrap-server localhost:9092 --topic msg-cli --group app2-cli

8. Enviar as seguintes mensagens do produtor

Msg 8
Msg 9
Msg 10
Msg 11

    -- consumer do mesmo grupo recebe as mensagens particionadas
    -- consumer de grupos diferentes sempre recebem a mensagem

9 . Parar o app-cli

    -- parar com CTRL + C

10 . Definir o deslocamento para -2 offsets do app-cli

    kafka-consumer-groups --bootstrap-server localhost:9092 --reset-offsets --shift-by -2 --execute --topic msg-cli --group app-cli

11 . Descrever grupo

    kafka-consumer-groups --bootstrap-server localhost:9092 --group app-cli --describe
    
    -- note no LAG que temos duas mensagens para trás (offset) em cada partição
    -- quando inicializamos o app-cli vamos ler estas 4 mensagens 

12 . Iniciar o app-cli

    kafka-console-consumer --bootstrap-server localhost:9092 --topic msg-cli --group app-cli

13 . Redefinir o deslocamento o app-cli

    -- finalizar o termnial CTRL + C
    
    kafka-consumer-groups --bootstrap-server localhost:9092 --group app-cli --describe
    
    -- repetindo o describe, ambos estão no fim
    
    -- agora vamos redefinir o offset desde o início
    kafka-consumer-groups --bootstrap-server localhost:9092 --reset-offsets --to-earliest --execute --topic msg-cli --group app-cli
    
    -- repetindo o describe, todos estão no início

14 . Iniciar o app-cli

    kafka-console-consumer --bootstrap-server localhost:9092 --topic msg-cli --group app-cli

15 . Listar grupo

    kafka-consumer-groups --bootstrap-server localhost:9092 -list 
