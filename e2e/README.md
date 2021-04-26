# End-to-end testing setup

Spin up a single node Elasticsearch cluster including Kibana to perform end-to-end testing.

Elasticsearch is available at http://localhost:9200/ and Kibana at http://localhost:5601.

## How to

Spin up the test stack:

```
docker compose up --build
```

Once it is done, configure kishell to be able to query from the local stack.

First, we need to configure the server:
```
/kishell --configure server
```
```
    Server name: local
    Protocol: http
    Hostname: localhost
    Port: 5601
    Username: 
    Password: 
    Kibana Version: 6.8.6
    Set as default? [Y/n]: 
```
Once the server is known, configure the role:
```
/kishell --configure role
```
```
    Role name: local
    Index name: logstash-*
    Window filter time (e.g. @timestamp, modified_date): @timestamp
    Set as default? [Y/n]: 
```

Now it is possible to query the data with a known expected result thanks to the data loaded on the local stack.

```
./kishell search --newer="8760h" --query="clientip:172.155.107.128"
```