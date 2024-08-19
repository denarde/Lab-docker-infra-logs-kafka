# Pipeline de Logs do Nginx com Fluentbit, Kafka, Kafka Manager, Logstash, Elasticsearch e Kibana

Este repositório contém um lab prático que demonstra a configuração de um pipeline de logging utilizando Docker, Nginx, Fluentbit, Kafka, Logstash, Elasticsearch e Kibana (ELK stack). O objetivo é capturar logs de acesso e erro do Nginx e enviá-los para um tópico Kafka, consumi-los com Logstash, armazená-los no Elasticsearch, e visualizá-los no Kibana.

## Arquitetura

- **Nginx**: Servidor web que gera logs de acesso e erro.
- **Fluentbit**: Agente de coleta de logs que lê os logs do Nginx e os envia para o Kafka.
- **Kafka**: Sistema de mensagens que atua como intermediário para os logs, permitindo que diferentes sistemas os consumam.
- **Logstash**: Pipeline de processamento de dados que consome os logs do Kafka e os envia para o Elasticsearch.
- **Elasticsearch**: Banco de dados de busca e análise que armazena os logs.
- **Kibana**: Ferramenta de visualização de dados que permite explorar os logs armazenados no Elasticsearch.
- **Kafka Manager**: Interface web para gerenciar e monitorar o Kafka.

## Requisitos

- Docker e Docker Compose instalados no sistema.

## Configuração

- **Nginx**: O Nginx é configurado para expor os logs de acesso e erro. Esses logs são montados no contêiner nginx para serem acessados pelo Fluentd.
- **Fluentbit**: O Fluentbit é configurado para ler os logs do Nginx e enviá-los para o Kafka usando o plugin do kafka. Tanto os logs de acesso quanto os de erro são enviados para o mesmo tópico no Kafka.
- **Kafka**: Configurado para receber os logs do Fluentbit. A variável `KAFKA_ADVERTISED_LISTENERS` é configurada para garantir que o Kafka esteja acessível aos outros contêineres.
- **Logstash**: Configurado para consumir logs do Kafka e enviá-los para o Elasticsearch.
- **Elasticsearch e Kibana**: Elasticsearch armazena os logs, e Kibana é usado para visualizá-los.
- **Kafka Manager**: Ferramenta para gerenciar e monitorar o Kafka.

## Como Usar

1. Inicie os serviços com Docker Compose:
    ```bash
    docker-compose up -d
    ```

2. Acesse o Kafka Manager em [http://localhost:9000](http://localhost:9000) para gerenciar e monitorar os tópicos Kafka.

3. Acesse o Kibana em [http://localhost:5601](http://localhost:5601) para visualizar os logs no Elasticsearch.

4. Para verificar os logs:
   - **Nginx**: Acesse [http://localhost:8080](http://localhost:8080) para gerar tráfego e criar logs.
   - **Fluentbit**: Verifique se os logs estão sendo enviados para o Kafka.
   - **Logstash**: Verifique se os logs estão sendo consumidos do Kafka e enviados para o Elasticsearch.


