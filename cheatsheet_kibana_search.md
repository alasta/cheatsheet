# Kibana Search

## Boolean Operators 
  
``` 
And : AND &&  +  
Or  : OR  ||  -  
Not : NOT  !  
```
_**Note :** operator in uppercase_

## Wildcards
  
```  
Single characters    ?
Multiple characters  *
Fuzzy                ~
```

## Ranges
  
```  
1 to 10, including 1 and 10             [ 1 TO 10 ]
1 to 10, excluding 1 and 10             { 1 TO 10 }
1 to 10, including 1, excluding 10      [1 to 5}
All days in 2017                        [2017-01-01 TO 2017-12-31]
Specific timestamp*                     [2017-01-01T09:00:00 TO 2017-01-01T09:00:10]
Larger then 10                          >10
Smaller then 10                         <10
Larger or equal to 10                   >=10
Smaller or equal to 10                  <=10
```
_\*  timestamp : warning to timezone_


## Reserved characters

```
Reserved                                + - = && || > < ! ( ) { } [ ] ^ " ~ * ? : \ /
Break character                         \
```

## Search

```
Keyword                                 keyword
Pattern                                 *ywo*      ?eywor?
Match field                             field:term
Match field**                           field.raw:TeRm
Field contains term1 or term2           field:(term1 OR term2)
Field exists                            _exists_:field
Field missing (v5)                      !(_exists_:field)
Field missing (v2)                      _missing_:field
Phrase                                  "/etc/elasticsearch/"
Regular Expressions                     /h?[tx]ml?/
JSON                                    { "match": { "field": "term" } }
```
_**Note :**  
term : complete word in lowercase_  
_** : Not analyzed fields are case sensitive_  

