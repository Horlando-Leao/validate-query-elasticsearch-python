# validate-query-elasticsearch-python
validate query elasticsearch example with Python

I had a bit of trouble finding an implementation example, so since I did, I'll post it here to help.

```python
from elasticsearch import Elasticsearch

es = Elasticsearch(
    hosts=['localhost'],
    http_auth=('user-auth', 'pass-auth'),
    scheme=False,
    port=9200,
    verify_certs=True
)


query = {
    "query": {
        "bool": {
            "filter": [
                {
                    "query_string": {
                        "query": "Developer AND \"Systems Analyst\" AND (java OR python)",
                        "default_field": "github"
                    }
                }
            ]
        }
    }
}

query_string = "Developer AND \"Systems Analyst\" AND (java OR python)"

validate_dict = es.indices.validate_query(index='my-index-test', body=query, doc_type='doc')
print(validate_dict)

validate_string = es.indices.validate_query(index='my-index-test', q=query_string, doc_type='doc')
print(validate_string)
```
