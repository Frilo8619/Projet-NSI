# Pendu

![Pendu](https://www.kastete.fr/img/partie.png)

## Présentation

- Le but du jeu est de trouver un mot choisi parmi une liste prédéfinie de mots en un maximum de 11 tentatives. A chaque tour, on propose une lettre, et si la lettre proposée n'est pas dans le mot, on perd une tentative. Au bout de 11 tentatives, la partie est perdue. La partie est terminée lorsque le mot a été trouvé.

## Code du jeu

### Initialisation de la partie

#### Explications

- Avant de commencer le code du jeu, on importe les modules `turtle` et `random` qui contiennent respectivement des fonctions permettant de créer des figures graphiques diverses et des fonctions d'aléatoire telles que `random()`, `randint()`, ou bien `choice()` qui sera par la suite utilisé.
- Une liste de chaînes de caractères `choix` est ensuite créée. Elle contient des mots présélectionnés qui pourront être utilisés dans le jeu.
- Nous choisissons maintenant le mot à trouver `solution` qui va être tiré *aléatoirement* de la liste `choix` à l'aide du module `random` importé précédemment.
- On initialise le nombre de tentatives du joueur à 11 puisque notre pendu comportera un total de 11 traits lorsqu'il sera complété (lorsque la partie jouée est perdue par le joueur).
- Ensuite, on initialise les variables `affichage` et `lettres_trouvees` avec des chaînes de caractères vides, elles correspondent respectivement à l'affichage du nombre de lettres vides dans le terminal avec un tiret bas suivi d'une espace (les lettres restantes à trouver) et l'affichage des lettres trouvées et connues.
- Enfin, on va, pour chaque caractère du mot `solution`, créer un tiret bas dans l'affichage du terminal `affichage` afin que le nombre de lettres à trouver corresponde.

#### Code

```python
from turtle import *
import random
choix = ['capital', 'orange', 'raide', 'fictif',
    'conseil', 'chirurgie', 'parachute',
    'connectivite', 'triste', 'fondre', 'lait',
    'chorale', 'cuillere a cafe', 'puissance',
    'disque', 'fichier', 'rectangle', 'liberer',
    'droite', 'ridicule']
solution = random.choice(choix)

tentatives = 11
affichage = ""
lettres_trouvees = ""

for i in solution:
  affichage = affichage + "_ "
```

### Déroulement de la partie

#### Explications

- La partie débute avec un message de bienvenue affiché dans le terminal.
- Ensuite, tant que le joueur possède encore des tentatives, on affiche dans le terminal `Mot à deviner : ` ainsi que le mot `affichage` contenant les lettres trouvées du joueur ainsi que les lettres non trouvées sous forme de tirets bas. On demande également au joueur de proposer sa prochaine lettre et on l'enregistre dans la variable `proposition`, en la transformant en minuscule si nécessaire grâce à la méthode `lower()`.
- Toujours dans la boucle `while`, on teste si la lettre donnée par le joueur `proposition` est dans le mot à trouver `solution`. Si c'est le cas, on rajoute cette lettre à la variable `lettres_trouvees` et on affiche un message de succès. Si ce n'est pas le cas, le joueur perd 1 tentative et on affiche le trait correspondant sur le pendu grâce à la fonction `affichage_erreur(tentatives)` expliquée plus tard.
- Toujours dans la boucle, on réinitialise notre `affichage` à une chaîne de caractères vide. Pour chaque `lettre` du mot `solution`, si la `lettre` fait partie des `lettres_trouvees`, on ajoute `lettre` suivie d'une espace à la variable `affichage`. Dans le cas contraire, `affichage` ne gagne qu'un tiret bas suivi d'une espace (une lettre non trouvée).

#### Code

```python
print(">> Bienvenue dans le pendu <<")

while tentatives > 0:
  print("\nMot à deviner : ", affichage)
  proposition = input("Proposez une lettre : ")[0:1].lower()

  if proposition in solution:
      lettres_trouvees += proposition
      print("-> Bien vu!")
  else:
      tentatives -= 1
      affichage_erreur(tentatives)

  affichage = ""
  for caractere in solution:
      if caractere in lettres_trouvees:
          affichage += caractere + " "
      else:
          affichage += "_ "
```

---

#### Explications fonction `affichage_erreur(tentatives)`

- Cette fonction va permettre de tracer un nouveau trait sur le pendu à chaque erreur de lettre de la part du joueur grâce au module `turtle`. Le nombre de tentatives étant initialisé à 11, jusqu'à 11 traits pourront être créés. Avant de tracer le trait correspondant, on affiche un message comme quoi le joueur a sélectionné une mauvaise lettre.

#### Code de la fonction `affichage_erreur(tentatives)`

```python
def affichage_erreur(tentatives):
    """ Affiche les parties du pendu dans le cas d'une lettre 
    n'étant pas dans la solution.
    """
    print("-> Raté\n")
    if tentatives == 0:
        backward(50)
        left(140)
        forward(50)
    if tentatives == 1:
        backward(60)
        left(135)
        forward(70)
        left(110)
        forward(50)
    if tentatives == 2:
        backward(60)
        left(90)
        forward(60)
    if tentatives == 3:
        right(45)
        forward(60)
    if tentatives == 4:
        left(90)
        penup()
        forward(60)
        pendown()
        forward(120)
    if tentatives == 5:
        right(90)
        circle(30)
    if tentatives == 6:
        backward(141)
        left(135)
        forward(100)
        right(90)
        forward(70)
    if tentatives == 7:
        backward(300)
        right(135)
        forward(141)
    if tentatives == 8:
        right(90)
        forward(400)
    if tentatives == 9:
        goto(-200, -100)
        left(90)
        forward(400)
    if tentatives == 10:
        ht()
        width(10)
        penup()
        goto(-200, -100)
        pendown()
        forward(400)
```

### Fin de la partie

#### Explications

- Durant chaque tour de la boucle `while`, on teste s'il reste des lettres non trouvées parmi l'`affichage`. Si ce dernier ne comporte aucun tiret bas, on en conclut donc que le mot `solution` est trouvé, et donc que la partie est gagnée. Un message signalant la victoire du joueur est donc envoyé.

#### Code

```python
    if "_" not in affichage:
        print(">>> Gagné! <<<")
        break

print("\n    * Fin de la partie *    ")
```

---

## Code entier

```python
from turtle import *

def affichage_erreur(tentatives):
    """ Affiche les parties du pendu dans le cas d'une lettre 
    n'étant pas dans la solution.
    """
    print("-> Raté\n")
    if tentatives == 0:
        backward(50)
        left(140)
        forward(50)
    if tentatives == 1:
        backward(60)
        left(135)
        forward(70)
        left(110)
        forward(50)
    if tentatives == 2:
        backward(60)
        left(90)
        forward(60)
    if tentatives == 3:
        right(45)
        forward(60)
    if tentatives == 4:
        left(90)
        penup()
        forward(60)
        pendown()
        forward(120)
    if tentatives == 5:
        right(90)
        circle(30)
    if tentatives == 6:
        backward(141)
        left(135)
        forward(100)
        right(90)
        forward(70)
    if tentatives == 7:
        backward(300)
        right(135)
        forward(141)
    if tentatives == 8:
        right(90)
        forward(400)
    if tentatives == 9:
        goto(-200, -100)
        left(90)
        forward(400)
    if tentatives == 10:
        ht()
        width(10)
        penup()
        goto(-200, -100)
        pendown()
        forward(400)


import random
choix = ['capital', 'orange', 'raide', 'fictif',
    'conseil', 'chirurgie', 'parachute',
    'connectivite', 'triste', 'fondre', 'lait',
    'chorale', 'cuillere a cafe', 'puissance',
    'disque', 'fichier', 'rectangle', 'liberer',
    'droite', 'ridicule']
solution = random.choice(choix)

tentatives = 11
affichage = ""
lettres_trouvees = ""

for i in solution:
  affichage = affichage + "_ "

print(">> Bienvenue dans le pendu <<")

while tentatives > 0:
  print("\nMot à deviner : ", affichage)
  proposition = input("Proposez une lettre : ")[0:1].lower()

  if proposition in solution:
      lettres_trouvees += proposition
      print("-> Bien vu!")
  else:
      tentatives -= 1
      affichage_erreur(tentatives)

  affichage = ""
  for caractere in solution:
      if caractere in lettres_trouvees:
          affichage += caractere + " "
      else:
          affichage += "_ "

  if "_" not in affichage:
      print(">>> Gagné! <<<")
      break
     
print("\n    * Fin de la partie *    ")
```
