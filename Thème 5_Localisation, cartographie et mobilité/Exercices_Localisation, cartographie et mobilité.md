## Exercices Thème 5 : Localisation, cartographie et mobilité

### Exercice 1

En utilisant Géoportail, trouver les coordonnées géographiques (latitude et longitude) du château de Chambord.
En utilisant openStreetMap, dire ce que l'on peut trouver aux coordonnées (latitude : 45.83267°, longitude : 6.86517°).

### Exercice 2

En Python, écrire une fonction `distance` telle que si un satellite a envoyé à l'instant t1 un signal, qui ensuite a été reçu à l'instant t2 par un récepteur, `distance(t1,t2)` renvoie la distance entre le satellite et le récepteur exprimée en km.
Les dates t1 et t2 sont données en heure UTC 
exemple : 064036.261116   : Trame envoyée à 06 h 40 min 36.261116 s
Valeur exacte de la célérité de la lumière : c=299.792,458 km/s

```Python
>>> print(distance(064036.261116,064036.328451))
20200.499999918975
```

Le GPS comprend au moins 24 satellites circulant à 20 200 km d'altitude. Ils se répartissent sur six orbites distinctes à raison de quatre satellites par orbite.

<img width="400" height="400" src="Assets/constellation.png">

Compléter la phrase au vue de l'exemple ci-dessous : une erreur d'un millionième de seconde provoque une erreur de ... mètres sur la position.

```Python
>>> print(distance(064036.261116,064036.328451))
20200.499999918975
>>> print(distance(064036.261116,064036.328452))
20200.800000020536
```

### Exercice 3

En utilisant Géoportail et l'outil "mesurer une distance", trouver la distance à vol d'oiseau de la Tour Eiffel à l'Arc de Triomphe.


### Exercice 4

En utilisant Géoportail et l'outil "calculer un itinéraire", trouver le temps de trajet en voiture pour aller de Dunkerque à Marseille.

### Exercice 5

Donner l'heure et les coordonnées d'acquisition de la trame NMEA 0183 suivante :
$GPGLL,4835.07,N,235.47,E,203712,A

### Exercice 6

Il y a plus de 2000 ans, le scientifique grec Ératosthène invente la discipline de la géographie dont le terme est encore utilisé aujourd'hui ; il a même réussi à estimer la circonférence de la Terre.

Pour cela il a constaté qu'à midi à Syène (aujourd’hui Assouan en Égypte) les rayons du Soleil sont à la verticale (un puits creusé en donne une preuve expérimentale car il est éclairé tout entier). Le même jour à la même heure, à Alexandrie, ville située quasiment sur le même méridien (à 3° de longitude près), les rayons lumineux forment un angle α de 7,2° avec un bâton planté verticalement.
De plus il sait que les caravanes de chameaux partant de Syène mettent 50 jours pour arriver à Alexandrie en parcourant 100 stades par jour (un stade équivaut à 160m).  


<img width="600" height="400" src="Assets/Erathosthene.png">

1. En utilisant l'égalité des angles alternes et internes, estimer la circonférence de la Terre en fonction de l'angle α et de la longueur de l'arc qui joint A à S. On rappelle que la longueur s d'un arc de cercle de rayon R sous-tendu par un angle α est donnée par la relation : s=R·α à condition d'exprimer α en radian. On retrouve ainsi l'expression bien connue du périmètre d'un cercle : p=2π·R avec π=180°.
2. Donner la valeur de la circonférence de la Terre calculée par Ératosthène. 
3. Estimer l'erreur relative commise en utilisant la valeur connue du rayon moyen de la Terre : 6 371 km.


### Exercice 7

1) Trouver "à la main" le plus court chemin de A à B dans le graphe suivant et donner sa longueur (chaque arête possède une longueur exprimée en km).

<img width="600" height="300" src="Assets/chemin_plus_court.png">

2) En utilisant l'algorithme de Dijkstra explicité dans ce [document](http://vfsilesieux.free.fr/Dijkstra.pdf) dont l'implémentation en Python est donnée ci-dessous, retrouver le plus court chemin de A à B.

3) Ajouter deux fonctions au programme précédent `distance_deux_points(graphe,i,j)` et `distance_totale(graphe,liste)` pour que le programme retourne également la longueur du chemin le plus court.

```Python
#  Implémentation  de  l’algorithme  de  Dijkstra

#  Graphe 1 est le graphe correspondant à l'exemple du document pdf

Graphe1 = [
          [0,2,5,False,3,False,False],
          [2,0,2,1,False,False,8],
          [5,2,0,1,4,2,False],
          [False,1,1,0,False,False,5],
          [3,False,4,False,0,False,False],
          [False,False,2,False,False,0,1],
          [False,8,False,5,False,1,False]
          ]

def ligneInit(Graphe,depart) :
#Renvoie  la  première  ligne  du  tableau
    L = []
#  nombre  de  lignes  de  Graphe  donc  nombre  de  sommets
    n = len(Graphe)
    for j in range(n) :
        poids = Graphe[depart][j]
        if poids :
#  si  l’arête  est  présente
            L.append([ poids, depart ])
        else :
            L.append(False)
    return [L]

def SommetSuivant(T, S_marques) :
#En  considérant  un  tableau  et  un  ensemble  de  sommets  marqués, détermine  le  prochain  sommet  marqué.
    L = T[-1]
    n = len(L)
#  minimum  des  longueurs,  initialisation
    min = False
    for i in range(n) :
        if not(i in S_marques) :
#  si  le  sommet  d’indice  i  n’est  pas  marqué
            if L[i]:
                if not(min) or L[i][0] < min :
#  on  trouve  un  nouveau  minimum
#  ou  si  le  minimum  n’est  pas  défini
                    min = L[i][0]
                    marque = i
    return(marque)

def ajout_ligne(T,S_marques,Graphe) :
#Ajoute  une  ligne  supplémentaire  au  tableau  """"""
    L = T[-1]
    n = len(L)
#  La  prochaine  ligne  est  une  copie  de  la  précédente, #  dont  on  va  modifier  quelques  valeurs.
    Lnew = L.copy()
#  sommet  dont  on  va  étudier  les  voisins
    S = S_marques[-1]
#  la  longueur  du  (plus  court)  chemin  associé
    long = L[S][0]
    for j in range(n) :
        if j not in S_marques:
            poids = Graphe[S][j]
            if poids :
#  si  l’arète  (S,j)  est  présente
                if not(L[j]) :  #  L[j]  =  False
                    Lnew[j] = [ long + poids, S ]
                else :
                    if long + poids < L[j][0]:
                        Lnew[j] = [ long + poids, S ]
    T.append(Lnew)
#  Calcul  du  prochain  sommet  marqué
    S_marques.append(SommetSuivant(T, S_marques))
    return T, S_marques

def calcule_tableau(Graphe, depart) :
#Calcule  le  tableau  de  l’algorithme  de  Dijkstra  """"""
    n = len(Graphe)
#  Initialisation  de  la  première  ligne  du  tableau
#  Avec  ces  valeurs,  le  premier  appel  à  ajout_ligne
#  fera  le  vrai  travail  d’initialisation
    T=[[False] *n]
    T[0][depart] = [depart, 0]
#  liste  de  sommets  marques
    S_marques = [ depart ]
    while len(S_marques) < n :
        T, S_marques = ajout_ligne(T, S_marques, Graphe)
    return T

def plus_court_chemin(Graphe, depart, arrivee) :
#Détermine  le  plus  court  chemin  entre  depart  et  arrivee  dans le  Graphe""""""
    n = len(Graphe)
#  calcul  du  tableau  de  Dijkstra
    T = calcule_tableau (Graphe,depart)
#  liste  qui  contiendra  le  chemin  le  plus  court,  on  place  l’arrivée
    C = [ arrivee ]
    while C[-1] != depart :
        C.append( T[-1][C[-1]][1] )
#  Renverse  C,  pour  qu’elle  soit  plus  lisible
    C.reverse()
    return C
    
>>> plus_court_chemin(Graphe1,0,6)
[0, 1, 2, 5, 6]

```



