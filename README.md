# Android - Layouts et Animations

---
### Préparation du projet

Assurez-vous d'avoir un projet qui compile, si ce n'est pas le cas partez d'un nouveau projet.

Tout au long de ce projet nous allons utiliser des éléments de design qui ne sont pas inclus par défaut dans le sdk d'Android pour cela vous devez ajouter la bibliothèque de support design de Google.

- Dans le build.gradle (Module : app) :
```
// Support lib for material design
compile 'com.android.support:design:25.1.0'
```

- Profitez-en pour changer la version minimum du sdk à 21 (Android Lollipop) si ce n'est pas déja le cas.
- Synchronisez le gradle.

---

### Un petit mot sur les thèmes

Un style est un ensemble d’attributs qui définisses l’apparence et le format d’une vue.
Il se défini dans un fichier ressource XML séparé du fichier XML de votre vue.
Ce fichier se nomme en général styles.xml et se situe dans le dossier values.

Vous pouvez appliquer un style (ou thème) sur l’application entière ou sur une vue spécifique.

Pour définir un style pour l’application il faut ajouter l’attribut thème dans le manifest.xml :

```
<application
android:allowBackup="true"
android:icon="@mipmap/ic_launcher"
android:label="@string/app_name"
***android:theme="@style/AppTheme »***>
```

De la même manière on peux définir un thème spécifique a une activité :

```
<activity
    android:name=".activity.SplashActivity"
    ***android:theme="@style/SplashTheme »***>
    <intent-filter>
    <action android:name="android.intent.action.MAIN" />
    <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>
```

Colors.xml

Pour une question de simplicité les couleurs peuvent être elles aussi séparé du layout.xml d’une vue.
Dans ce cas les couleurs sont rassemblé dans le dossier res/values/colors.xml

Vous pouvez ajouter celle-ci :

```
 <color name="white">#FFFFFF</color>
 <color name="yellow">#FFFF00</color>
 <color name="fuchsia">#FF00FF</color>
 <color name="red">#FF0000</color>
 <color name="silver">#C0C0C0</color>
 <color name="gray">#808080</color>
 <color name="olive">#808000</color>
 <color name="purple">#800080</color>
 <color name="maroon">#800000</color>
 <color name="aqua">#00FFFF</color>
 <color name="lime">#00FF00</color>
 <color name="teal">#008080</color>
 <color name="green">#008000</color>
 <color name="blue">#0000FF</color>
 <color name="navy">#000080</color>
 <color name="black">#000000</color>
```

Par défaut Android a besoin de 3 types de couleurs qu’on retrouvera partout dans les composants de base.

```
<color name="colorPrimary">#3F51B5</color>
<color name="colorPrimaryLight">#989AD7</color>
<color name="colorPrimaryDark">#37398D</color>
```

Dans le fichier style.xml :

```
<!-- Main theme colors -->
<!--   your app branding color for the app bar -->
<item name="colorPrimary">@color/colorPrimary</item>
<!--   darker variant for the status bar and contextual app bars -->
<item name="colorPrimaryDark">@color/colorPrimaryDark</item>
<item name="colorAccent">@color/colorAccent</item>
```

Ce sont ces trois couleurs qui seront utilisé par défaut pour donner une couleur aux vue tel que l’actionBar.

- A vous de jouer en modifiant les couleurs du thème par défaut par celle que vous préféré.

---

### Construction du 1er layout

- Modifiez le layout de login en faisant en sorte que le layout racine soit un `linear layout` ayant pour id `llBackground` comme ci dessous :

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

[Lien vers le logo](http://damien.dabernat.fr/android/channel_messaging_logo.png), ou faites le votre rapidement à condition qu'il soit blanc avec une résolution similaire ;)

Attention cependant les champs identifiant et mot de passe ne sont pas de simple champs `TextView` et `EditText` mais une des nouvelles façons d'animer simplement les champs de type input d'après les guidelines material design. Voici un exemple d'intégration de ces nouveaux éléments :

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

- Faites de même pour le champ mot de passe. Pensez bien toutefois à renseigner le champ `inputType` de l'`editText` avec la valeur `textPassword`

Si vous souhaitez modifier la couleur du texte d'indication voici comment faire :

Dans le fichier `style.xml` du dossier `values` ajouter ce style :


```
    <style name="TextLabel" parent="TextAppearance.AppCompat">
        <!-- Hint color et label color si pas de focus -->
        <item name="android:textColorHint">@color/red_500</item>
        <item name="android:textSize">20sp</item>
        <!-- bar color -->
        <item name="colorControlNormal">@color/pink_300</item>
         <!-- Label color si focus -->
        <item name="colorControlActivated">@color/green_400</item>
    </style>
```

Puis dans le layout de l'activité indiquer à la vue TextInputLayout quel thème utiliser en y ajoutant l'attribut : `android:theme="@style/TextLabel"`

---

### Construction du 2ème layout

- Construisez un 2ème layout (normalement celui qui liste les salons de discussion) en rajoutant la même `ImageView` représentant le même logo de l'application mais d'une couleur différente.

Indice : Pour lui appliquer une coloration différente, jetez un oeil du côté de l'attribut xml `tint`

![N|Solid](http://damien.dabernat.fr/android/channelListActivity.jpg)

---

### Les transitions

Les transitions sont le moyen le plus simple d'obtenir de jolis effets d'ouverture et de fermeture entre plusieurs activitées. 

Dans l'exemple qui suit nous allons essayer d'obtenir une transition entre les deux logos présents dans les layout créés dans la première partie.

- Créez un dossier de ressource nommé `transition`
- Créez le fichier : `change_image_transform.xml`

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


Par la suite nous devons déclarer dans le fichier de style que nous allons utiliser des transitions. Puis définir les transitions d'entrée et de sortie par défaut.

Mettre dans style.xml dans le style de votre choix (généralement `appTheme`) :
```
<!-- enable window content transitions -->
<item name="android:windowActivityTransitions">true</item>
  
<!-- specify shared element transitions -->
<item name="android:windowSharedElementEnterTransition">@transition/change_image_transform</item>
<item name="android:windowSharedElementExitTransition">@transition/change_image_transform</item>
```

Il ne reste plus que deux étapes avant d'en terminer avec cette transition :

Donnons un nom de transition au **second** logo dans le layout de votre deuxième activité (celui de la liste des salons) : Ajoutez l'attribut `transitionName` à l'`ImageView ` donnez lui pour nom `logo`

La 'final touch' : Dans votre première activité java (celle de login) lors de votre intent vers le 2ème écran 

Remplacez votre intent par celle-ci :

```
Intent loginIntent = new Intent(LoginActivity.this, ChannelListActivity.class);
startActivity(loginIntent, ActivityOptions.makeSceneTransitionAnimation(LoginActivity.this, mIvLogo, "logo").toBundle());
```

L'astuce réside ici dans `ActivityOptions.makeSceneTransitionAnimation` qui prends en 1er paramètre l'activité, en second la vue `ImageView` du 1er logo et enfin le nom que nous avons précédement donner au second logo (ici Android sait donc par quelle vue commencer et par quelle vue finir !)

- Testez ! Essayez plusieurs type de transition et incorporez un second élément de transition (comme un `TextView` par exemple).

Astuce pour incorporer plusieurs élément de transition :
```
ActivityOptions options = ActivityOptions.makeSceneTransitionAnimation(this,
        Pair.create(view1, "agreedName1"),
        Pair.create(view2, "agreedName2"));
```
---

##### Transition seconde partie :
Pour finir nous allons préciser la façon dont la fênetre de l'activité elle-même doit s'animer en entrée ou en sortie. Pour cela mettre dans style.xml :

```
  <!-- specify enter and exit transitions -->
  <item name="android:windowEnterTransition">@android:transition/slide_top</item>
  <item name="android:windowExitTransition">@android:transition/explode</item>


```

- Testez une nouvelle fois.

---

### Les animations

Dans ce chapitre nous allons voir deux façons d'obtenir de belles animations.

Le but est de pouvoir reproduire ce layout :

![N|Solid](http://damien.dabernat.fr/android/animation.gif)

La plus simple est d'importer des bibliothèques réputées et soutenues par la communauté. Il y en a beaucoup mais aujourd'hui nous allons utiliser AndroidViewAnimations qui a l'avantage d'être très simple d'utilisation :

[Lien du git ici](https://github.com/daimajia/AndroidViewAnimations)

Dans le build.gradle (Module : app) :
```
compile 'com.android.support:support-compat:25.1.1'
compile 'com.daimajia.easing:library:2.0@aar'
compile 'com.daimajia.androidanimations:library:2.2@aar'
```

- Prennez connaissance de la bibliothèque.

On souhaite maintenant ajouter l'effet 'tada' au logo toutes les 4 secondes.

Pour pouvoir exécuter une tache toute les 'x' seconde une des méthodes possible est la suivante (à mettre dans le onCreate) :

```
mHandlerTada = new Handler(); // android.os.handler
mShortDelay = 4000; //milliseconds

mHandlerTada.postDelayed(new Runnable(){
    public void run(){
        // Your code here
        mHandlerTada.postDelayed(this, mShortDelay);
    }
}, mShortDelay);
```

- Complétez ce code en y ajoutant l'animation 'Tada' sur le logo du layout.

---

##### Animation seconde partie :

Une seconde façon de faire est de définir une animation a la main en `xml` :

- Créez un dossier de ressource (package `res`) nommé `anim`
- Créez le fichier `slide_left.xml` dans ce dossier et y insérer :

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

Nous allons à l'appui du bouton connexion faire disparaitre le `TextView` du dessous via une animation de glissement par la gauche. Pour cela il suffit de déclarer et d'instancier l'animation au moment voulu. Puis de la lancer via la méthode `startAnimation()` de la vue. 

Dans l'activité java ou vous voulez que l'animation se joue :

```
            Animation animSlideLeft = AnimationUtils.loadAnimation(this, R.anim.slide_left);
            view.startAnimation(animFade);
            
            [...]
            
            // To reset 
            view.clearAnimation();
```

**Astuce :** Vous pouvez retarder la connexion à l'api via un handler()

A vous de jouer en créant plusieurs animations sur différentes vues à l'aide [de ce site](http://www.journaldev.com/9481/android-animation-example).

---

### Les RelativeLayouts

Insérez cette bibliothèque : [AVLoadingIndicatorView](https://github.com/81813780/AVLoadingIndicatorView)

Votre objectif ici est qu'à l'appui sur le bouton connexion le bouton disparaisse via un fondu sortant et laisse place à un loader.
Pour cela vous allez devoir entourer les composants `Button` et `AVLoadingIndicatorView` d'un `RelativeLayout`.

---

### Snackbar

Insérer une snackBar en cas d'erreur de connexion. (Aidez-vous de la [documentation](https://developer.android.com/training/snackbar/action.html))
Ajoutez-y une action de re-connexion.

---

### Défilement

Faites défiller plusieurs messages en dessous du bouton de connexion

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

Yoyo possède un listener qui permet de lancer du code lors de différents évènements.
```
YoYo.with(Techniques.SlideOutRight).duration(750).withListener(new Animator.AnimatorListener() {...}).playOn(mTvExplain);
```

---

### Dégradé animé

Une dernière touche d'animation pour finir ce layout : [La réalisation d'un dégradé animé.](https://github.com/dynamitechetan/Flowing-Gradient)

---

### Pour les plus rapides

Réalisez une activité "A propos" en utilisant les coordinators layout

---

### En vrac

```
<style name="TextLabel" parent="TextAppearance.AppCompat">
    <!-- Hint color and label color in FALSE state -->
    <item name="android:textColorHint">@color/red_500</item>
    <item name="android:textSize">20sp</item>
    <!-- Label color in TRUE state and bar color FALSE and TRUE State -->
    <item name="colorControlNormal">@color/pink_300</item>
    <item name="colorControlActivated">@color/green_400</item>
</style>
```

```
<android.support.design.widget.TextInputLayout
    android:id="@+id/input_layout_email"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:theme="@style/TextLabel"
    android:layout_margin="16dp">
 ```
