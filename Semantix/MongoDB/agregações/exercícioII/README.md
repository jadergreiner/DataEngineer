# Agregação com Lookup e project

 1. Crie a collection cursos no banco de dados escola

2. Importe o arquivo “dataset\cursos.csv” para a collection cursos, com os seguintes atributos:

id_curso: Number
id_unidade: Number
nome: String
nivel: String
Arquivos do Dataset

3. Realizar o left outer join da collection alunos e cursos, quando o id_curso dos 2 forem o mesmo.

4. Realizar o left outer join da collection alunos e cursos, quando o id_curso dos 2 forem o mesmo e visualizar apenas os seguintes campos

Alunos: id_discente, nivel
Cursos: id_curso, id_unidade, nome
