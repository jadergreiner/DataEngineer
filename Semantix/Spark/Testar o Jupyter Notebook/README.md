# Cluster de Big Data para o curso e treinamento

1. Instalação do docker e docker-compose.

2. Executar os seguintes comandos, para baixar as imagens do Cluster de Big Data:

        git clone https://github.com/rodrigo-reboucas/docker-bigdata.git spark

        cd spark

        docker-compose –f docker-compose-parcial.yml pull

3. Iniciar o cluster Hadoop através do docker-compose

        docker-compose –f docker-compose-parcial.yml up -d
      
4. Listas as imagens em execução

5. Verificar os logs dos containers do docker-compose em execução

6. Verificar os logs do container jupyter-spark

7. Acessar pelo browser o Jupyter, através do link:

        http://localhost:8889
        
# Exercícios – Testar o Jupyter Notebook

1. Criar o arquivo do notebook com o nome teste_spark.ipynb

2. Obter as informações da sessão de spark (spark)

3. Obter as informações do contexto do spark (sc)

4. Setar o log como INFO.

5. Visualizar todos os banco de dados com o catalog

6. Ler os dados "hdfs://namenode:8020/user/rodrigo/data/juros_selic/juros_selic.json“ com uso de Dataframe

7. Salvar o Dataframe como juros no formato de tabela Hive

8. Visualizar todas as tabelas com o catalog

9. Visualizar no hdfs o formato e compressão que está a tabela juros do Hive

10. Ler e visualizar os dados da tabela juros, com uso de Dataframe no formato de Tabela Hive

11. Ler e visualizar os dados da tabela juros , com uso de Dataframe no formato Parquet

