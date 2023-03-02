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
- Initialize a client and use it as shown in the USER_GUIDE example.
- Below code is a demo script for the OpenSearch javascript client.

```javascript
// Description: This is a demo script to show how to use the OpenSearch client.
// Usage: node demo.js

'use strict';

var host = 'localhost';
var protocol = 'https';
var port = 9200;
var auth = 'admin:admin'; // For testing only. Don't store credentials in code.
var ca_certs_path = '/full/path/to/root-ca.pem';

// Optional client certificates if you don't want to use HTTP basic authentication.
// var client_cert_path = '/full/path/to/client.pem'
// var client_key_path = '/full/path/to/client-key.pem'

// Create a client with SSL/TLS enabled.
var { Client } = require('@opensearch-project/opensearch');
var fs = require('fs');
var client = new Client({
  node: protocol + '://' + auth + '@' + host + ':' + port,
  ssl: {
    rejectUnauthorized: false
    //ca: fs.readFileSync(ca_certs_path),
    // You can turn off certificate verification (rejectUnauthorized: false) 
    //if you're using self-signed certificates with a hostname mismatch.
    // cert: fs.readFileSync(client_cert_path),
    // key: fs.readFileSync(client_key_path)
  },
});

async function main() {


// Creating an index
console.log('Creating index:');

var index_name = 'books';
var settings = {
  settings: {
    index: {
      number_of_shards: 4,
      number_of_replicas: 3,
    },
  },
};

var response = await client.indices.create({
  index: index_name,
  body: settings,
});

console.log(response.body);


// Adding a document

console.log('Adding document:');

var document = {
  title: 'The Outsider',
  author: 'Stephen King',
  year: '2018',
  genre: 'Crime fiction',
};

var id = '1';

var response = await client.index({
  id: id,
  index: index_name,
  body: document,
  refresh: true,
});

console.log(response.body);


// Searching for a document

console.log('Search results:');

var query = {
  query: {
    match: {
      title: {
        query: 'The Outsider',
      },
    },
  },
};

var response = await client.search({
  index: index_name,
  body: query,
});

console.log(response.body.hits);
  


// Deleting a document

console.log('Deleting document:');

var response = await client.delete({
  index: index_name,
  id: id,
});

console.log(response.body);



// Deleting an index

console.log('Deleting index:');
var index_name = 'books';
var response = await client.indices.delete({
index: index_name,
});

console.log(response.body);


}

main();
```

### Contributing to OpenSearch
- First, go through the "CONTRIBUTING" file in the client repos.
- Pick an issue in the client repo or create a new one and raise a PR with solution for it.
- For testing the code locally, use commands in "DEVELOPER_GUIDE"  in the client repos.


### Demo Video
https://user-images.githubusercontent.com/117196660/222495715-79521c50-63a9-40ba-82b6-f8932dd1bde1.mp4

