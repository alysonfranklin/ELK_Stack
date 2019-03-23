##### Elasticsearch:
O ElasticSearch é uma engine de busca com foco na análise de dados em tempo real, baseado na arquitetura RESTful.
ElasticSearch é um backend NoSQL baseado no Apache Lucene.

##### Logstash:
O Logstash é uma solução para gerenciamento e agregação de logs. O formato estruturado do JSON é o padrão, e também é a forma como o ElasticSearch vai tratá-lo. Existem diversas opções de filtros e funcionalidades similares que você pode experimentar. É muito útil para agilizar a leitura dos logs, compreensão e filtragem.

##### Kibana:
O Kibana é o frontend do nosso stack, que irá apresentar os dados armazenados pelo Logstash no ElasticSearch, em uma interface altamente customizável com histograma e outros painéis que irão te dar um excelente overview sobre os seus dados. Muito bom para análises em tempo real e pesquisa de dados que você tenha parseado no ElasticSearch. 

Ele permite transformar os logs em informações úteis, pois permite realizar correlação de eventos, filtrar logs por origem, hosts, e N outras combinações.

## Beats: 
Beats são uma família de transportadores leves que enviam dados de edge machines (ou máquinas de “borda”) para o Elasticsearch.
##### MetricBeat:
Colete métricas de seus sistemas e serviços. Da CPU à memória, do Redis ao NGINX e muito mais, o Metricbeat é uma maneira leve de enviar estatísticas de sistema e serviço.

## RabbitMQ:
RabbitMQ é um servidor de mensageria de código aberto (open source) desenvolvido em Erlang, implementado para suportar mensagens em um protocolo denominado Advanced Message Queuing Protocol (AMQP). Ele possibilita lidar com o tráfego de mensagens de forma rápida e confiável, além de ser compatível com diversas linguagens de programação, possuir interface de administração nativa e ser multiplataforma.

### Resumindo toda Stack:
A aplicação envia o log para o RabbitMQ (Pode ser um Beats ou Syslog-ng lendo log da aplicação e enviando pro RabbitMQ).\
Logstash fica escutando a fila de logs do RabbitMQ e grava no ElasticSearch e confirma que a mensagem foi persistida.\
Kibana reprocessa as queries que são exibidas em seus boards - Gráfico e Consultas são atualizados na tela do usuário.

#### Como usar:
git clone https://github.com/alysonfranklin/ELK_Stack.git \
cd ELK_Stack \
docker-compose up

###### Credenciais do RabbitMQ:
http://localhost:15672/ \
User: guest \
Password: 123qwe \
No RabbitMQ clique em Queues e sem seguida clique na fila DevOps. \
No campo Payload você pode colar um log ou texto qualquer em json \
para ver a mensagem sendo consumida pelo logstash e o mesmo postando no elasticsearch.

Json de exemplo: \
{
	"age":100, \
	"name":"mkyong.com", \
	"messages":["msg 1","msg 2","msg 3"] \
}

###### URL do Kibana: 
http://localhost:5601

###### URL do Elasticsearch:
http://localhost:9200 \

## Dashboards

![alt text](https://i.imgur.com/tuaOiRh.png)

![alt text](https://i.imgur.com/BK5t8R9.png)

![alt text](https://i.imgur.com/EPaxONg.png)

![alt text](https://i.imgur.com/IZYvYOt.png)
