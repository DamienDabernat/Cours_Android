# Android - Layouts et Animations


### Préparation du projet

Assurer-vous d'avoir un projet qui compile, si ce n'est pas le cas partez d'un nouveau projet.

Tout au long de ce projet nous allons utilisé des éléments de design qui ne sont pas inclus par défaut dans le sdk d'Android pour cela vous devais ajouter la bibliothèque de support design de Google.

Dans le build.gradle (Module : app) :
```
// Support lib for material design
compile 'com.android.support:design:25.1.0'
```

Profitez-en pour changer la version minimum du sdk à 21 (Android Lollipop) si ce n'est déja pas le cas.

Synchroniser le gradle.

### Construction du 1er layout

Modifier le layout de login en faisant en sorte que le layout racine soit un `linear layout` ayant pour id `llBackground` comme ci dessous :

```
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:orientation="vertical"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context=".activity.LoginActivity"
    android:id="@+id/llBackground">
```

Faites en sorte d'obtenir le résultat suivant :

![N|Solid](http://damien.dabernat.fr/android/loginActivity.jpg)

[Lien vers le logo](http://damien.dabernat.fr/android/channel_messaging_logo.png), où faites le votre rapidement à condition qu'il soit blanc avec une résolution similaire ;)

Attention cependant les champs identifiant et mot de passe ne sont pas de simple champs `TextView` et `EditText` mais une des nouvelles façon d'animer simplement les champs de type input d'après les guidelines material design. Voici un exemple d'intégration de ses nouveaux éléments :

```
    <android.support.design.widget.TextInputLayout
        android:id="@+id/input_layout_email"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_margin="16dp">

        <EditText
            android:id="@+id/etIdentifiant"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:textColor="@color/white"
            android:inputType="textEmailAddress"
            android:hint="@string/login" />

    </android.support.design.widget.TextInputLayout>
```

Faites de même pour le champs mot de passe. Pensez bien toutefois à renseigner le champs `inputType` de l'`editText` avec la valeur `textPassword`

### Construction du 2nd layout

Construiser un 2nd layout (normalement celui qui liste les salons de disscution) en rajoutant la même `ImageView` représentant le même logo de l'application mais d'une couleur différente.

Indice : Pour lui appliquer une coloration différente, jetez un oeil du côté de l'attribut xml `tint`

![N|Solid](http://damien.dabernat.fr/android/channelListActivity.jpg)

### Les transitions

Les transitions sont le moyen le plus simple d'obtenir de joli effet d'ouverture et de fermeture entre plusieurs activitées. 

Dans l'exemple qui suit nous allons essayé d'obtnir une transition entre les deux logo présents dans les layout créer dans la première partie.

Creer un dossier de ressource nommé `transition`
Créer le fichier : `change_image_transform.xml`

Mettre le code suivant dans le fichier précédement créé :
```
<transitionSet xmlns:android="http://schemas.android.com/apk/res/android">
    <recolor/>
    <autoTransition/>
</transitionSet>
```

[Voir la liste des transitions disponible ici](
https://developer.android.com/reference/android/transition/Transition.html)

Nous avons donc un fichier de définition de transition qui décrit comment une transition doit s'oppérer : d'abord par une coloration de l'ancien logo par le nouveau puis par une translation vers le nouveau logo.

Par la suite nous devons déclarer dans le fichier de style que nous allons utilisé des transition. Puis définir les transition d'entrée et de sortie par défaut.

Procédez comme suit :

Mettre dans style.xml :
```
<!-- enable window content transitions -->
<item name="android:windowActivityTransitions">true</item>
  
<!-- specify shared element transitions -->
<item name="android:windowSharedElementEnterTransition">@transition/change_image_transform</item>
<item name="android:windowSharedElementExitTransition">@transition/change_image_transform</item>
```

Il ne reste plus que deux étapes avant d'en terminer avec cette transision :

Donnons un nom de transition au **second** logo (celui dans la liste des salons) : Ajoutez l'attribut `transitionName` à l'`ImageView ` donnez lui pour nom `logo`

La 'final touch' : Dans votre première activité (celle de login) lors de votre intent vers le 2nd écra.n 

Remplacer votre intent par celle-ci :

```
Intent loginIntent = new Intent(LoginActivity.this, ChannelListActivity.class);
startActivity(loginIntent, ActivityOptions.makeSceneTransitionAnimation(LoginActivity.this, mIvLogo, "logo").toBundle());
```

L'astuce réside ici dans `ActivityOptions.makeSceneTransitionAnimation` qui prends en 1er paramètre l'activité, en second la vue ImageView du logo et enfin le nom que nous avons précédement donner au 2nd logo (ici Android connait donc par quelle vue commencer et par quelle vue finir !)

Testez ! Essayer plusieur type de transition et incorporez un second élément de transition (comme un `TextView` par exemple).

Astuce pour incorporer plusieurs élément de transition :
```
ActivityOptions options = ActivityOptions.makeSceneTransitionAnimation(this,
        Pair.create(view1, "agreedName1"),
        Pair.create(view2, "agreedName2"));
```

Pour finir nous allons préciser la façon dont la fênetre de l'activité elle-même doit s'animer en entrée ou en sortie pour cela mettre dans style.xml :

```
  <!-- specify enter and exit transitions -->
  <item name="android:windowEnterTransition">@android:transition/slide_top</item>
  <item name="android:windowExitTransition">@android:transition/explode</item>


```

Tester une nouvelle fois.

### Les animations

Dans ce chapitre nous allons voir deux façon d'obtenir de belles animations.

Le but est de pouvoir reproduire ce layout :

![N|Solid](http://damien.dabernat.fr/android/animation.gif)

La plus simple est d'importer des bibliothèques réputé et soutenu par la communauté. Il y en a pléthore mais aujourd'hui nous allons utiliser AndroidViewAnimations qui a l'avantage d'être très simple d'utilisation :

[Lien du git ici](https://github.com/daimajia/AndroidViewAnimations)

Dans le build.gradle (Module : app) :
```
compile 'com.android.support:support-compat:25.1.1'
compile 'com.daimajia.easing:library:2.0@aar'
compile 'com.daimajia.androidanimations:library:2.2@aar'
```

Synchroniser.

Prennez connaissance de la bibliothèque.

On souhaite ajouter maintenant ajouter l'effet 'tada' au logo toutes les 4 secondes.

Pour pouvoir exécuter une tache toute les 'x' secondes une des méthodes possible est la suivante :

```
mHandlerTada = new Handler();
mShortDelay = 4000; //milliseconds

mHandlerTada.postDelayed(new Runnable(){
    public void run(){
        // Your code here
        mHandlerTada.postDelayed(this, mShortDelay);
    }
}, mShortDelay);
```

Compléter ce code en y ajoutant l'animation 'Tada' sur le logo du layout.

Une seconde façon de faire est de définir une animation a la main en `xml`

Creer un dossier de ressource nommé `anim`

Créer le fichier `slide_left.xml` dans ce dossier et y insérer :

```
<set xmlns:android="http://schemas.android.com/apk/res/android"
    android:fillAfter="true" >

    <scale
        android:duration="500"
        android:fromXScale="1.0"
        android:fromYScale="1.0"
        android:interpolator="@android:anim/accelerate_decelerate_interpolator"
        android:toXScale="0.0"
        android:toYScale="1.0" />

</set>
```

C'est dans ce dossier qu'on insère toutes les animations du projet.

Nous allons à l'appuis du bouton connexion faire disparaitre le `TextView` du dessous via une animation de glissement par la gauche pour cela il suffit de déclarer et d'instancier l'animation au moment voulu dans la lancer via la methode `startAnimation()` de la vue. 

```
            Animation animSlideLeft = AnimationUtils.loadAnimation(this, R.anim.slide_left);
            view.startAnimation(animFade);
            
            [...]
            
            // To reset 
            view.clearAnimation();
```

**Astuce :** Vous pouvez retarder la connexion à l'api via un handler()

A vous de joué en créant plusieurs animations sur différente vue à l'aide [de ce site](http://www.journaldev.com/9481/android-animation-example).

### Les RelativeLayouts

Insérez cette bibliothèque : [AVLoadingIndicatorView](https://github.com/81813780/AVLoadingIndicatorView)

Votre objectif ici est qu'a l'appuis sur le bouton connexion le bouton disparasse via un fondu sortant et laisse place à un loader.
Pour cela vous allez devoir entourer les composant `Button` et `AVLoadingIndicatorView` d'un `RelativeLayout`.

### Snackbar

Insérer une snackBar en cas d'erreur de connexion. (Aidez-vous de la [documentation](https://developer.android.com/training/snackbar/action.html))
Ajoutez-y une action de re-connexion.

### Défilement

Faites défillé plusieurs messages en dessous du bouton de connexion

***Aide :***

```
private static final String[] explainStringArray = {
        "Connecte toi pour chatter avec tes amis",
        [...]
};
[...]
explainStringArray[new Random().nextInt(explainStringArray.length)]
```
***Aide (bis):***

Yoyo possède un listener qui permet de lancer du code lors de différents évènement.
```
YoYo.with(Techniques.SlideOutRight).duration(750).withListener(new Animator.AnimatorListener() {...}).playOn(mTvExplain);
```

### Dégradé animé

Une dernière touche d'animation pour finir ce layout : [La réalisation d'un dégradé animé.](https://github.com/dynamitechetan/Flowing-Gradient)

### Pour les plus rapides

Réaliser une activité "A propos" en utilisant les coordinators layout


