# 24 hour - total traffic
 * request
 * response
 * statistics
 * table

> request
```json
{
  "size": 0,
  "aggs": {
    "2": {
      "date_histogram": {
        "field": "@timestamp",
        "interval": "30m",
        "time_zone": "Pacific/Honolulu",
        "min_doc_count": 1
      }
    }
  },
  "version": true,
  "query": {
    "bool": {
      "must": [
        {
          "query_string": {
            "query": "*",
            "analyze_wildcard": true
          }
        },
        {
          "range": {
            "@timestamp": {
              "gte": 1521353712139,
              "lte": 1521440112139,
              "format": "epoch_millis"
            }
          }
        }
      ],
      "must_not": []
    }
  },
  "_source": {
    "excludes": []
  },
  "highlight": {
    "pre_tags": [
      "@kibana-highlighted-field@"
    ],
    "post_tags": [
      "@/kibana-highlighted-field@"
    ],
    "fields": {
      "*": {
        "highlight_query": {
          "bool": {
            "must": [
              {
                "query_string": {
                  "query": "*",
                  "analyze_wildcard": true,
                  "all_fields": true
                }
              },
              {
                "range": {
                  "@timestamp": {
                    "gte": 1521353712139,
                    "lte": 1521440112139,
                    "format": "epoch_millis"
                  }
                }
              }
            ],
            "must_not": []
          }
        }
      }
    },
    "fragment_size": 2147483647
  }
}
```

> response

```json
{
  "took": 448,
  "timed_out": false,
  "_shards": {
    "total": 142,
    "successful": 142,
    "skipped": 134,
    "failed": 0
  },
  "hits": {
    "total": 7437143,
    "max_score": 0,
    "hits": []
  },
  "aggregations": {
    "2": {
      "buckets": [
        {
          "key_as_string": "2018-03-17T20:00:00.000-10:00",
          "key": 1521352800000,
          "doc_count": 74152
        },
        {
          "key_as_string": "2018-03-17T20:30:00.000-10:00",
          "key": 1521354600000,
          "doc_count": 148721
        },
        {
          "key_as_string": "2018-03-17T21:00:00.000-10:00",
          "key": 1521356400000,
          "doc_count": 150616
        },
        {
          "key_as_string": "2018-03-17T21:30:00.000-10:00",
          "key": 1521358200000,
          "doc_count": 148285
        },
        {
          "key_as_string": "2018-03-17T22:00:00.000-10:00",
          "key": 1521360000000,
          "doc_count": 150141
        },
        {
          "key_as_string": "2018-03-17T22:30:00.000-10:00",
          "key": 1521361800000,
          "doc_count": 147748
        },
        {
          "key_as_string": "2018-03-17T23:00:00.000-10:00",
          "key": 1521363600000,
          "doc_count": 208689
        },
        {
          "key_as_string": "2018-03-17T23:30:00.000-10:00",
          "key": 1521365400000,
          "doc_count": 177763
        },
        {
          "key_as_string": "2018-03-18T00:00:00.000-10:00",
          "key": 1521367200000,
          "doc_count": 172674
        },
        {
          "key_as_string": "2018-03-18T00:30:00.000-10:00",
          "key": 1521369000000,
          "doc_count": 157715
        },
        {
          "key_as_string": "2018-03-18T01:00:00.000-10:00",
          "key": 1521370800000,
          "doc_count": 162669
        },
        {
          "key_as_string": "2018-03-18T01:30:00.000-10:00",
          "key": 1521372600000,
          "doc_count": 153931
        },
        {
          "key_as_string": "2018-03-18T02:00:00.000-10:00",
          "key": 1521374400000,
          "doc_count": 155510
        },
        {
          "key_as_string": "2018-03-18T02:30:00.000-10:00",
          "key": 1521376200000,
          "doc_count": 149995
        },
        {
          "key_as_string": "2018-03-18T03:00:00.000-10:00",
          "key": 1521378000000,
          "doc_count": 159533
        },
        {
          "key_as_string": "2018-03-18T03:30:00.000-10:00",
          "key": 1521379800000,
          "doc_count": 157222
        },
        {
          "key_as_string": "2018-03-18T04:00:00.000-10:00",
          "key": 1521381600000,
          "doc_count": 154633
        },
        {
          "key_as_string": "2018-03-18T04:30:00.000-10:00",
          "key": 1521383400000,
          "doc_count": 153136
        },
        {
          "key_as_string": "2018-03-18T05:00:00.000-10:00",
          "key": 1521385200000,
          "doc_count": 154600
        },
        {
          "key_as_string": "2018-03-18T05:30:00.000-10:00",
          "key": 1521387000000,
          "doc_count": 150693
        },
        {
          "key_as_string": "2018-03-18T06:00:00.000-10:00",
          "key": 1521388800000,
          "doc_count": 147539
        },
        {
          "key_as_string": "2018-03-18T06:30:00.000-10:00",
          "key": 1521390600000,
          "doc_count": 152485
        },
        {
          "key_as_string": "2018-03-18T07:00:00.000-10:00",
          "key": 1521392400000,
          "doc_count": 157071
        },
        {
          "key_as_string": "2018-03-18T07:30:00.000-10:00",
          "key": 1521394200000,
          "doc_count": 152906
        },
        {
          "key_as_string": "2018-03-18T08:00:00.000-10:00",
          "key": 1521396000000,
          "doc_count": 159941
        },
        {
          "key_as_string": "2018-03-18T08:30:00.000-10:00",
          "key": 1521397800000,
          "doc_count": 151560
        },
        {
          "key_as_string": "2018-03-18T09:00:00.000-10:00",
          "key": 1521399600000,
          "doc_count": 152258
        },
        {
          "key_as_string": "2018-03-18T09:30:00.000-10:00",
          "key": 1521401400000,
          "doc_count": 153012
        },
        {
          "key_as_string": "2018-03-18T10:00:00.000-10:00",
          "key": 1521403200000,
          "doc_count": 155652
        },
        {
          "key_as_string": "2018-03-18T10:30:00.000-10:00",
          "key": 1521405000000,
          "doc_count": 151871
        },
        {
          "key_as_string": "2018-03-18T11:00:00.000-10:00",
          "key": 1521406800000,
          "doc_count": 150641
        },
        {
          "key_as_string": "2018-03-18T11:30:00.000-10:00",
          "key": 1521408600000,
          "doc_count": 151640
        },
        {
          "key_as_string": "2018-03-18T12:00:00.000-10:00",
          "key": 1521410400000,
          "doc_count": 184444
        },
        {
          "key_as_string": "2018-03-18T12:30:00.000-10:00",
          "key": 1521412200000,
          "doc_count": 151574
        },
        {
          "key_as_string": "2018-03-18T13:00:00.000-10:00",
          "key": 1521414000000,
          "doc_count": 156616
        },
        {
          "key_as_string": "2018-03-18T13:30:00.000-10:00",
          "key": 1521415800000,
          "doc_count": 153192
        },
        {
          "key_as_string": "2018-03-18T14:00:00.000-10:00",
          "key": 1521417600000,
          "doc_count": 155788
        },
        {
          "key_as_string": "2018-03-18T14:30:00.000-10:00",
          "key": 1521419400000,
          "doc_count": 148545
        },
        {
          "key_as_string": "2018-03-18T15:00:00.000-10:00",
          "key": 1521421200000,
          "doc_count": 153113
        },
        {
          "key_as_string": "2018-03-18T15:30:00.000-10:00",
          "key": 1521423000000,
          "doc_count": 124773
        },
        {
          "key_as_string": "2018-03-18T16:00:00.000-10:00",
          "key": 1521424800000,
          "doc_count": 151742
        },
        {
          "key_as_string": "2018-03-18T16:30:00.000-10:00",
          "key": 1521426600000,
          "doc_count": 150572
        },
        {
          "key_as_string": "2018-03-18T17:00:00.000-10:00",
          "key": 1521428400000,
          "doc_count": 152613
        },
        {
          "key_as_string": "2018-03-18T17:30:00.000-10:00",
          "key": 1521430200000,
          "doc_count": 150832
        },
        {
          "key_as_string": "2018-03-18T18:00:00.000-10:00",
          "key": 1521432000000,
          "doc_count": 142393
        },
        {
          "key_as_string": "2018-03-18T18:30:00.000-10:00",
          "key": 1521433800000,
          "doc_count": 147948
        },
        {
          "key_as_string": "2018-03-18T19:00:00.000-10:00",
          "key": 1521435600000,
          "doc_count": 159218
        },
        {
          "key_as_string": "2018-03-18T19:30:00.000-10:00",
          "key": 1521437400000,
          "doc_count": 148710
        },
        {
          "key_as_string": "2018-03-18T20:00:00.000-10:00",
          "key": 1521439200000,
          "doc_count": 80068
        }
      ]
    }
  },
  "status": 200
}
```

> statistics
```json
Query Duration 	448ms
Request Duration 	554ms
Hits 	7437143
Index 	*:logstash-*
Id 	*:logstash-*
```

> table
```json
@timestamp per 30 minutes 	Count
March 17th 2018, 20:00:00.000	74,152
March 17th 2018, 20:30:00.000	148,721
March 17th 2018, 21:00:00.000	150,616
March 17th 2018, 21:30:00.000	148,285
March 17th 2018, 22:00:00.000	150,141
March 17th 2018, 22:30:00.000	147,748
March 17th 2018, 23:00:00.000	208,689
March 17th 2018, 23:30:00.000	177,763
March 18th 2018, 00:00:00.000	172,674
March 18th 2018, 00:30:00.000	157,715
```
