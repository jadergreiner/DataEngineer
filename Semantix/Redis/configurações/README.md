# Exercícios - Configuração

1 . Visualizar todos os parâmetros de configuração

    config get *

2 . Verificar o parâmetro “appendonly”

    config get appendonly
    
    -- este comando indica se queremos ter a persistência dos nossos dados
    
3 . Remover a persistência dos dados, alterando o parâmetro “appendonly” para “no”

    config set appendonly no

4 . Verificar o parâmetro “save”

    config get save

5 . Adicionar a persistência dos dados, para a cada 2 minutos (120 segundos) se pelo menos 500 chaves forem alteradas, adicionando o parâmetro “save” para “120 500”

    config get save '120 500'
    
    -- como são 2 parâmetros, obrigatoriamente precisa colocar entre aspas 

6 . Verificar os parâmetros “maxmemory*”

    config get maxmemory*

7 . Permitir que o Redis remova automaticamente os dados antigos à medida que você adiciona novos dados,  com uso da politica “allkeys-lru”, quando chegar a 1mb de memória.

    config set maxmemory-policy allkeys-lru
    
    config set maxmemory 1mb
    
    
