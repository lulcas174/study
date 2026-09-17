### Arquitetura da Solução

#### Fluxo dos Dados e Componentes

1. **Origem (Mock):** Um script Python local (usando a biblioteca `Faker`) gera dois tipos de dados:
    
    - _Batch:_ Perfis de clientes e contas (salvos em um banco PostgreSQL local ou arquivos CSV no S3/DBFS).
        
    - _Streaming:_ Eventos de transações (enviados para um cluster **Apache Kafka** local via Docker).
        
2. **Ingestão (Bronze):** O Databricks consome o Kafka (Structured Streaming) e os dados relacionais (Batch), salvando tudo em formato Delta (Raw) no DBFS (Databricks File System).
    
3. **Transformação (Silver):** Limpeza, tipagem, desduplicação e o Join entre as transações (Stream) e o cadastro do cliente (Batch).
    
4. **Agregação (Gold):** Janelas de tempo (Tumbling/Sliding Windows) calculando métricas como "Total gasto na última hora por cliente", sinalizando anomalias baseadas em regras de negócio.