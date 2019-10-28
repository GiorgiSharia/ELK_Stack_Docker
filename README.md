# ELK_Stack_Docker
In order to run the system, do "docker-compose up". It will automatically download necessary images. In order to access kibana navigate to localhost:5601. Credentials are username:elastic and password:notagoodpasswod. In order to test the hole pipeline (second logstash is not configured, thus it goes from source->logstash->elasticsearch->kibana), run command "nc localhost 5000 ./log/dummy.log". Using netcat utility this will send dummy.log files to tcp port 5000.


Whole system consists of elasticsearch (7.4.1), kibana (7.4.1) and two logstashes (7.4.1). They all are put in the same bridged network - elastic. Elasticsearch is mapped to port 9200. Logstash is configured to listen to tcp port 5000. It outputs to elasticsearch:9200 with an index "logstash-2019.10.27-000001". Note that index will be created only after logs will reach elasticsearch.

In order to view logs in kibana, after running the command to put logs to logstash navigate to management->kibana->Index Patterns and create new kibana index to match existing elasticsearch index. Example index name -  "logstash*". In the next window for filtering select @timestamp from dropdown menu and press create index pattern. Navigate to Discover tab to see the logs.
