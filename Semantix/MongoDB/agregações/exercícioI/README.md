# Agregações de Match, Group, Sort e Limit

1. Crie o banco de dados escola
2. Crie a collection alunos no banco de dados escola

<img src = "./img/01.png">

3. Importe o arquivo “dataset/alunos.csv” para a collection alunos, com os seguintes atributos:

- id_discente: Number
- nome: String
- ano_ingresso: Number
- nivel: String
- id_curso: Number
- Arquivos para Dataset

<img src = "./img/03A.png">

<img src = "./img/03B.png">

4. Visualizar os valores únicos do “nivel” de cada “ano_ingresso”

        {
          _id: "$ano_ingresso",
          nível_por_ano: {
            $addToSet: "$nivel"
          }
        }
        
<img src = "./img/04.png">

5. Calcular a quantidade de alunos matriculados por cada “id_curso”

        -- Como o Mongo não possui um count, usamos o sum: 1
        -- nesta técnica ele conta 1 para cada linha
        
        {
          _id: "$id_curso",
          qtd_por_curso: {
            $sum: 1
          }
        }

<img src = "./img/05.png">

6. Calcular a quantidade de alunos matriculados por “ano_ingresso” no "id_curso“: 1222

        -- nesta atividade precisamos adiciona um estágio
        -- adicionamos o Match do is_curso
        -- depois aplicamos o group em cima do resultado

        [{$match: {
         id_curso: 1222
        }}, {$group: {
         _id: '$ano_ingresso',
         qtd_por_curso: {
          $sum: 1
         }
        }}]
        
<img src = "./img/06.png">

7. Visualizar todos os documentos do “nível”: “M”

        -- aqui é só aplicar um match

<img src = "./img/07.png">

8. Visualizar o último ano que teve cada curso (id_curso) dos níveis “M”

        -- usamos um Match pelo nível M
        -- depois aplicamos um group mostrando o ID do maior ano
        {
          _id: "$id_curso",
          "último_ano_curso": {
            $max: "$ano_ingresso"
          }
        }
        
<img src = "./img/08.png">

9. Visualizar o último ano que teve cada curso (id_curso) dos níveis “M”, ordenados pelos anos mais novos de cada curso

        -- mantém os estágios do 8
        -- adiciona um novo estágio de ordenação (sort) com opção -1
        
<img src = "./img/09.png">

10. Visualizar o último ano que teve os 5 últimos cursos (id_curso) dos níveis “M”, ordenados pelos anos mais novos

        -- mantém os estágios
        -- adiciona um novo estágio de limit
        
<img src = "./img/10.png">        

## Arquivo final completo

        [{
                $match: {
                        nivel: 'M'
                }
        }, {
                $group: {
                        _id: '$id_curso',
                        'último_ano_curso': {
                                $max: '$ano_ingresso'
                        }
                }
        }, {
                $sort: {
                        'último_ano_curso': -1
                }
        }, {
                $limit: 5
        }]
