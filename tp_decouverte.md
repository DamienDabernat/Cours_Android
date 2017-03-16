# Découverte d’Android:    
  
>Java est un langage de programmation utilisé aussi bien dans vos smartphones android que dans de nombreux automates, dans des applications bancaires, etc… 
>Java est reconnu pour sa robustesse et perdure depuis 1995.  
 
Nous vous proposons de découvrir le langage JAVA avec Android et une de ses plateformes de développement dans un petit exercice.  
 
**Objectifs:**

1.	Découvrir Android Studio  
2.	Importer un projet et l’exécuter 
3.	Comprendre le code et le manipuler 
 
---

## Lancez l'outil de développement :  
 
Comme vous pouvez le faire chez vous, nous utiliserons un outil de développement spécifique préconfiguré pour programmer sur Android : [`Android Studio`](http://developer.android.com/sdk/index.html). A partir du menu `Démarrer`, puis cherchez le programme `Android studio`.  Vous devez obtenir la fenêtre suivante si c’est votre première utilisation du logiciel :  
 
 ![N|Solid](http://damien.dabernat.fr/android/android1.jpg)

---

## Importer le projet : 
 
Importez le projet dans Android Studio : 

1.	[Téléchargez le projet ici](http://damien.dabernat.fr/android/CookieClicker.zip)  

2.	Recopiez le projet compressé (CookieClicker.zip) se trouvant sur dans votre lecteur P : et décompressez le sur le lecteur D :. 
Pour décompresser l'archive : clic-droit dessus puis ` Extraire tout... `
 
3.	Revenez à la fenêtre de démarrage d’Android Studio et sélectionnez `Open an existing Android Studio Project` . Si par contre, vous êtes arrivé sur l’interface classique d’Android Studio, allez dans l’onglet `File->Open`. Dans tous les cas, vous devriez voir apparaître la fenêtre suivante : 
 
   ![N|Solid](http://damien.dabernat.fr/android/android2.jpg)

A l’aide de cet explorateur de fichier, comme montré ci-dessous, ciblez le dossier que vous venez de décompresser, il doit avoir une apparence différente des dossiers classiques (logo vert d’Android Studio). Validez avec le bouton `OK`. Votre projet prêt à l'emploi devrait déjà fonctionner ! 
 
Une fois le projet ouvert, l'apparence d'Android Studio devrait ressembler à ceci : 
 
  ![N|Solid](http://damien.dabernat.fr/android/android3.jpg)
  
Si ce n'est déja pas le cas mettez la vue en mode `Android` en ouvrant la rubrique `Projet` puis en selectionnant le projet `Android` :

 ![N|Solid](http://damien.dabernat.fr/android/android5.jpg)
 
--- 
 
## Du code ! 
  
#### Exercice 1)
  
> Vous pouvez à tout moment démarrer votre application grâce au bouton `Run` : ![N|Solid](http://damien.dabernat.fr/android/android4.jpg)

1. Lancer l'application, et jouez un peu avec pour prendre un main le projet.
2. Exploration du code : 
A l'aide de l'explorateur de projet, à gauche de l'interface, naviguez dans la structure du programme.  
Trouvez où se cache le code permettant de : 
    * Définir le nombre de cookie au départ 
    * Définir le nombre de cookie gagné par seconde
3. Modifiez le code pour changer le nombre de cookie au départ (10 semble être une bonne valeur).
4. Modifier le nombre de cookie gagné par seconde (2 semble être une bonne valeur)

#### Exercice 2)

1. [Rendez à cette adresse et trouvez une nouvelle image de cookie qui vous plaise.](https://www.google.fr/search?q=cookie&tbm=isch&tbs=isz:m&*#tbs=isz:m&tbm=isch&q=cookie+png&*)
2. Renommez-la cookie.png
3. Trouvez le dossier `res->Drawable` dans le projet

 ![N|Solid](http://damien.dabernat.fr/android/android6.jpg)
4. Faire un clique droit sur ce dossier puis `show in explorer`
5. Dans le dossier `Drawable` copier et remplacer le fichier cookie.png par le nouveau que vous avez choisi en prenant le temps de le renommer également `cookie.png`

#### Exercice 3) 

1. Faites en sorte que le nombre de cookie gagné (au total / par clique / par seconde) soit sauvegardé d'un lancement à un autre

> Indice : Pour arrêter l'application vous pouvez cliquer sur le carré rouge puis relancer le jeu avec la flêche verte. Si le nombre de cookie est le même alors vous avez réussi !

#### Exercice 4) 
1. A partir de la liste d'effet ci-dessous faites-en sorte de modifier l'animation du 'gros' cookie
##### Effets :
  
Attention :
* `Flash`, `Pulse`, `RubberBand`, `Shake`, `Swing`, `Wobble`, `Bounce`, `Tada`, `StandUp`, `Wave`

Special  :
* `Hinge`, `RollIn`, `RollOut`,`Landing`,`TakingOff`,`DropOut`
  
> Indice : Cherchez la ligne : `YoYo.with(Techniques.Pulse)` du 'gros cookie' où `Techniques.Pulse` correspond à l'effet `Pulse`

#### Exercice 5) 

1. Trouvez le code qui permet d'ajouter des `magasins` (les menus qui ajoutes des bonus)
2. [Rendez à cette adresse et trouvez une nouvelle image d'usine qui vous plaise.](https://www.google.fr/search?q=cookie&tbm=isch&tbs=isz:m&*#q=factory+png&tbs=isz:i&tbm=isch&*)
3. Renommez-la usine.png
4. Ajoutez cette image dans le dossier `res->Drawable` dans le projet
3. Créez votre propre menu qui ajoute un bonus de +5 cookie par clique

>Indice : Un coût de `(2000 * numberOfCookiesGainedByClick)` parait raisonable

>Indice² : Le type de bonus est `Menu.BonusType.CLICK`

---

## Voici vos premiers pas en programmation Android, de nombreuses autres notions intéressantes sont à voir !





