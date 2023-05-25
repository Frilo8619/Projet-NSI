# Jeu pierre, papier, ciseaux contre l'ordinateur

# Présentation

Pierre-papier-ciseaux est un jeu effectué avec les mains et opposant deux joueurs. Il possède de nombreux noms alternatifs, notamment en variant l'ordre des termes ou en remplaçant certains mots comme « papier » par « feuille » ou « pierre » par « caillou » ou « roche ». Le terme chifoumi est également une appellation courante. 

## Déroulement du jeu

De façon générale, la pierre bat les ciseaux (en les émoussant), les ciseaux battent la feuille (en la coupant), la feuille bat la pierre (en l'enveloppant). Ainsi chaque coup bat un autre coup, fait match nul contre le deuxième (son homologue) et est battu par le troisième.

## Import randint et tkinter 
```python
from random import randint
from tkinter import *
```
`from random import randint` : Cette ligne importe la fonction randint du module random. La fonction randint est utilisée pour générer un nombre aléatoire dans un intervalle donné. L'importation de cette fonction spécifique permet d'utiliser directement randint dans le code sans avoir à préciser le nom complet du module.

`from tkinter import * `: Cette ligne importe tous les objets et les fonctions du module tkinter, qui est une bibliothèque graphique standard de Python. Tkinter est utilisé pour créer des interfaces graphiques (GUI) avec des fenêtres, des boutons, des champs de texte, etc. L'importation de tous les objets avec * permet d'accéder directement à ces objets sans avoir à préciser le nom complet du module.
## Code
```python
def augmenter_scores(mon_coup,ton_coup):
    global mon_score, ton_score
    if mon_coup == 1 and ton_coup == 2:
        ton_score += 1
    elif mon_coup == 2 and ton_coup == 1:
        mon_score += 1
    elif mon_coup == 1 and ton_coup == 3:
        mon_score += 1
    elif mon_coup == 3 and ton_coup == 1:
        ton_score += 1
    elif mon_coup == 3 and ton_coup == 2:
        mon_score += 1
    elif mon_coup == 2 and ton_coup == 3:
        ton_score += 1        
```

> augmenter_scores(mon_coup, ton_coup): Cette fonction est responsable de mettre à jour les scores (mon_score et ton_score) en fonction des coups joués. Les scores sont déclarés comme des variables globales au début du code. La fonction compare les valeurs de mon_coup et ton_coup pour déterminer qui gagne et incrémente le score approprié en conséquence.

```python  
def jouer(ton_coup):
    global mon_score, ton_score, score1, score2
    mon_coup = randint(1,3)
    if mon_coup==1:
        lab3.configure(image=pierre)
    elif mon_coup==2:
        lab3.configure(image=papier)
    else:
        lab3.configure(image=ciseaux)
    augmenter_scores(mon_coup,ton_coup)
    score1.configure(text=str(ton_score))
    score2.configure(text=str(mon_score))
```
> jouer(ton_coup): Cette fonction est appelée lorsque vous jouez un coup (pierre, papier ou ciseaux). Elle prend en argument ton_coup, le coup joué par le joueur. La fonction génère également un coup aléatoire pour l'ordinateur en utilisant randint(1,3). Ensuite, en fonction des coups choisis, les images correspondantes (pierre, papier ou ciseaux) sont configurées pour être affichées dans lab1 et lab3, qui semblent être des éléments d'interface graphique. Ensuite, la fonction augmenter_scores est appelée pour mettre à jour les scores, et enfin, les valeurs des scores sont affichées à l'aide des objets score1 et score2.

```python 
def jouer_pierre():
    jouer(1)
    lab1.configure(image=pierre)

def jouer_papier():
    jouer(2)
    lab1.configure(image=papier)

def jouer_ciseaux():
    jouer(3)
    lab1.configure(image=ciseaux)

def reinit():
    global mon_score,ton_score,score1,score2,lab1,lab3
    ton_score = 0
    mon_score = 0
    score1.configure(text=str(ton_score))
    score2.configure(text=str(mon_score))
    lab1.configure(image=rien)
    lab3.configure(image=rien)
```
> jouer_pierre(), jouer_papier(), jouer_ciseaux(): Ces fonctions sont liées à des événements (par exemple, des clics de bouton) et sont appelées lorsque vous jouez respectivement avec la pierre, le papier ou les ciseaux. Chaque fonction appelle la fonction jouer avec un argument correspondant au coup joué (1 pour pierre, 2 pour papier, 3 pour ciseaux) et configure l'image affichée dans lab1 en conséquence.

> reinit(): Cette fonction est appelée lorsque vous souhaitez réinitialiser le jeu. Elle réinitialise les scores (mon_score et ton_score) à zéro, configure les images dans lab1 et lab3 pour afficher une image vide (rien), et met à jour les valeurs des scores affichées à l'aide des objets score1 et score2.

# Variables globales
```python
ton_score = 0
mon_score = 0
```

# Fenêtre graphique
```python
fenetre = Tk()
fenetre.title("Pierre, papier, ciseaux")
```
# Images
```python
rien = PhotoImage(file ='rien.gif')
versus = PhotoImage(file ='versus.gif')
pierre = PhotoImage(file ='pierre.gif')
papier = PhotoImage(file ='papier.gif')
ciseaux = PhotoImage(file ='ciseaux.gif')
```
# Label
```python
texte1 = Label(fenetre, text="Humain :", font=("Helvetica", 16))
texte1.grid(row=0,column=0)

texte2 = Label(fenetre, text="Machine :", font=("Helvetica", 16))
texte2.grid(row=0,column=2)

texte3 = Label(fenetre, text="Pour jouer, cliquez sur une des icones ci-dessous.")
texte3.grid(row=3, columnspan =3, pady =5)

score1 = Label(fenetre, text="0", font=("Helvetica", 16))
score1.grid(row=1, column=0)    

score2 = Label(fenetre, text="0", font=("Helvetica", 16))        
score2.grid(row=1, column=2)      

lab1 = Label(fenetre, image=rien)
lab1.grid(row =2, column =0)

lab2 = Label(fenetre, image=versus)
lab2.grid(row =2, column =1)

lab3 = Label(fenetre, image=rien)
lab3.grid(row =2, column =2)
```

# Boutons
```python
bouton1 = Button(fenetre,command=jouer_pierre)
bouton1.configure(image=pierre)
bouton1.grid(row =4, column =0)

bouton2 = Button(fenetre,command=jouer_papier)
bouton2.configure(image=papier)
bouton2.grid(row =4, column =1,)

bouton3 = Button(fenetre,command=jouer_ciseaux)
bouton3.configure(image=ciseaux)
bouton3.grid(row =4, column =2)

bouton4 = Button(fenetre,text='Recommencer',command=reinit)
bouton4.grid(row =5, column =0, pady =10, sticky=E)

bouton5 = Button(fenetre,text='Quitter',command=fenetre.destroy)
bouton5.grid(row =5, column =2, pady =10, sticky=W)
```
# Démarrage du jeu:
```python
fenetre.mainloop()               
```
## Lancement du jeu 

![image](https://zupimages.net/up/23/21/sdx4.png)
 
## Lien des images

https://www.apprendre-en-ligne.net/pj/ppcg/pierre.gif

https://www.apprendre-en-ligne.net/pj/ppcg/papier.gif

https://www.apprendre-en-ligne.net/pj/ppcg/ciseaux.gif

https://www.apprendre-en-ligne.net/pj/ppcg/rien.gif

https://www.apprendre-en-ligne.net/pj/ppcg/versus.gif
