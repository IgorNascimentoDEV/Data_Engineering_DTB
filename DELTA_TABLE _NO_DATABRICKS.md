# Delta Table no Databricks

## Índice
1. Introdução ao Delta Lake\
2. Arquitetura Interna de uma Delta Table\
   2.1 Arquivos Parquet\
   2.2 Transaction Log (\_delta_log)
3. Conceito de ACID no Delta Lake\
4. Versionamento e Time Travel\
5. Comandos de Inpeção
6. Consultando Versões Específicas\
7. Criação de Views com Versionamento\
8. DELETE e Comportamento Interno\
9. RESTORE TABLE\
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
