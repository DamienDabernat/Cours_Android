

Extension en Swift :

```Java
package fr.dabernat.dabernify

val String.removeSpecifier: String get() = removeSpecifier()
fun removeSpecifier(): String {
    return "toto"
}

fun String.add1(): String {
    return this + "1"
}
```

Ensuite à l'appel :

```Java
Log.d("Test", string.removeSpecifier)
Log.d("Test", string.add1())
```
Faire de l'async IZI :

```Java
class doAsync(val handler: () -> Unit) : AsyncTask<Void, Void, Void>() {
    override fun doInBackground(vararg params: Void?): Void? {
        handler()
        return null
    }
}
```

Puis n'importe ou faire :

```Java
doAsync {
    //My async code
}.execute()
```
