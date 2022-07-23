# RDD - Exercícios

1. Ler com RDD os arquivos localmente do diretório “/opt/spark/logs/” ("file:///opt/spark/logs/")

        log = sc.textFile("file:///opt/spark/logs")

2. Com uso de RDD faça as seguintes operações

a) Contar a quantidade de linhas

        log.count()

b) Visualizar a primeira linha

        log.first()

c) Visualizar todas as linhas

        log.collect()        

d) Contar a quantidade de palavras

        # Separar as palavras da linha
        # regra da lambda (função anônima) - para cada linha, quero separar por espaços
        palavras = log.flatMap(lambda linha: linha.split(" "))
        palavras.count()

e) Converter todas as palavras em minúsculas

        # regra da lambda - para cada palavra, leia a palavra e converta para mínusculo
        minusculas = palavras.map(lambda palavra: palavra.lower())

f) Remover as palavras de tamanho menor que 2

        # regra da lambda - filtro >> para cada palavra conte o número de letras e filtre apenas aquelas com mais de duas letras
        minusculas_filter_maior2 = minusculas.filter(lambda palavra: len(palavra) > 2)

g) Atribuir o valor de 1 para cada palavra

        # regra da lambda > mapeando e toda vez que tenho uma palavra eu monto um array com a palavra associado ao número 1
        palavra_chave_valor = minusculas_filter_maior2.map(lambda palavra: (palavra,1))

h) Contar as palavras com o mesmo nome

        # Juntar as palavras
        # usei o reduce pela chave. Sendo que a chave á a própria palavra
        ## regra da lambda > lendo a chave1 e chave2 (palavra igual), soma o valor da chave 2 (igual 1) ao valor acumulado da chave1
        palavras_reduce = palavra_chave_valor.reduceByKey(lambda chave1, chave2 : chave1 + chave2)
        ## agora podemos contar as palavras
        palavras_reduce.count()

i) Visualizar em ordem alfabética

        # 0 ordena pela chave
        palavras_ordenadas = palavras_reduce.sortBy(lambda palavra: palavra[0])

j) Visualizar em ordem decrescente a quantidade de palavras

        ## 0 [1] ordena pelo valor
        ## o sinal de negativo (-) ordena descrecente
        palavras_ordenadas = palavras_reduce.sortBy(lambda palavra: -palavra[1])
        ## outra forma
        palavras_ordenadas = palavras_reduce.sortBy(lambda palavra: palavra[1],False)

k) Remover as palavras, com a quantidade de palavras > 1

        palavras_filter_maior_1 = palavras_ordenadas.filter(lambda palavra: palavra[1]>1)

l) Salvar o RDD no diretorio do HDFS /user/<seu-nome>/logs_count_word

        palavras_filter_maior_1.saveAsTextFile("/user/jader/logs_count_word")
        
        ##  conferir se está salvo
        !hdfs dfs -ls /user/jader
