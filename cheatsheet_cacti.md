# Cacti

## Définitions :

### Général
  
* DS : Data Source  
* PDP : Primary Data Point
* RRA : Round Robin Archive
* RRD : Round Robin Database (base de données tournante en FIFO)

Un RRD peut contenir plusieurs RRA (correspondant aux différent cycle de conservation de données : jours, semaine, mois, année)
  
### Source de données
  
* _COUNTER_ : stock la valeur entre le PDP actuel et le PDP précédent, le tout divisé par la période d'échantillonnage. Le PDP doit être positif.
* _DERIVE_ : identique à COUNTER, mais accepte les PDP négatifs.
* _ABSOLUTE_ : identique à COUNTER sauf que le PDP précédent est toujours de 0.
* _GAUGE_ : le PDP est stocké brute, pas de calcul avec le PDP/échnatillonnage précédent.
   
Exemple : 
  
| ------------- |:-------------:| -----:|
| Values        | 300 | 600 | 900 | 1200 |
| Step          | 300 seconds |||           |
| COUNTER DS    |   1 |  1  |   1 |    1 |
| DERIVE DS     |   1 |  1  |   1 |   1  |
| ABSOLUTE DS   |   1 |  2  |   3 |   4  |
| GAUGE DS      | 300 | 600 | 900 | 1200 | 
  


  
## Graph avec un script maison :

### Le script  
Le script doit renvoyer key:value séparés par des espaces s'il y en a plusieurs :  
key1:value1 key2:value2 key3:value3 ...  
  
Peut importe le langage du moment que le serveur connait l'interpreteur.  
  
### intégration
  
* Déclarer le script dans Data Input Methods
* Déclarer la source de données dans Data Template
* Générer les sources à partir d'un host dans Data Sources
* Créer le Graph Template
* Associer le Graph template à un Host ou un Host template


  


  
  
