# Exercícios - Configuração

1 . Visualizar todos os parâmetros de configuração

2 . Verificar o parâmetro “appendonly”

3 . Remover a persistência dos dados, alterando o parâmetro “appendonly” para “no”

4 . Verificar o parâmetro “save”

5 . Adicionar a persistência dos dados, para a cada 2 minutos (120 segundos) se pelo menos 500 chaves forem alteradas, adicionando o parâmetro “save” para “120 500”

6 . Verificar os parâmetros “maxmemory*”

7 . Permitir que o Redis remova automaticamente os dados antigos à medida
que você adiciona novos dados,  com uso da politica “allkeys-lru”, quando chegar a 1mb de memória.
