# Comandos HDFS

1. Iniciar o cluster de Big Data
* cd docker-bigdata
* docker-compose up -d

2. Baixar os dados dos exercícios do treinamento
* cd input
* sudo git clone https://github.com/rodrigo-reboucas/exercises-data.git

3. Acessar o container do namenode
4. Criar a estrutura de pastas apresentada a baixo pelo comando: 
  <code>
  $ hdfs dfs -ls -R /user/aluno/<nome>
  
      data
      recover
      delete
  </code>

5. Enviar a pasta “/input/exercises-data/escola” e o arquivo “/input/exercises-data/entrada1.txt” para  data

6. Mover o arquivo “entrada1.txt” para recover

7. Baixar o arquivo do hdfs “escola/alunos.json” para o sistema local /

8. Deletar a pasta recover

9. Deletar permanentemente o delete

10. Procurar o arquivo “alunos.csv” dentro do /user

11. Mostrar o último 1KB do arquivo “alunos.csv”

12. Mostrar as 2 primeiras linhas do arquivo “alunos.csv”

13. Verificação de soma das informações do arquivo “alunos.csv”

14. Criar um arquivo em branco com o nome de “test” no data

15. Alterar o fator de replicação do arquivo “test” para 2

16. Ver as informações do arquivo “alunos.csv”

17. Exibir o espaço livre do data e o uso do disco

18. Clicar no botão de Enviar Tarefa, e enviar o texto: ok
