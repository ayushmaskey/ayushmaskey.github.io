# py elastic

References
 * [Elasticsearch DLS](https://elasticsearch-dsl.readthedocs.io/en/latest/)
 * [Elasticsearch py](https://elasticsearch-py.readthedocs.io/en/master/)
 * [tryolabs](https://tryolabs.com/blog/2015/02/17/python-elasticsearch-first-steps/)
 * [bitquabit](https://bitquabit.com/post/having-fun-python-and-elasticsearch-part-1/)
 * [qbox](https://qbox.io/blog/python-scripts-interact-elasticsearch-examples)
 * [analyticsvidhya](https://www.analyticsvidhya.com/blog/2017/05/beginners-guide-to-data-exploration-using-elastic-search-and-kibana/)
 * [macrobonzanini](https://marcobonzanini.com/2015/02/02/how-to-query-elasticsearch-with-python/)


```bash
# status of elastic
curl -XGET localhost:9200/

# all indices
curl http://localhost:9200/_aliases?pretty=1 

# indices with health and size
curl 'localhost:9200/_cat/indices?v'

```


* connection to elastic from host3 - done
* connection to elastic from outside - ufw
* create connection
* loop over list of indices 
  * increment by date
    * something index missing for a date - handle exeception
    * there should be something easier
  * each index find all the available doc_types
  * need to get time - total traffic in some time interval
