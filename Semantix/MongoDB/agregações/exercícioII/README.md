# Agregação com Lookup e project

 1. Crie a collection cursos no banco de dados escola

        -- conforme exercício 1

2. Importe o arquivo “dataset\cursos.csv” para a collection cursos, com os seguintes atributos:

- id_curso: Number
- id_unidade: Number
- nome: String
- nivel: String

        -- conforme exercício 1

3. Realizar o left outer join da collection alunos e cursos, quando o id_curso dos 2 forem o mesmo.

        -- usamos no compass. Abaixo o código completo se fossemos executar no shell
        [{$lookup: {
         from: 'cursos',
         localField: 'id_curso',
         foreignField: 'id_curso',
         as: 'curso'
        }}]

        -- cria um documentado identado
        -- para cada aluno os dados do curso
        -- poderia ser o contrário. Para cada curso, mostrar os alunos
        
<img src= "./img/03.png">        
        
4. Realizar o left outer join da collection alunos e cursos, quando o id_curso dos 2 forem o mesmo e visualizar apenas os seguintes campos

Alunos: id_discente, nivel
Cursos: id_curso, id_unidade, nome

    -- após estágio do LOOKUP, adicionar um novo estágio de project
    {
      id_discente: 1, nivel: 1, 
      "curso.id_curso": 1,
      "curso.id_unidade": 1,
      "curso.nome": 1,
    }
    
<img src= "./img/04.png">            

## Código final completo

    [{$lookup: {
         from: 'cursos',
         localField: 'id_curso',
         foreignField: 'id_curso',
         as: 'curso'
        }
    }, {
        $project: {
            id_discente: 1,
             nivel: 1,
             'curso.id_curso': 1,
             'curso.id_unidade': 1,
             'curso.nome': 1
        }
    }]
