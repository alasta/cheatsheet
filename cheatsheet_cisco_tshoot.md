## BGP

### Critères de sélection de la 'best'

    next-hop : doit être accessible
    weight : le plus grand
    local preference : la plus grande
    injectée localement
    as-path : le plus petit
    origin-code : préférence du i au ?
    MED : la plus petite
    eBGP préféré à IGP
    iBGP : voisin IGP le plus proche
    eBGP : chemin le plus ancien
    router-ID : le plus petit

### Configuration :

```
router bgp <AS>  

   ! si l'AS du voisin est égale à l'AS locale c'est une relation iBGP dans le cas contraire c'est de l'eBGP  
   neighbor <IP_du_voisin> remote-as <AS_du_voisin>

   ! utiliser une interface particulère pour monter la relation (par défaut c'est l'ip de l'interface du voisin).  
   neighbor <IP_du_voisin> update-source <Interface local>

   ! dans le cas ou l'IP du routeur n'est pas sur l'interface directement connecté au voisin  
   neighbor <IP_du_voisin> ebgp-multihop 

   ! injection de routes dans la table BGP  
   network <sous-réseau> [mask <masque_de_sous-réseau>]

   ! redistribution de routes dans la table BGP  
   redistribute <Type_de_routes> [metric <metric> route-map <Nom_route-map>] 


   !!Optionnelle  
   ! Modification des timers  
   timers bgp <hello> <holdtime>

   ! Modification de la fréquence des annonces  
   neighbor <IP_du_voisin> advertisement-interval <Interval_en_secondes>

   ! Modification de l'interval de scan de la table BGP pour l'insertion dans la table de routage  
   bgp scan-time <Interval_en_secondes>

   ! Autoriser/forcer le set du next-hop dans les annonces iBGP avec un voisin iBGP.  
   neighbor <IP_du_voisin_iBGP> next-hop-self

   ! Modification du weight  
   neighbor <IP_du_voisin> weight <Valeur>  
   ! ou via route-map  
   neighbor <IP_du_voisin> route-map W1

   ! Modification de la local preference (global à toutes les reception d'annonces eBGP)  
   bgp default local-preference 200  
   ! ou via route-map  
   neighbor <IP_du_voisin> route-map LC200 in

   ! Modification de l'AS-Path via route map  
   ! route-map ASPP  
   !   set as-path prepend <AS_local> <AS_local> ...  
   neighbor <IP_du_voisin> route-map ASPP out

   ! Modification de la MED via route-map  
   ! route-map M60  
   !   set metric 60  
   neighbor <IP_du_voisin> route-map M60 out  
   ! ou en global  
   default-metric 60

   ! Modification de traffic avec l'AS-PATH  
   ! ip as-path access-list 1 permit 2000$  
   ! route-map ASFilter  
   !  match as-path 1  
   neighbor <IP_du_voisin> route-map ASFilter in

   ! Filtrage des annonces :  
   ! selon l'AS  
   ! ip as-path access-list 1 permit \REGEX\  
   ! ip as-path access-list 1 deny ...
   
   ! Filtrage des annonces reçues du voisin  
   neighbor <IP_du_voisin> filter-list 1 in

   ! Filtrage des annonces envoyées au voisin  
   neighbor <IP_du_voisin> filter-list 1 out

   ! selon des réseaux  
   ! ip prefix-list \NAME\ permit ...  
   ! ip prefix-list NAME deny ...

   ! Filtre les annonces reçues du voisin  
   neighbor <IP_du_voisin> prefix-list NAME in

   ! Filtre les annonces envoyées au voisin  
   neighbor <IP_du_voisin> prefix-list NAME_ out

   ! selon divers paramètres  
   ! route-map DIVERS permit 10  
   !   match ip-adress ...

   ! route-map DIVERS deny 20  
   !   match ip address prefix-list ...

   ! route-map DIVERS permit 30  
   !   match as-path ...

   ! Filtre les annonces reçues du voisin  
   neighbor <IP_du_voisin> route-map DIVERS in

   ! Filtre les annonces envoyées au voisin  
   neighbor <IP_du_voisin> route-map DIVERS out

   ! Aggrégation de routes  
   aggregate-address 10.0.0.0 255.0.0.0 summary-only

   ! Ajout de la soft-configuration  
   neighbor <IP_du_voisin> soft-reconfiguration inbound
   ```
   
   
   ### Debug commandes
```   
show bgp summary
  router-id
  AS
```  
http://meetings.ripe.net/ripe-44/presentations/ripe44-eof-bgp.pdf  
  
  ### table BGP
```  
    * : l’étoile signifie que la route est valide
    > : le chevron signifie que c’est la meilleure route disponible pour cette destination (
    Network : le réseau de destination
    Next Hop : prochain saut pour joindre la destination
    Metric : un des attributs constituant la métrique totale
    LocPrf : un des attributs constituant la métrique totale
    Weight : un des attributs constituant la métrique totale
    Path : les AS par lesquels il faudra passer (ici il n’y en a que 1 : le 200)
```


   
   ## OSPF
   
   ### Configuration
   
```   
router ospf 100  
 ! Declaration du router-id  
 router-id 1.1.1.1  
 
 ! auth md5
 area 0 authentication message-digest
 
 ! declaration des reseaux qui participent a OSPF
 network 10.0.3.0 0.0.0.255 area 0  
 network 10.0.0.0 0.0.0.255 area 0  
   
 ! Redistribution  
 redistribute connected  
   
 ! Annonce d'une default
 default-information originate  
   
 ! Summarization  
   area 20 range 10.20.0.0 255.255.252.0
   
 ! Definition de l'auth en md5
 int fa 1/0
  ip ospf message-digest-key 1 md5 passworD
 
 ! Forcer a devenir DR (defaut : 1)
 int fa 1/0
  ip ospf priority 200
 
 ! Forcer a NE PAS devenir DR/BDR
 int fa 1/0
   ip ospf priority 0
``` 

### Debug
```
show ip ospf neighbor  
    Affiche les voisins  
   
 show ip ospf neighbor detail    
 
 show ip ospf interface
    Process ID OSPF
    Etat DR/BDR
    Timers
    
   
 clear ip ospf process  
   reinitialise le process ospf  
 ```  
### Type de routes

```
O : route OSPF standard
IA : Route venant d’une autre Area
N1 : Route de type 1 qui a été redistribuée dans une NSSA
N2 : Route de type 2 qui a été redistribuée dans une NSSA
E1 : Route externe qui a été redistribuée, de type 1
E2 : Route externe qui a été redistribuée, de type 2
```

### Etat avec le voisin
```
Down : Nous n’avons pas encore reçus de Hello du voisin, mais nous essayons de le joindre
Init : On reçoit un Hello du voisin, mais notre routeur n’est pas listé dans le champ Neighbors
2-Way : La relation est créée (notre routeur est listé dans le champ Neighbors). Election DR / BDR si nécessaire
Exchange : Echange de DBD – Data Base Description
Loading : Echange de LSU – Link State Update
Full : Bases de données synchronisées
```
