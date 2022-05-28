# Sqoop - Importação BD Employees- Otimização

Realizar com uso do MySQL

1 . Criar a tabela cp_titles_date, contendo a cópia da tabela titles com os campos title e to_date

2 . Pesquisar os 15 primeiros registros da tabela cp_titles_date

3 . Alterar os registros do campo to_date para null da tabela cp_titles_date, quando o título for igual a Staff

Realizar com uso do Sqoop - Importações no warehouse /user/hive/warehouse/db_test_<numero_questao> e visualizar no HDFS

4 . Importar a tabela titles com 8 mapeadores no formato parquet

5 . Importar a tabela titles com 8 mapeadores no formato parquet e compressão snappy

6 . Importar a tabela cp_titles_date com 4 mapeadores (erro)

Importar a tabela cp_titles_date com 4 mapeadores divididos pelo campo título no warehouse /user/hive/warehouse/db_test2_title
Importar a tabela cp_titles_date com 4 mapeadores divididos pelo campo data no warehouse /user/hive/warehouse/db_test2_date
Qual a diferença dos registros nulos entre as duas importações?
