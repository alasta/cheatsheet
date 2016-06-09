# Cacti

## Définitions :

### Source de données
  
* _COUNTER_ : stock la valeur entre le PDP actuel et le PDP précédent, le tout divisé par la période d'échantillonnage. Le PDP doit être positif.
* _DERIVE_ : identique à COUNTER, mais accepte les PDP négatifs.
* _ABSOLUTE_ : identique à COUNTER sauf que le PDP précédent est toujours de 0.
* _GAUGE_ : le PDP est stocké brute, pas de calcul avec le PDP/échnatillonnage précédent.
  
  
