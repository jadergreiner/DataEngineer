# Exercícios - Sets

1. Deletar a chave “pesquisa:produto”

        del pesquisa:produto
        
        -- se aparecer 0 a chave nem existia
        -- se aparecer 1 a chave foi deletada

2. Criar a chave "pesquisa:produto" do tipo set com os seguintes valores: monitor, mouse e teclado

        sadd pesquisa:produto monitor mouse teclado

3. Visualizar a quantidade de valores da chave

        scard pesquisa:produto

4. Retornar todos os elementos da chave

        smembers pesquisa:produto
        
        -- veja que o set não é ordenado

5. Verificar se existe o valor monitor

        sismember pesquisa:produto monitor

6. Remover o valor monitor

        srem pesquisa:produto monitor

7. Recuperar um elemento e remove-lo do set

        spop pesquisa:produto
        
        -- o set não tem ordenação, remove qualquer item

8. Criar a chave "pesquisa:desconto“ do tipo set com os seguintes valores: memória RAM, monitor, teclado, HD

        sadd pesquisa:desconto 'memória RAM' monitor teclado HD

9. Próximas questões fazem uso dos sets pesquisa:produto e pesquisa:desconto

Visualizar a interseção entre os 2 sets

        sinter pesquisa:produto pesquisa:desconto
        
Visualizar a diferença entre os 2 sets

        sdiff pesquisa:produto pesquisa:desconto
        
Criar o set "pesquisa:produto_desconto" com a união entre os 2 sets

        sunion pesquisa:produto pesquisa:desconto
        -- assim mostra valores
        
        -- para criar um novo set, adicionar store e o nome da nova chave
        sunionstore pesquisa:produto_desconto pesquisa:produto pesquisa:desconto
        
        -- para visualizar a nova chave
        smembers pesquisa:produto_desconto
        
        
