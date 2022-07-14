# Agregações

Realizar os exercícios no índice bolsa

1. Calcular a média do campo volume

        -- usando o size=0 para não mostrar as linhas individualizadas. Assim mostra direto o resultado do aggs
        GET bolsa/_search
        {
          "size": 0, 
          "aggs": {
            "media": {
              "avg": {
                "field": "volume"
              }
            }
          }
        }

2. Calcular a estatística do campo close

        GET bolsa/_search
        {
          "size": 0, 
          "aggs": {
            "media": {
              "stats": {
                "field": "close"
              }
            }
          }
        }

3. Visualizar os documentos do dia 2019-04-01 até agora. (hits = 3)

        GET bolsa/_search
        {
          "query": {
            "range": {
              "@timestamp": {
                "gte": "2019-04-01",
                "lte": "now"
              }
            }
          }
        }

4. Calcular a estatística do campo open do período do dia 2019-04-01 até agora

        GET bolsa/_search
        {
          "size": 0, 
          "query": {
            "range": {
              "@timestamp": {
                "gte": "2019-04-01",
                "lte": "now"
              }
            }
          },
          "aggs": {
            "estatistica": {
              "stats": {
                "field": "open"
              }
            }
          }
        }


5. Calcular a mediana do campo open

        -- não existe a função mediana no slastic. Mas podemos usar o percentiles que nos dá o resultado. Os valores dos percents são informados
        -- na query. Aqui deixei o padrão, mas poderia remover ou adicionar qualquer outro valor.
        GET bolsa/_search
        {
          "size": 0, 
          "aggs": {
            "mediana": {
              "percentiles": {
                "field": "open",
                "percents": [
                  1,
                  5,
                  25,
                  50,
                  75,
                  95,
                  99
                ]
              }
            }
          }
        }

6. Contar a quantidade de documentos agrupados por ano

        GET bolsa/_search
        {
          "size": 0,
          "aggs": {
            "doc_anos": {
              "date_histogram": {
                "field": "@timestamp",
                "calendar_interval": "year"
              }
            }
          }
        }

7. Contar a quantidade de documentos de 2 anos atrás até hoje

        GET bolsa/_search
        {
          "size": 0,
          "aggs": {
            "qtd_2anos": {
              "date_range": {
                "field": "@timestamp",
                "ranges": [
                  {
                    "from": "now-2y",
                    "to": "now"
                  }
                ]
              }
            }
          }
        }
