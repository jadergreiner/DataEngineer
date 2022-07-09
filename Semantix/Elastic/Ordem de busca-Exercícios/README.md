# Ordem de Busca

Realizar todas as buscas a seguir no índice produto

    -- por padrão, as consultas usam o atributo ou. Precisamos especificar o atributo "e" em nossa consulta.

1. Buscar os documentos que contenham as palavras “Windows” e “Linux” no atributo descrição

        GET produto/_search
        {
          "query": {
            "match": {
              "descricao": {
                "query": "windows linux",
                "operator": "and"
              }
            }
          }
        }

2. Buscar os documentos que contenham as palavras “Windows”, “Linux” ou “USB” no atributo descrição

        -- o padrão já é "OU". 
        GET produto/_search
        {
          "query": {
            "match": {
              "descricao": "windows linux usb"
            }
          }
        }

3. Buscar os documentos que contenham pelo menos 2 palavras da seguinte lista de palavras: “Windows”; “Linux” e “USB” no atributo descrição

        GET produto/_search
        {
          "query": {
            "match": {
              "descricao": {
                "query": "windows linux usb",
                "minimum_should_match": 2
              }
            }
          }
        }

4. Buscar os documentos que contenham pelo menos 50 % da seguinte lista de palavras: “Windows”; “Linux” e “USB” no atributo descrição

        GET produto/_search
        {   
          "query": {
            "match": {
              "descricao": {
                "query": "windows linux usb",
                "minimum_should_match": "50%"
              }
            }
          }
        }
