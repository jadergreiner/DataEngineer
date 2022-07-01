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

    -- abrir em outro terminal o console producer
    kafka-console-producer --broker-list localhost:9092 --topic msg-cli

- Msg 1    
- Msg 2

5 . Criar outro consumidor do grupo app-cli

    kafka-console-consumer --bootstrap-server localhost:9092 --topic msg-cli-2 --group app-cli

6. Enviar as seguintes mensagens do produtor

Msg 4
Msg 5
Msg 6
Msg 7
7. Criar outro consumidor do grupo app2-cli

8. Enviar as seguintes mensagens do produtor

Msg 8
Msg 9
Msg 10
Msg 11
9. Parar o app-cli

10. Definir o deslocamento para -2 offsets do app-cli

11. Descrever grupo

12. Iniciar o app-cli

13. Redefinir o deslocamento o app-cli

14. Iniciar o app-cli

15. Listar grupo
