# Morpion

![Morpion](https://th.bing.com/th/id/OIP.KBkXeSm43Lk9cNHlxEcA6QAAAA?w=161&h=169&c=7&r=0&o=5&dpr=1.3&pid=1.7)

## Présentation

- Le but du jeu est que l'un des deux joueurs aligne trois de ces pions sur le plateau.

## Code du jeu

### Initialisation de la partie

#### Explications

- Tout d'abord on crée le `tableau` qui est une `liste` composée de 9 éléments, allant de l'indice 0 à 8.
- Puis on créé la fonction `affiche_tableau` dans la quelle on va afficher dans le terminale chaque élément du `tableau` concatener avec `|`.
- On initialise la valeur de la variable `Partie_en_cours` à `True` car la partie vient de commencer étant donné que le tableau est construit.
- La partie vient de commencer donc la variable `Gagnant` est à `None`.
- Enfin c'est le joueur `X` qui commence étant donné qu'on lui attribue la variable.

#### Code

```python
tableau = ["-","-","-","-","-","-","-","-","-"]

def afficher_tableau():
    print(tableau[0] + " | " + tableau[1] + " | " + tableau[2])
    print(tableau[3] + " | " + tableau[4] + " | " + tableau[5])
    print(tableau[6] + " | " + tableau[7] + " | " + tableau[8])
    
Partie_en_cours = True

Gagnant = None

tour_de_joueur = "X"

```

### Déroulement de la partie

#### Explications

Le déroulement de la partie se résume grâce à la fonction `morpion`:

- La partie débute avec un message affiché dans le terminal.
- Par la suite viens la fonction qui va `afficher_tableau()`.
- Puis, dans une boucle `while` trois autres fonctions s'active tant que la `Partie_en_cours`, l'un des joueurs doit placer un pion grâce à la fonction `choix`, puis on vérifie qu'il n'y a pas de gagnant avec la fonction `Veri_si_partie_fini()` et cela est bien le cas on change de joueur grâce à la fonction `change_de_joueur`.
- Enfin si `Gagnant` est `X` ou `O`, on affiche le nom du gagnant sinon on affiche 2galité. 

#### Code

```python
def morpion():
    
    afficher_tableau()
    
    while Partie_en_cours:
        
        choix(tour_de_joueur)
        Verif_si_partie_fini()
        change_de_joueur()
        
    if Gagnant == "X" or Gagnant == "O":
        print(Gagnant + " à gagner.")
    elif Gagnant == None:
        print("égalité")

```
---

#### Explications `change_de_joueur()`

- Au lieu de crée deux joueurs distincts, il est plus facile de créer un seul joueur dont on change la valeur. C'est ce que fait cette fonction. Sachant qu'au départ du jeu, `tour_de_joueur` est initialisée avec `X`, cette fonction va donc changer la valeur à chaque tour de boucle, passant de `X` à `O` et inversement.

## Code de la fonction `change_de_joueur()` 

```python

def change_de_joueur():
    
    if tour_de_joueur == "X":
        tour_de_joueur = "O"
    elif tour_de_joueur == "O":
        tour_de_joueur = "X"

```

### Fin de la partie

#### Explications

- Durant chaque tour de la boucle, on teste deux choses. On teste s'il reste un espace de libre et si ce n'est pas cas, on déclare égalité grâce à la fonction `Veri_si_egalite` ou bien on examine chaques lignes, colonnes, diagonales ainsi que les éléments qui les composent, et si trois éléments sont égaux entre eux et ne sont pas des espaces libre `-` on renvoie le premier élément de l'alignement et cela représentera le gagnant donc soit `X` soit `O`.

#### Code

```python

def Verif_si_partie_fini():
    
    Verif_si_gagnant()
    Verif_si_egalite()
    
def Verif_si_gagnant():
    
    ligne_gagnant = verif_ligne()
    colone_gagnant = verif_colone()
    diagonal_gagnant = verif_diagonal()
    
    if ligne_gagnant:
        Gagnant = ligne_gagnant
    elif colone_gagnant:
        Gagnant = colone_gagnant
    elif diagonal_gagnant:
        Gagnant = diagonal_gagnant
    else:
        Gagnant = None

def verif_ligne():
    
    ligne1 = tableau[0] == tableau[1] == tableau[2] != "-"
    ligne2 = tableau[3] == tableau[4] == tableau[5] != "-"
    ligne3 = tableau[6] == tableau[7] == tableau[8] != "-"
    if ligne1 or ligne2 or ligne3:
        Partie_en_cours = False
    if ligne1:
        return tableau[0]
    elif ligne2:
        return tableau[3]
    elif ligne3:
        return tableau[6]

def verif_colone():
    
    colone1 = tableau[0] == tableau[3] == tableau[6] != "-"
    colone2 = tableau[1] == tableau[4] == tableau[7] != "-"
    colone3 = tableau[2] == tableau[5] == tableau[8] != "-"
    if colone1 or colone2 or colone3:
        Partie_en_cours = False
    if colone1:
        return tableau[0]
    if colone2:
        return tableau[1]
    if colone3:
        return tableau[2]
        
def verif_diagonal():
    
    diagonal1 = tableau[0] == tableau[4] == tableau[8] != "-"
    diagonal2 = tableau[2] == tableau[4] == tableau[6] != "-"
    if diagonal1 or diagonal2 :
        Partie_en_cours = False
    if diagonal1:
        return tableau[0]
    if diagonal2:
        return tableau[2]

def Verif_si_egalite():

    if "-" not in tableau:
        Partie_en_cours = False
```
---

## Code en entier

```python

tableau = ["-","-","-","-","-","-","-","-","-"]

def afficher_tableau():
    print(tableau[0] + " | " + tableau[1] + " | " + tableau[2])
    print(tableau[3] + " | " + tableau[4] + " | " + tableau[5])
    print(tableau[6] + " | " + tableau[7] + " | " + tableau[8])
    
Partie_en_cours = True

Gagnant = None

tour_de_joueur = "X"

def morpion():
    
    afficher_tableau()
    
    while Partie_en_cours:
        
        choix(tour_de_joueur)
        Verif_si_partie_fini()
        change_de_joueur()
        
    if Gagnant == "X" or Gagnant == "O":
        print(Gagnant + " à gagner.")
    elif Gagnant == None:
        print("égalité")
    
def change_de_joueur():
    
    global tour_de_joueur
    if tour_de_joueur == "X":
        tour_de_joueur = "O"
    elif tour_de_joueur == "O":
        tour_de_joueur = "X"
    return    
    
def choix(joueurs):
    
    print("C'est le tour de " + joueurs)
    position = input("Choisie une position de 1 à 9: ")
    valable = False
    while not valable:
        while position not in ["1","2","3","4","5","6","7","8","9"]:
                position = input("Choisez une position de 1 à 9: ")
        
        position = int(position) - 1
        if tableau[position] == "-":
            valable = True
        else:
            print("Emplacement déjà pris. Réessayez")
    tableau[position] = joueurs
    afficher_tableau()
    
def Verif_si_partie_fini():
    
    Verif_si_gagnant()
    Verif_si_egalite()
    
def Verif_si_gagnant():
    
    global Gagnant
    ligne_gagnant = verif_ligne()
    colone_gagnant = verif_colone()
    diagonal_gagnant = verif_diagonal()
    
    if ligne_gagnant:
        Gagnant = ligne_gagnant
    elif colone_gagnant:
        Gagnant = colone_gagnant
    elif diagonal_gagnant:
        Gagnant = diagonal_gagnant
    else:
        Gagnant = None
    return

def verif_ligne():
    
    global Partie_en_cours
    ligne1 = tableau[0] == tableau[1] == tableau[2] != "-"
    ligne2 = tableau[3] == tableau[4] == tableau[5] != "-"
    ligne3 = tableau[6] == tableau[7] == tableau[8] != "-"
    if ligne1 or ligne2 or ligne3:
        Partie_en_cours = False
    if ligne1:
        return tableau[0]
    elif ligne2:
        return tableau[3]
    elif ligne3:
        return tableau[6]
    return

def verif_colone():
    
    colone1 = tableau[0] == tableau[3] == tableau[6] != "-"
    colone2 = tableau[1] == tableau[4] == tableau[7] != "-"
    colone3 = tableau[2] == tableau[5] == tableau[8] != "-"
    if colone1 or colone2 or colone3:
        Partie_en_cours = False
    if colone1:
        return tableau[0]
    if colone2:
        return tableau[1]
    if colone3:
        return tableau[2]
    return

def verif_diagonal():
    
    diagonal1 = tableau[0] == tableau[4] == tableau[8] != "-"
    diagonal2 = tableau[2] == tableau[4] == tableau[6] != "-"
    if diagonal1 or diagonal2 :
        Partie_en_cours = False
    if diagonal1:
        return tableau[0]
    if diagonal2:
        return tableau[2]
    return

def Verif_si_egalite():

    global Partie_en_cours
    if "-" not in tableau:
        Partie_en_cours = False
    return

morpion()
```
