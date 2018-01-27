

all DNS
{
  "query": {
    "multi_match": {
	  "query": "53",
	  "fields": ["dst_mapped_port", "src_mapped_port","src_port","dst_port"]
	}
  }
}
all printer
{
  "query": {
	"terms": {
		"dst_ip.keyword": [
			"10.0.95.31", "10.0.95.77", "10.0.95.235", "10.0.95.188", "10.0.95.180", "10.0.95.99", "10.0.95.230", "10.0.95.104", "10.0.95.137",
			"10.0.22.12", "10.0.22.10", "10.0.22.13", "10.0.22.43", "10.0.22.112", "10.0.22.14", "10.0.22.50",
			"10.0.13.200", "10.0.13.22", "10.0.13.228",
			"10.0.6.160", "10.0.6.150", "10.0.6.117", "10.0.19.201",
			"10.0.12.90", "10.0.12.22", "10.0.12.80",
			"10.0.18.210", "10.0.18.211", "10.0.18.212", "10.0.18.213", "10.0.18.215", "10.0.18.216", "10.0.18.217", "10.0.18.218",
			"10.0.0.70", "10.0.0.109", "10.0.0.221", "10.0.0.53", "10.0.0.241", "10.0.0.74", "10.0.0.88", "10.0.0.224", "10.0.0.110",
			"10.0.0.173", "10.0.0.121", "10.0.0.116",
			"10.0.0.92", "10.0.0.91", "10.0.0.175", "10.0.0.222", "10.0.0.113",
			"10.0.0.223", "10.0.0.243", "10.0.0.185"
		]
	}
  }
}
blocked traffic
{
  "query": {
    "match": {
      "message": {
        "query": "SFR requested to drop",
        "type": "phrase"
      }
    }
  }
}
hosts (11)
{
  "query": {
	"terms": {
		"dst_ip.keyword": [
			 "10.0.0.171", "10.0.18.52", "10.0.18.53", "10.0.18.43", "10.0.18.40", "10.0.18.42", 
			 "10.0.22.20", "10.0.18.50", "10.0.18.85", "10.0.18.86", "10.0.18.87"
		]
	}
  }
}
Servers Terminal (1,2,4,5,6,7,8,9,11)
{
  "query": {
	"terms": {
		"dst_ip.keyword": [
			"10.0.18.66", "10.0.18.65", "10.0.18.68", "10.0.18.69",  "10.0.18.71",
			"10.0.18.37", "10.0.18.24", "10.0.18.73",  "10.0.18.75"
		]
	}
  }
}
Servers Terminal (no scan)
{
  "query": {
	"terms": {
		"dst_ip.keyword": [
			"10.0.18.74", "10.0.18.76", "10.0.18.88", "10.0.18.89", "10.0.18.90", 
			"10.0.18.95", "10.0.18.96", "10.0.18.97", "10.0.18.98", "10.0.18.99"  
		]
	}
  }
}

			
server - apps1 (acct, lan02,03, app/01, cliniview, demo, dental, sql, i2i) (10)
{
  "query": {
	"terms": {
		"dst_ip.keyword": [
			"10.0.18.19", "10.0.18.35", "10.0.22.15", "10.0.18.54", "10.0.18.14", 
			"10.0.18.44", "10.0.18.140", "10.0.18.105", "10.0.18.58", "10.0.18.27"
		]
	}
  }
}			      
Servers Apps2 (doc, esm, qs1, snpp-ap, splunk,  sysaid, veeam, web, term02, warehouse)(10)
{
  "query": {
	"terms": {
		"dst_ip.keyword": [
			"10.0.18.16", "10.0.18.56", "10.0.18.26", "10.0.18.23", "10.0.18.36",
			"10.0.18.9",  "10.0.18.13", "10.0.18.154","10.0.0.15", "10.0.18.144"
		]
	}
  }
}
Servers Apps3 (skype, ca, subca, fax, train, SAN)(10)
{
  "query": {
	"terms": {
		"dst_ip.keyword": [
			"10.0.18.31", "10.0.18.17", "10.0.18.33", "10.0.18.28", "10.0.18.131",
			"10.0.22.31", "10.0.22.30", "10.0.22.33", "10.0.18.91", "10.0.22.60"
		]
	}
  }
}
Servers Apps4 (defence, safe, DC, WSUS, fs, exch)(10)
{
  "query": {
	"terms": {
		"dst_ip.keyword": [
			"10.0.18.12", "10.0.18.34", "10.0.18.29", "10.0.22.22", "10.0.18.30",
			"10.0.0.6", "10.0.22.23", "10.0.18.8", "10.0.18.20", "10.0.18.18"
		]
	}
  }
}

DMZ
{
  "query": {
	"terms": {
		"dst_ip.keyword": [
			"192.168.32.10", "192.168.32.2"
		]
	}
  }
}



remove DMZ traffic
{
  "query": {
	"bool": {
		"must_not": {
			"bool": {
				"should": [
					{ "match": { "src_mapped_ip.keyword": "192.168.32.2" } },
					{ "match": { "src_mapped_ip.keyword": "192.168.32.10" } }
				]
			}
		  }
		}
	}
}

significant terms
curl -XGET "http://localhost:9200/_search" -d'
{
  "query": {
    "range": {
      "@timestamp": {
        "gt": "now-1d"
      }
    }
  },
  "aggregations": {
    "keyword": {
      "significant_terms": {
        "field": "src_ip.keyword"
      }
    }
  }
}'


all SAN
{
  "query": {
    "bool": {
      "should": [
        { "query": { "wildcard": { "src_ip": { "value": "172.0.25.*" } } } },
        { "query": { "wildcard": { "src_ip": { "value": "172.25.0.*" } } } }
      ]
    }
  }
}
vpn users
{
  "query": {
    "bool": {
      "should": [
        {
          "prefix": {
            "src_ip": "192.168.33."
          }
        }
      ]
    }
  }
}

firewall users
{
  "query": {
    "bool": {
      "should": [
        {
          "prefix": {
            "src_fwuser": "local"
          }
        }
      ]
    }
  }
}

Remove all DNS query to 8.8.8.8
```
```
{
	"query": 
	{
		"bool": 
		{
			"must_not":
			{
				"bool":
				{
					"should": 
					[
					{
						"bool":
						{
							"must": 
							[
								{
								  "match": {
									"src_mapped_port": "53"
								  }
								},
								{
								  "match": {
									"src_mapped_ip": "8.8.8.8"
								  }
								}
							]
						}
					},
					{
						"bool":
						{
							"must": 
							[
								{
								  "match": {
									"dst_mapped_port": "53"
								  }
								},
								{
								  "match": {
									"dst_mapped_ip": "10.0.18.29"
								  }
								}
							]
						}
					}
					]
				}
			}
		}
	}
}

```




{"query":{"bool":{"should":[{"must":[{"match":{"src_mapped_port.keyword":"53"}},{"match":{"src_mapped_ip.keyword":"8.8.8.8"}}]},{"must":[{"match":{"dst_mapped_port.keyword":"53"}},{"match":{"dst_mapped_ip.keyword":"10.0.18.29"}}]}]}}}


{
  "query": {
    "bool": {
      "must_not": 
	  [
        {
          "match": {
            "dst_mapped_port.keyword": "53"
          }
        },
        {
          "match": {
            "dst_mapped_ip.keyword": "8.8.8.8"
          }
        }
      ]
    }
  }
}