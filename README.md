# Anagramas puntuados del español

Este repo está inspirado en el blog post por Mark Dominus titulado [I found
the best anagram in English](https://blog.plover.com/lang/anagram-scoring.html),
en el que diseña un sistema de puntaje para anagramas para encontrar "el
mejor".

Quise probar hacer lo mismo para el español, para lo que usé el código de Mark,
levemente modificado para hacer que funcionara en mi máquina. Mi fork es
https://github.com/pilaf/anagram-scoring

Las listas de anagramas son:

* [scored.txt](scored.txt) &mdash; anagramas con puntaje, órden alfabético
* [scored-sorted.txt](scored-sorted.txt) &mdash; anagramas con puntaje,
  ordenados por puntaje
* [simple.txt](simple.txt) &mdash; anagramas sin puntaje

## Proceso

Para la lista de palabras usé el paquete
[wspanish](https://launchpad.net/ubuntu/+source/wspanish).

Como las palabras del español tienen tildes, y estas no me importan para
encontrar anagramas, tuve que quitárselas al diccionario original. Para eso usé
`iconv` para transliterar Latin1 a ASCII:

```bash
$ iconv -f latin1 -t ascii//TRANSLIT words.spanish.latin1 > words.spanish.ascii
```

El resultado es que las vocales acentuadas (áéíóú) son reemplazadas con `'`
seguido de la vocal (e.g. `'a` para á) y la ñ es reemplazada con `~n`. Como
queremos preservar la ñ reemplazamos `~n` con `ñ` otra vez y eliminamos todas
las `'`:

```bash
$ sed 's/~n/ñ/g' words.spanish.ascii > words.spanish.utf8
```

Como ASCII no contiene ñ, el resultado de correr `sed` va a ser UTF-8.

```bash
$ sed -i "s/'//g" words.spanish.utf8
```

Finalmente tenemos un archivo de palabaras que podemos usar para calcular los
anagramas.

Usando el fork de `anagram-scoring` mencionado arriba, podemos correr
`make-scoredict` con `words.spanish.utf8`. Los resultados están linkeados
arriba.
