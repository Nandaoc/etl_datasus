# ETL DataSUS

## Objetivo
Este repositório tem como objetivo armazenar e versionar o código desenvolvido para realização do processo de Extração, Transformação e Carregamento (ETL) de dados obtidos através do [DataSUS](https://datasus.saude.gov.br/transferencia-de-arquivos/), repositório de dados públicos de saúde do Ministério da Saúde do Brasil.

É importante observar que aqui utilizou-se o dataset "CNES", mas o código apresentado pode ser utilizado para quaisquer datasets do DataSUS, desde que se importe a biblioteca correspondente do pysus.

## Ambiente
O código apresentado foi desenvolvido em linguagem [Python](https://www.python.org/downloads/) (3.11.7) utilizando o Jupyter Notebook no Ubuntu 22.04 LTS.

## Bibliotecas
Para rodar este código, instale e importe as seguintes bibliotecas: 
1. [pysus](https://pysus.readthedocs.io/en/latest/databases/CNES.html);
2. [psycopg2](https://pypi.org/project/psycopg2/);
3. [sqlalchemy](https://www.sqlalchemy.org/);
4. [os](https://docs.python.org/3/library/os.html);
5. [shutil](https://docs.python.org/pt-br/3/library/shutil.html);
6. [time](https://docs.python.org/3/library/time.html).

Para instalar as bibliotecas, basta usar:
``` pip install [NOME_BIBLIOTECA] ```

## Funções
1. extracao_cnes_leitos(uf, ano, mes=[1,2,3,4,5,6,7,8,9,10,11,12]):
  Esta função recebe como parâmetros o estado, o ano e os meses (em formato de lista) e retorna os arquivos que estão disponíveis no servidor FTP do DataSUS.
  ```arquivos_dbc = extracao_cnes_leitos('AC', 2023, [1,2])```
2. geracao_nomes_dataframes(arquivos):
  Esta função é utilizada para extrair os nomes dos arquivos que serão usados, posteriormente, para armazenar os DataFrames gerados a partir dos arquivos.
  ```nomes = geracao_nomes_dataframes(arquivos)```
3. download_cnes_leitos(arquivos):
  Esta função recebe os arquivos obtidos do servidor FTP do DataSUS e realiza o download dos mesmos. Esses arquivos ficam salvos com a extensão ".parquet" no diretório "pysus" que é automaticamente   criado na máuina.
  ```arquivos_parquet = download_cnes_leitos(arquivos)```
4. remove_arquivos():
  Esta função não recebe parâmetros e é utilizada para limpar o diretório "pysus" após os dados serem carregados no banco, sendo utilizada dentro de uma outra função.
   ```remove_arquivos()```
5. parquet_para_dataframe(arquivos_parquet, nomes_arquivos)
  Esta função converte os arquivos ".parquet" em DataFrame, retornando uma lista com dicionários que contém os DataFrames e cujas chaves são os nomes dos arquivos sem sua extensão.
  ```dataframes = parquet_para_dataframe(arquivos_parquet, nomes)```
6. concexao_bancopg(host, porta, banco, usuario, senha):
  Esta função recebe as credencias de acesso a um banco de dados PostgreSQL e retorna uma string de conexão ao banco.
  ```conexao = concexao_bancopg('meu_host', 'porta', 'banco_dados', 'meu_usuario', 'minha_senha')```
7. insercao_dados(tabela, conexao, dataframes):
  Esta função recebe o nome da tabela do banco na qual os dados serão persistidos (ela não precisa existir no banco), a string de conexão e a lista de dataframes que devem ser carregados. Além        disso, após 3 segundos da carga dos dados, esta função executa a remove_arquivos() para limpar o diretório "pysus".
  ```insercao_dados('nome_tabela_banco', conexao, dataframes)```
