# ETL DataSUS

## Objetivo
Este repositório tem como objetivo armazenar e versionar o código desenvolvido para realização do processo de Extração, Transformação e Carregamento (ETL) de dados obtidos através do [DataSUS](https://datasus.saude.gov.br/transferencia-de-arquivos/), repositório de dados públicos de saúde do Ministério da Saúde do Brasil.

## Ambiente
O código apresentado foi desenvolvido em linguagem [Python](https://www.python.org/downloads/) (3.11.7) utilizando o Jupyter Notebook no Ubuntu 22.04 LTS.

## Bibliotecas
Para rodar este código, instale e importe as seguintes bibliotecas: 
1. [pysus](https://pysus.readthedocs.io/en/latest/databases/CNES.html):
2. [psycopg2](https://pypi.org/project/psycopg2/):
3. [sqlalchemy](https://www.sqlalchemy.org/):
4. [os](https://docs.python.org/3/library/os.html):
5. [shutil](https://docs.python.org/pt-br/3/library/shutil.html)
6. [time](https://docs.python.org/3/library/time.html)

Para instalar as bibliotecas, basta usar:
```pip install [NOME_BIBLIOTECA]```
