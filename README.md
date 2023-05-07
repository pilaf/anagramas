# Anagramas puntuados del español

Inspirado en el blog post de Mark Dominus titulado *[I found the best anagram in
English](https://blog.plover.com/lang/anagram-scoring.html)* en el que diseña
un sistema para medir la complejidad de anagramas, decidí buscar "el mejor
anagrama" (en realidad el más complejo) del español. Para eso hice [un fork del
código de Mark](https://github.com/pilaf/anagram-scoring) y construí una lista
simple de palabras.

Los resultados son:

* [scored.txt](scored.txt) &mdash; anagramas con puntaje de complejidad en
  órden alfabético
* [scored-sorted.txt](scored-sorted.txt) &mdash; anagramas con puntaje,
  ordenados por puntaje
* [simple.txt](simple.txt) &mdash; simple lista de anagramas sin puntajes

## Reproducción

Para la lista de palabras usé el paquete
[wspanish](https://launchpad.net/ubuntu/+source/wspanish).

Como las palabras del español tienen tildes, y estas no importan para encontrar
anagramas, tuve que quitárselas a la lista de palabras original. Para eso usé
el comando `iconv` para transliterar Latin1 a ASCII:

```bash
$ iconv -f latin1 -t ascii//TRANSLIT words.spanish.latin1 > words.spanish.ascii
```

El resultado es que las vocales acentuadas (áéíóú) son reemplazadas con `'`
seguido de la vocal (e.g. `'arbol` para *árbol*) y la ñ es reemplazada con `~n`
(e.g. `ni~no` para *niño*).  Como queremos preservar la ñ reemplazamos `~n` con
`ñ` y eliminamos todas las `'`:

```bash
$ sed 's/~n/ñ/g' words.spanish.ascii > words.spanish.utf8
```

Como ASCII no contiene ñ, el resultado de correr el comando de arriba va a ser
UTF-8.

```bash
$ sed -i "s/'//g" words.spanish.utf8
```

Finalmente tenemos un archivo de palabaras que podemos usar para calcular los
anagramas.

Usando el fork de `anagram-scoring` mencionado arriba, podemos correr
`make-scoredict` con `words.spanish.utf8`. Los resultados están linkeados
arriba.

## Anagramas favoritos/interesantes

### Países y nacionalidades

* 07 argentino / ignorante
* 11 aeronautico / ecuatoriano

### Profesiones

* 09 avicultor / lucrativo
* 03 ferretero / refertero (DRAE: adj. Dicho de una persona: Que ocasiona riñas o pendencias)
* 09 ceramista / escatimar
* 09 carnicero / correncia (coloq. diarrea. / coloq. vergüenza)
* 09 aborrencia / carabinero
* 08 cesantia / cineasta
* 08 cercamiento / comerciante

### Realeza/nobleza

* 05 emperador / empoderar
* 08 baronesa / soberana

### Religión

* 03 santa / satan
* 04 sacro / craso (indisculpable)
* 05 islamico / laicismo
* 09 calentadora / cardenalato
* 08 cortesia / sectario
* 06 satanico / tasacion

### Significados opuestos

* 04 conexion / inconexo
* 04 extension / inextenso
* 05 deshermanar / hermandarse
* 06 apolitico / capitolio
* 08 belicosa / sociable

### Asociaciones

* 08 protestar / trasporte
* 06 cochino / hocicon
* 10 pirotecnica / crepitacion (Ruido que se produce al crepitar algo, en especial, el que produce la leña al quemarse.)
* 08 defuncion / infecundo
* 09 casamentero (Que gusta de proponer o concertar casamientos) / encamotarse (Quedar enamorado de alguien)

### Nombres propios

* 04 norma / roman
* 05 norma / ramon
* 05 pedro / poder
* 06 sarmiento / mentirosa

### Varios

* 04 acuchillar / cucharilla
* 05 nutria / rutina
* 05 obviar / vibora
* 06 mediocre / merecido
* 06 mejorar / remojar
* 08 cachondeo / encochado
* 08 cartesiano / estacionar
* 08 corseteria / secretario
* 08 cortesana / ratonesca
* 08 lamentar / maternal
* 08 pandereta / pedantear
* 08 pintoresca / prestacion
* 08 revelado / valedero
* 09 acontecida / anecdotica
* 09 aglutinar / triangula
* 09 apresurosa / persuasora
* 09 aracnoides / sacadinero (actividad que induce a gastar dinero)
* 09 ardidamente / determinada
* 09 atraccion / narcotica
* 09 bulliciosamente / escabullimiento
* 09 contraposicion / pronosticacion
* 09 curvilinea / virulencia
* 09 desamoblar / embaldosar
* 09 desangramiento / grandiosamente
* 09 duomesino / seudonimo
* 09 erutacion / neurotica
* 09 escalonamiento / ocasionalmente
* 09 incorrecta / retraccion
* 09 infeccioso / oficinesco
* 09 interesado / sedentario
* 09 presuncioso / supersonico
* 10 ironicamente / renacimiento
* 11 entropezada / panderetazo
