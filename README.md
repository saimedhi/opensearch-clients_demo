# OpenSearch_clients_demo

## Welcome!

### What is OpenSearch?
OpenSearch is a scalable, flexible, and extensible open-source software suite for search, analytics, and observability applications.
[opensearch documentation](https://opensearch.org/)

### Why do we need OpenSearch Clients?
OpenSearch Clients provides a safer and easier way to interact with your OpenSearch cluster. Rather than using OpenSearch from the browser and potentially exposing your data to the public, you can build an OpenSearch client that takes care of sending requests to your cluster. OpenSearch client contains a library of APIs that let you perform different operations on your cluster and return a standard response body. 



### Installing OpenSearch

First install [docker](https://docs.docker.com/get-docker/).

To run OpenSearch in a docker container, use the following commands in terminal and for detailed explanation go through the [Installation guide](https://opensearch.org/docs/latest/install-and-configure/install-opensearch/index/).

```javascript

docker pull opensearchproject/opensearch:latest

docker run -d -p 9200:9200 -p 9600:9600 -e "discovery.type=single-node" opensearchproject/opensearch:latest

curl https://localhost:9200 -ku 'admin:admin'
```

### Opensearch Clients Userguide
OpenSearch provides clients in [JavaScript](https://github.com/opensearch-project/opensearch-js), [Python](https://github.com/opensearch-project/opensearch-py), [Ruby](https://github.com/opensearch-project/opensearch-ruby), [Java](https://github.com/opensearch-project/opensearch-java), [PHP](https://github.com/opensearch-project/opensearch-php), [.NET](https://opensearch.org/docs/latest/clients/OpenSearch-dot-net/), [Go](https://github.com/opensearch-project/opensearch-go) and [Rust](https://github.com/opensearch-project/opensearch-rs). 
OpenSearch language clients documentation can be found [here](https://opensearch.org/docs/latest/clients/index/).

- For example code, go through the "USER_GUIDE" in client repos.
- Initialize a client and use it as shown in the example.


### Contributing to OpenSearch
- First, go through the "CONTRIBUTING" file in the client repos.
- Pick an issue in the client repo or create a new one and raise a PR with solution for it.
- For testing the code locally, use commands in "DEVELOPER_GUIDE"  in the client repos.
