# Juste Prix

![Vincent Lagaf](https://resize.programme-television.ladmedia.fr/r/670,670/img/var/premiere/storage/images/tele-7-jours/news-tv/le-juste-prix-tf1-vincent-lagaf-de-retour-en-janvier-2015-4068658/74747540-1-fre-FR/Le-Juste-prix-TF1-Vincent-Lagaf-de-retour-en-janvier-2015.jpg)

## Présentation

Le but du jeu est de trouver un montant choisi aléatoirement dans un intervalle allant de 1 à un nombre choisi par le joueur.  
Pour se faire, ce dernier propose un nombre dans l'intervalle, et saura si le montant à trouver est supérieur, inférieur, ou égal au nombre proposé par le joueur.  
Il pourra ainsi proposer un montant en conséquence.

## Code de l'activité

Regardons comment est codé ce jeu.

### Démarrage de la partie

#### Explication 

Tout d'abord, on importe toutes les fonctions du module random. Ainsi, on pourra par la suite générer un nombre aléatoire dans l'intervalle allant de 1 à un nombre choisi.  
On initialise une variable `arret` à 0 pour le cas où le joueur trouve le bon montant.
On commence à déterminer l'intervalle. On définit la première bordure à 1, puis l'utilisateur choisira la seconde bordure. Ce nombre sera tout d'abord une chaîne de caractères, mais est par la suite transtypé en entier.
L'intervalle maintenant défini, on utilise la fonction `randint` du module `random` pour déterminer le montant à trouver.
Enfin, l'utilisateur rentre le nombre de tentatives qu'il aura pour trouver le montant. Ce nombre sera en entrée une chaîne de caractères et sera immédiatement transtypé en entier.

#### Code

```python
import random

arret = 0

valeur_minimale = 1
valeur_max = input("Quelle sera la valeur maximale ? : ")
valeur_maximale = int(valeur_max)

solution = random.randint(valeur_minimale, valeur_maximale)
tentatives = int(input("Proposez le nombre de tentatives : "))
```

### Partie

#### Explication

On commence par afficher une phrase de bienvenue dans le jeu.
Ensuite, on démarre une boucle qui ne s'arrêtera pas tant que le nombre de tentatives est non nul et que la variable d'arrêt est toujours égale à 0.  
Le joueur devra proposer un montant, qui sera stocké dans une variable sous la forme d'une chaîne de caractères. On transtype ensuite cette chaîne en entier.  
On regarde si la proposition est différente de la solution. Si c'est le cas, on regarde si la proposition est supérieure ou inférieure à la solution, ce qui a pour effet de réduire le nombre de tentatives de 1 et affiche une indication permettant de comprendre si la solution est supérieure ou inférieure au montant proposé.  
Dans le cas où la proposition est égale à la solution, on définit la variable `arret` à 1, ce qui va permettre d'arrêter la boucle, et on affiche un message de victoire.

#### Code

```python
print(">> Bienvenue dans le juste prix <<")

while (tentatives > 0) and (arret != 1):
    proposition = input("Proposez un montant: ")
    proposition = int(proposition)
    
    if proposition != solution:
        if proposition < solution:
            tentatives = tentatives - 1
            print("-> C'est plus\n")
        else:
            tentatives = tentatives - 1
            print("-> C'est moins\n")
    else:
        arret = 1
        print(">>> Gagné! <<<")
```

### Fin de partie

#### Explication

On vérifie si la variable `arret` est à 0 afin de déterminer la raison de la fin de la boucle, donc soit le nombre de tentatives est nul ce qui signifie une défaite, soit la variable d'arrêt est égale à 1 traduisant une victoire. Ainsi si la variable d'arrêt est nulle, cela indique que le premier cas s'est produit, et on affiche par conséquent un message de défaite.
Pour finir, on affiche un message de fin de partie.

#### Code

```python
if arret == 0:
    print(">>> Perdu... <<<")
print("\n    * Fin de la partie *    ")
```

---

### Code entier

```python
import random

arret = 0

valeur_minimale = 1
valeur_max = input("Quelle sera la valeur maximale ? : ")
valeur_maximale = int(valeur_max)

solution = random.randint(valeur_minimale, valeur_maximale)
tentatives = int(input("Proposez le nombre de tentatives : "))


print(">> Bienvenue dans le juste prix <<")

while (tentatives > 0) and (arret != 1):
    proposition = input("Proposez un montant: ")
    proposition = int(proposition)
    
    if proposition != solution:
        if proposition < solution:
            tentatives = tentatives - 1
            print("-> C'est plus\n")
        else:
            tentatives = tentatives - 1
            print("-> C'est moins\n")
    else:
        arret = 1
        print(">>> Gagné! <<<")
        
if arret == 0:
    print(">>> Perdu... <<<")
print("\n    * Fin de la partie *    ")
```
