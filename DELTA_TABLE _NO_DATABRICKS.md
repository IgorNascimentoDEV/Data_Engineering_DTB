# Delta Table no Databricks

## Índice
01. Introdução ao Delta Lake\
02. Arquitetura Interna de uma Delta Table\
   2.1 Arquivos Parquet\
   2.2 Transaction Log (\_delta_log)
03. Conceito de ACID no Delta Lake\
04. Versionamento e Time Travel\
05. Comandos de Inpeção
06. Consultando Versões Específicas\
07. Criação de Views com Versionamento\
08. DELETE e Comportamento Interno\
09. RESTORE TABLE\
10. Comandos de %fs no Databricks\
11. Fluxo Interno de Funcionamento do Delta Lake

-----------------------------------------------------------

# 1. Introdução ao Delta Lake

Delta Lake é uma camada de armazenamento que adiciona confiabilidade e governança sobre arquivos Parquet em Data Lakes.

Ele oferece:

-   Trasanções ACID
-   Vercionamento automático
-   Time Travel
-   Schema Enforcement
-   Schema Evolution
-   Histórico de operações

No databricks, uma tabela Delta é armazenada fisicamente como arquivos Parquet, mas controlada por um log transacional.

-----------------------------------------------------------

# 2. Arquitetura Interna de uma Delta Table

uma Delta Table é composta por:

-   Arquivos de dados (Parquet)
-   Diretório especial chamado \_delta_log

## 2.1 Arquivos Parquet

Os dados são armazenados em formato colunar (.parquet).

Exemplo de estrutura física:

/mnt/dados/tabela/ part-0000.parquet part-0001.parquet \_delta_log/

Cada operação pode gerar novos arquivos parquet.

## 2.2 Transaction Log (\_delta_log)

Dentro da pasta da tabela existe o diretório:

\_delta_log/

Ele contém arquivos como:

000000.json 000001.json 000002.json 000003.checkpoint.parquet

Cada arquivo JSON representa um commit.

O log registra:

-   Inserções
-   Atualizações
-   Deleções
-   Alterações de schema
-   Operações de restore

Esse log perimete recontruir qualquer versção da tabela.

-----------------------------------------------------------

