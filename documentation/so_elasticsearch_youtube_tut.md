
[Python and Elasticsearch](https://www.bing.com/videos/search?q=elasticsearch-py+tutorial&view=detail&mid=38BF6563D4D78074BC0738BF6563D4D78074BC07&FORM=VIRE)
Date histogram 11min 18sec

[Elasticsearch DSL - Honza Kral](https://www.bing.com/videos/search?q=elasticsearch-py+tutorial&&view=detail&mid=5600FB18BE79857AAC575600FB18BE79857AAC57&&FORM=VDRVRV)
```python
from elasticsearch_dsl import Search, Q

#create Search, bind it to client
s = Search(using=es)

#querying twicen will combine queries
# or combine manually: s.query( Q() & ~Q() )
s = s.query( 'match', title='python').query( ~Q('match', title='ruby ) )

# filter will turin it to filtered query
s = s.filter('range', creation_date={ "from": date(2012, 1, 1)})

# get a fance result object
result = s.execute() 

```

### Q/F/A --> shortcuts for Queries/Filters/Aggregations
```python
Q('match', title='python') == Match(title='python') == Q( {match: {title: 'python'} } )

# boolean
Q(1) & Q(2) == Q('bool', must=[ Q(1), Q(2) ])
Q(1) | Q(2) | Q(3) == Q('bool', should=[ Q(1), Q(2), Q(3) ])
~F(1) == F('bool', must=[F(1)])
```

### Chaining
```python
#copy is made in each change
s2 = s1.query( Q(1) )
s1 != s2

#same for other methods
s[0:10], s.using(es), s.index('today', 'yesterday'), ...

#except Aggs
s.aggs.bucket('per_tag').metric('avg).metric('max')
s.aggs.bucket('per_country').bucket('per_tag'), metric('avg')
s.aggs['per_country'].metric(...)
```

### Response
```python
# response object is returned;
response = s.execute()
if not response.success(): print("partial result")

#iterate over iterate
for h in response:
	print(h._meta.id, h.title)
	
#Aggregations can be assessed
top_tag = response.aggregations.per_tag.bucker[0]
```