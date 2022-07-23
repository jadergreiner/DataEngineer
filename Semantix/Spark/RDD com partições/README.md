# RDD com Partições

1. Ler com RDD os arquivos localmente do diretório “/opt/spark/logs/” ("file:///opt/spark/logs/") com 10 partições

        log_particoes = sc.textFile("file:///opt/spark/logs",10)
        log_particoes.getNumPartitions()

2. Contar a quantidade de cada palavras do RDD em 5 partições

        ## primeiro um word_count
        palavras_particoes = log_particoes.flatMap(lambda linha: linha.split(" "))
        palavras_minusculas_particoes = palavras_particoes.map(lambda palavra: palavra.lower())
        palavras_count_particoes = palavras_minusculas_particoes.map(lambda palavra: (palavra,1))
        
        palavras_reduce_particoes = palavras_count_particoes.reduceByKey(lambda chave1, chave2: chave1 + chave2,5)
        palavras_reduce_particoes.getNumPartitions()

3. Salvar o RDD no diretório do HDFS /user/<seu-nome>/logs_count_word_5

        palavras_reduce_particoes.saveAsTextFile("/user/jader/logs_count_word_particoes")

4. Refazer a questão 2, com todas as funções na mesma linha de um RDD
        execucao_unica_linha = log_particoes.flatMap(lambda linha: linha.split(" ")).map(lambda palavra: palavra.lower()).map(lambda palavra: (palavra,1))
