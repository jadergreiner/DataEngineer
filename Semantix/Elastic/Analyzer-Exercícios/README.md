# Analyzer

## 1. Criar os Analyzer simple, standard, brazilian e portuguese para a seguinte frase:

O elasticsearch surgiu em 2010

##### O Simples não cria token para os números

    POST _analyze
    {
      "analyzer": "simple",
      "text": "O elastichsearch surgiu em 2010"
    }
##### Standard é o padrão. Semelhante ao Simple, mas agora cria token para o número
    POST _analyze
    {
      "analyzer": "standard",
      "text": "O elastichsearch surgiu em 2010"
    }
##### No brazilian, ele retirou "O" do começo e o "em". O "surgiu" deixou apenas a raiz (surg)
    POST _analyze
    {
      "analyzer": "brazilian",
      "text": "O elastichsearch surgiu em 2010"
    }
##### No portuguese, ele retirou "O" do começo e o "em". Manteve o surgiu normalmente. O portuguese é o Português de Portugal
    POST _analyze
    {
      "analyzer": "portuguese",
      "text": "O elastichsearch surgiu em 2010"
    }

## 2. Realizar os passos no índice produto

##### a) Criar um analyzer brazilian para o atributo descricao
Primeiramente, podemos fazer um mapping no índice e verificar que o campo descrição não possui um Analyzer pra ele.
  
    GET produto/_mapping

Como já temos o indice e o atributo, não vamos conseguir fazer um PUT no campo e adicionar o Analyzer. Será necessário reindexar.

Primeiro vamos criar um PUT provisório com os settings e mappings que vamos atualizar ou adicionar

    PUT produto1
    {
      "settings": {
        "index": {
          "number_of_shards": 1,
          "number_of_replicas": 0
        }
      },
      "mappings": {
        "properties": {
          "descricao": {
            "type": "text",
            "analyzer": "brazilian"
          }
        }
      }
    }

Agora vamos reindexar os dados com **POST**

    POST _reindex
    {
      "source": {
        "index": "produto"
      },
      "dest": {
        "index": "produto1"
      }
    }
Vamos dar um **GET** no produto1 e verificar o analyzer da descrição

    GET produto1/_mapping

b) Para o atributo descricao aplicar o analzyer brazilian para o tipo de campo text e criar o atributo descricao.original com o dado do tipo keyword

Como no exercício acima criamos o analyzer em produto1. Vamos fazer este exercício em cima de exercício.
Vamos deletar o índice produto e depois fazer um PUT em produto.

    DELETE produto
   
Agora vamos fazer o PUT. 
E todos os outros campos? Ele vai pegar quando reindexarmos do produto1.

    PUT produto
    {
      "settings": {
        "index": {
          "number_of_shards": 1,
          "number_of_replicas": 0
        }
      },
      "mappings": {
        "properties": {
          "descricao": {
            "type": "text",
            "analyzer": "brazilian",
            "fields": {
              "original": {"type": "keyword"}
            }
          }
        }
      }
    }
    
Após o reindex, dar um **GET** em produto

    GET produto

c) Buscar a palavra “compativel” no campo descricao.original (hits = 0)

        GET produto/_search
        {
          "query": {
            "match": {
              "descricao.original": "compativel"
            }
          }
        }

d) Buscar a palavra “compativel” no campo descricao

    GET produto/_search
    {
      "query": {
        "match": {
          "descricao": "compativel"
        }
      }
    }
