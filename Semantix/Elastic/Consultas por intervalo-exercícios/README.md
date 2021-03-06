# Consultas por Intervalo

1. Verificar se existe o índice populacao

        HEAD populacao

2. Executar as consultas no índice populacao

a) Mostrar os documentos com o atributo "Total Population" menor que 100

        GET populacao/_search
        {
          "query": {
            "range": {
              "Total Population": {
                "lt": 100
              }
            }
          }
        }


b) Mostrar os documentos com o atributo "Median Age" maior que 70

        GET populacao/_search
        {
          "query": {
            "range": {
              "Median Age": {
                "gt": 70
              }
            }
          }
        }

c) Mostrar os documentos 50 (Zip Code: 90056) à 60 (Zip Code: 90067) do índice de populacao

        -- por padrão a paginação mostra 10 registros. Vou incluir opcionalmente o atributo size para mostrar 20 registros por página
        GET populacao/_search
        {
          "size": 20,
          "query": {
            "range": {
              "Zip Code": {
                "gte": 90056,
                "lte": 90067
              }
            }
          }
        }

3. Importar através do Kibana o arquivo weekly_MSFT.csvPré-visualizar o documento (Guia Arquivos/dataset/weekly_MSFT.csv) com o índice bolsa

4. Executar as consultas no índice bolsa

        -- conhecendo os campos do dataset e os tipos
        GET bolsa/_mapping

a) Visualizar os documentos do dia 2019-01-01 à 2019-03-01. (hits = 9)

        GET bolsa/_search
        {
          "query": {
            "range": {
              "timestamp": {
                "gte": "2019-01-01",
                "lte": "2019-03-01",
                "format": "yyyy-MM-dd"
              }
            }
          }
        }                

b) Visualizar os documentos do dia 2019-04-01 até agora. (hits = 3)

        GET bolsa/_search
        {
          "query": {
            "range": {
              "timestamp": {
                "gte": "2019-04-01",
                "lte": "now",
                "format": "yyyy-MM-dd"
              }
            }
          }
        }
