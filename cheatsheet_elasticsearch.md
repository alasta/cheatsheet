# ElasticSearch

Affiche les infos sur le master  
```
GET /_cat/master  
```
  
Affiche les infos sur les nodes  
```
GET /_cat/nodes  
```

Affiche les stats  
```
GET _nodes/stats/
```

Affiche les stats mais seulement pour les directives transport et http  
```
GET _nodes/stats/transport,http
```
  
Création d'un Index  
```
PUT /monindex
```

Afficher les index  
```
GET _cat/indices  
```

Affiche les shards    
```
GET _cat/shards  
```
  
Affiche la santé du cluster  
```
GET _cat/health  
```


## Afficher la configuration du cluster

```
GET /_cluster/settings
```

## Allocation dynamique des shards
transient : ne survit pas au reboot du cluster.  
  
```
PUT /_cluster/settings
{
  "transient": {
    "cluster.routing.allocation.enable": "none"
  }
}
``` 
  
persistent : survit au reboot du cluster.  
```
PUT /_cluster/settings
{
  "persistent": {
    "cluster.routing.allocation.enable": "none"
  }
}
```
Valeurs :  
  
  - "all" : allocation dynamique activée
  - "none" : allocation dynamique désactivée
  - null : on supprime la directive
  
  
  
