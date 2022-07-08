# Índices

1. Visualizar as configurações do índice produto

        GET produto/_settings

2. Visualizar o mapeamento do índice produto

        GET produto/_mapping

3. Visualizar o mapeamento do atributo nome do índice produto

        GET produto/_mapping/field/nome

4. Inserir o campo data do tipo date no índice produto

        PUT produto/_mapping
        {
          "properties":{
            "data": {
              "type":"date"
            }
          }
        }

5. Adicionar o documento:

_id: 6, "nome": "teclado", "qtd": 100, "descricao": "USB", "data":"2020-09-18"

        PUT produto/_doc/6
        {
          "nome": "teclado", "qtd": 100, "descricao": "USB", "data":"2020-09-18"
        }

6. Reindexar o índice produto para produto2, com o campo quantidade para o tipo short

    ### se olhar o mapeamento, qtd é do tipo long
        {
          "produto" : {
            "mappings" : {
              "properties" : {
                "data" : {
                  "type" : "date"
                },
                "descricao" : {
                  "type" : "text",
                  "fields" : {
                    "keyword" : {
                      "type" : "keyword",
                      "ignore_above" : 256
                    }
                  }
                },
                "nome" : {
                  "type" : "text",
                  "fields" : {
                    "keyword" : {
                      "type" : "keyword",
                      "ignore_above" : 256
                    }
                  }
                },
                "qtd" : {
                  "type" : "long"
                }
              }
            }
          }
          
      ### não conseguimos dar um PUT como realizamos acima por este o campo qtd já existe
      ### Vamos criar o índice produto2
        PUT produto2
        {

        }
    ### depois daremos um GET maping em produto e copiamos o properties para usar no produto2. 
        PUT produto2/_mapping
        {
          "properties" : {
                "data" : {
                  "type" : "date"
                },
                "descricao" : {
                  "type" : "text",
                  "fields" : {
                    "keyword" : {
                      "type" : "keyword",
                      "ignore_above" : 256
                    }
                  }
                },
                "nome" : {
                  "type" : "text",
                  "fields" : {
                    "keyword" : {
                      "type" : "keyword",
                      "ignore_above" : 256
                    }
                  }
                },
                "qtd" : {
                  "type" : "short"
                }
              }
        }
    ### Agora faremos o reindex
        POST _reindex
        {
          "source": {
            "index": "produto"
            },
            "dest": {
              "index": "produto2"
            }
        }

7. Visualizar o mapeamento do índice produto2

        GET produto2/_mapping

8. Fechar o índice produto

        POST produto/_close

9. Pesquisar todos os documentos no índice produto

        GET produto/_search

10. Abrir o índice produto

        POST produto/_open
