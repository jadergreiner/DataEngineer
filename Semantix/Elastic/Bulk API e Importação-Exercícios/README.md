# Bulk API e Importação

1 . Importar os dados na Guia Arquivos para os índices

### - Índice: concessionaria2
  - dataset/cars.bulk
  
<img src = "i1.gif"> 
<br>

### - Índice: populacao

  - dataset/populacaoLA.csv
<br>
<img src = "i2.gif"> 
<br>
  
2 . Executar as consultas

- Contar o número de documentos de cada um dos novos índices

      GET populacao/_count

      GET concessionaria/_count

- Mostrar todos os documentos de cada um dos novos índices
      
      GET populacao/_search

      GET concessionaria/_search
      
      -- notar que nem todos os documentos são exibidos. Verificare sobre a paginação dos resultados em outros exemplos.

### Vídeo demonstrativo
<img src = "i3.gif">

