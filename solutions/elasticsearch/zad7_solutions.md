7.3
GET games/_search 
{ 
  "query": { 
    "bool": { 
      "must": [ 
        { "match": { "Name": "Mario" } } 
      ], 
      "filter": [ 
        { "range": { "Year": { "gte": 2000 } } }, 
        { "terms": { "Genre.keyword": ["Platform", "Racing"] } } 
      ], 
      "must_not": [ 
        { "term": { "Publisher.keyword": "Ubisoft" } } 
      ] 
    } 
  } 
} 
7.4
GET games/_search
{
  "query": {
    "match": {
      "Name": {
        "query": "Assasin Cred",
        "fuzziness": "AUTO"
      }
    }
  }
}
7.5
GET games/_search 
{ 
  "query": { "match": { "Name": "Duty" } }, 
  "highlight": { 
    "fields": { "Name": {} } 
  } 
}
7.6
GET games/_search 
{ 
 "query": { 
   "match_all": {} 
 }, 
 "sort": [ 
   { 
     "Global_Sales": { "order": "desc" } 
   } 
 ], 
 "size": 3, 
 "from": 0 
} 
7.7
GET games/_search 
{ 
 "query": { 
   "multi_match": { 
     "query": "Nintendo", 
     "fields": ["Publisher", "Name^3"] 
   } 
 } 
} 
7.8
GET games/_search 
{ 
 "query": { 
   "match": { "Genre": "Sports" } 
 }, 
 "_source": ["Name", "Year"] 
} 
 7.9 (Terms Aggregation)
GET games/_search
{
  "size": 0,
  "aggs": {
    "top_publishers": {
      "terms": {
        "field": "Publisher.keyword",
        "size": 5
      }
    }
  }
}
7.10 (Avg Aggregation)
GET games/_search
{
  "size": 0,
  "query": {
    "match": { "Genre": "Shooter" }
  },
  "aggs": {
    "srednia_sprzedaz": {
      "avg": { "field": "Global_Sales" }
    }
  }
}
7.11 (Prefix)
GET games/_search
{
  "query": {
    "match_phrase_prefix": {
      "Name": "Super Ma"
    }
  },
  "_source": ["Name"]
}