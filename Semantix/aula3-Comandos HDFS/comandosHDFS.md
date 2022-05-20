# Resolução do exercício de comandos HDFS da aula 3

1. Iniciar o cluster de Big Data

    <code>
      cd docker-bigdata
    </code>
    <br>
    <code>
      docker-compose up -d
    </code>

2. Baixar os dados dos exercícios do treinamento
  
    <code>
      cd input
    </code> <br>
    <code>
      sudo git clone https://github.com/rodrigo-reboucas/exercises-data.git
    </code>
  
3. Acessar o container do namenode

    <code>
      docker exec -it namenode bash
    </code> <br>
4. Criar a estrutura de pastas apresentada a baixo pelo comando: $ hdfs dfs -ls -R / <br>
    user/aluno/ 
    <nome> <br>
    data <br>
    recover <br>
    delete <br>
  
    <code>
      hdfs dfs -mkdir -p /user/aluno/jader/data/
    </code> <br>
    <code>
      hdfs dfs -mkdir -p /user/aluno/jader/recover
    </code> <br>
    <code>
      hdfs dfs -mkdir -p /user/aluno/jader/delete
    </code>
      
5. Enviar a pasta “/input/exercises-data/escola” e o arquivo “/input/exercises-data/entrada1.txt” para data
  
    <code>
      hdfs dfs -put /input/exercises-data/escola/ /user/aluno/jader/data/
    </code> <br>
    <code>
      hdfs dfs -put /input/exercises-data/entrada1.txt /user/aluno/jader/data/
    </code>
  
6. Mover o arquivo “entrada1.txt” para recover
  
    <code>
      hdfs dfs -mv /user/aluno/jader/data/entrada1.txt /user/aluno/jader/recover/
    </code> <br>
  
7. Baixar o arquivo do hdfs “escola/alunos.json” para o sistema local /
  
    <code>
      hdfs dfs -get /user/aluno/jader/data/escola/alunos.json
    </code>
  
8. Deletar a pasta recover
  
    <code>
      hdfs dfs -rm -r /user/aluno/jader/recover
    </code>
  
9. Deletar permanentemente o delete
  
    <code>
      hdfs dfs -rm -r -skipTrash /user/aluno/jader/delete
    </code>
  
10. Procurar o arquivo “alunos.csv” dentro do /user
  
    <code>
      hdfs dfs -find / -name alunos.csv
    </code>
  
11. Mostrar o último 1KB do arquivo “alunos.csv”
  
    <code>
      hdfs dfs -tail /user/aluno/jader/data/escola/alunos.csv
    </code> <br>
  
    Outra forma de visualizar com tail </br>
    <code>
      hdfs dfs -cat /user/aluno/jader/data/escola/alunos.csv | tail -n 5
    </code>
  
12. Mostrar as 2 primeiras linhas do arquivo “alunos.csv”
  
    <code>
      hdfs dfs -cat /user/aluno/jader/data/escola/alunos.csv | head -n 2
     </code>
  
13. Verificação de soma das informações do arquivo “alunos.csv”

    <code>
      hdfs dfs -checksum /user/aluno/jader/data/escola/alunos.csv
    </code>
 
14. Criar um arquivo em branco com o nome de “test” no data

    <code>
      hdfs dfs -touchz /user/aluno/jader/data/test
    </code>
    
15. Alterar o fator de replicação do arquivo “test” para 2

    <code>
      hdfs dfs -setrep 2 /user/aluno/jader/data/test
    </code>
    
16. Ver as informações do arquivo “alunos.csv”

    <code>
      hdfs dfs -stat /user/aluno/jader/data/escola/alunos.csv
    </code>
    
17. Exibir o espaço livre do data e o uso do disco

      Espaço livre diretorio data </br>
      <code>
        hdfs dfs -df -h /user/aluno/jader/data/
      </code> </br> </br>
      Uso do disco </br>
      <code>
        hdfs dfs -du -h /user/aluno/jader/data/
      </code>
