## Exercices Thème 7 : La photographie numérique

### Exercice 1

On dispose d'une image carrée dont la définition est de 4 Mpx. Déterminer les dimensions en cm de cette image :
- si elle est affichée sur un écran de résolution 144 ppi
- si elle est imprimée par une imprimante de résolution 300 dpi

1 inch = 1 pouce = 2.54 cm

### Exercice 2

Un magasin propose deux ordinateurs à des prix intéressants. Le premier possède un écran de définition 1233 × 925 px et de dimensions 345,44 × 259,08 mm (écran 17"). Le second a un écran de définition 1219 × 914 px et de dimensions 304,80 × 228,60 mm (écran 15"). Lequel a la meilleure résolution ? On calculera la résolution de chaque écran exprimée en ppi.

### Exercice 3

Lorsque l'on dispose du code RVB d'une couleur, qu'on note (R,V,B) le calcul de la luminance se calcule à l'aide de la formule L = 0,2126 × R + 0,7152 × V + 0,0722 × B.
Écrire une fonction en Python telle que `lum(couleur)` qui renvoie la valeur de la luminance, lorsque la couleur est donnée sous forme d'un triplet (r,v,b).
La tester dans le cas du blanc (255,255,255), du rose clair (255,192,203) et du bordeaux (165,42,42).

### Exercice 4

On souhaite convertir une photographie couleur en noir et blanc. Les niveaux de gris s'obtiennent avec les codes RVB de la forme (x,x,x), c'est-à-dire avec la même composante de rouge, de vert et de bleu.
Pour convertir les couleurs en niveaux de gris, on peut utiliser la valeur de la luminance donnée dans l'exercice précédent : si le code RVB de la couleur est (R,V,B) et L la luminance, on utilise le code RVB(L',L',L') où L' est la partie entière de L.

Écrire une fonction Python telle que `niveau_gris(couleur)` qui renvoie le code RVB du niveau de gris correspondant puis la tester sur le rose clair et le bordeaux.
On utilisera la fonction floor du module `math` en saisissant la commande `from math import floor`. 
`floor(x)` renvoie la partie entière du nombre flottant x.

```Python
from math import floor
>>> floor(2.78)
2
```

### Exercice 5

Dans cet exercice nous allons utiliser le module Image de la librairie PIL de Python.

On suivra [ici](http://vfsilesieux.free.fr/traitements_d_une_me%CC%82me_image.pdf) les différentes traitements d'une même image.

### Exercice 6

Analyser le code source de la [page html](http://isnangellier.alwaysdata.net/php/melange.html) suivante et procéder à une réalisation similaire. 
