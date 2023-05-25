```python
from turtle import *

def affichage_erreur(tentatives):
    """ Affiche les parties du pendu dans le cas d'une lettre 
    n'étant pas dans la solution.
    """
    print("-> Nope\n")
    if tentatives==0:
        backward(50)
        left(140)
        forward(50)
        ontimer(bye(), 5000)
    if tentatives==1:
        backward(60)
        left(135)
        forward(70)
        left(110)
        forward(50)
    if tentatives==2:
        backward(60)
        left(90)
        forward(60)
    if tentatives==3:
        right(45)
        forward(60)
    if tentatives==4:
        left(90)
        penup()
        forward(60)
        pendown()
        forward(120)
    if tentatives==5:
        right(90)
        circle(30)
    if tentatives==6:
        backward(141)
        left(135)
        forward(100)
        right(90)
        forward(70)
    if tentatives==7:
        backward(300)
        right(135)
        forward(141)
    if tentatives==8:
        right(90)
        forward(400)
    if tentatives==9:
        goto(-200, -100)
        left(90)
        forward(400)
    if tentatives==10:
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

for l in solution:
  affichage = affichage + "_ "

print(">> Bienvenue dans le pendu <<")

while tentatives > 0:
  print("\nMot à deviner : ", affichage)
  proposition = input("proposez une lettre : ")[0:1].lower()

  if proposition in solution:
      lettres_trouvees = lettres_trouvees + proposition
      print("-> Bien vu!")
  else:
      tentatives = tentatives - 1
      affichage_erreur(tentatives)

  affichage = ""
  for x in solution:
      if x in lettres_trouvees:
          affichage += x + " "
      else:
          affichage += "_ "

  if "_" not in affichage:
      print(">>> Gagné! <<<")
      break
     
print("\n    * Fin de la partie *    ")
```
