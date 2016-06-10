##Install Marvel [Marvel | Monitor Elasticsearch](https://www.elastic.co/products/marvel)

Documentation [html](https://www.elastic.co/guide/en/marvel/current/index.html)

Install marvel by command line:

<pre>
 plugin -i elasticsearch/marvel/latest
</pre>

To access by url:
http://localhost:9200/_plugin/marvel/sense/index.html

###Other options:

Sense (Beta) is a plugin for Google Chrome [chrome web store](https://chrome.google.com/webstore/detail/sense-beta/lhjgkmllcaadmopgmanpapmpjgmfcfig)

Get mapping from an index (playlist example)
<pre>
    GET playlist/_mapping
</pre>


Delete an index
<pre>
    DELETE /playlist/
</pre>

Match by name (mysql "like") ([match](https://www.elastic.co/guide/en/elasticsearch/reference/1.4/query-dsl-match-query.html))

<pre>
GET playlist/_search
{
  "query": {
    "match": {
      "name": "wish"
    }
  }
}
</pre>

Query limit 0,2 ([from/size](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-request-from-size.html))

<pre>
GET playlist/_search
{
  "from" : 0, "size" : 2, 
  "query": {
    "match": {
      "name": "Rock"
    }
  }
}
</pre>

Contains "Rock" and not "About" and not "Cherub"... ([bool](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-bool-query.html))

<pre>
GET playlist/_search
{
  "from" : 0, "size" : 10, 
  "query": {
    "bool": {
      "must": { "match": { "name": "Rock" }},
      "must_not": { "match": { "name":  "About" }},
      "must_not": { "match": { "name":  "Cherub" }},
      "must_not": { "match": { "name":  "Ages" }}
    }
  }
}
</pre>

Contains "Rock" and not "Music" in playListName

<pre>
GET playlist/_search
{
  "from" : 0, "size" : 100, 
  "query": {
    "bool": {
      "must": { "match": { "name": "Rock" }},
      "must_not": { "match": { "playListName":  "Music" }}
    }
  }
}
</pre>

##Filter

id = 5 ([Term](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-terms-query.html))

<pre>
GET playlist/_search
{
  "query": {
    "term": {
      "id": 5
    }
  }
}

</pre>

Mysql "in" 

<pre>
GET playlist/_search
{
  "query": {
    "terms": { "id": [2, 4, 100] }
  }
}
</pre>

Range ([Ranges](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-range-query.html))

<pre>
GET playlist/_search
{
  "query": {
    "filtered": {
      "filter": {
        "range": {
          "album.id": {
            "gt":  2,
            "lte": 5
          }
        }
      }
    }
  }
}
</pre>

Order ([sorting]())

<pre>
GET playlist/_search?from=0&size=20
{
  "from" : 0, "size" : 20, 
  "query": {
    "match_all": {}
  },
  "sort": {"id":{"order":"asc"}}
}
</pre>

