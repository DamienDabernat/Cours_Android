

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
