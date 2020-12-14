#### PySpark Streaming

**A faire, si vous le souhaitez, lorsque vous aurez fini le sujet principal**

Et si on voulait faire la même chose avec PySpark Streaming ?

La grosse différence est que l'on ne va plus faire du traitement de données connues à un instant donné mais du traitement d'un flux continu de données: dès que PySpark va recevoir des données (dans un intervalle de quelques secondes), il va réaliser sur ces données les traitement pré-définies.

Commençons par définir un traitement: 

```console
# On réalise les imports qui vont nous permettre d'utiliser PySpark

from pyspark.streaming import StreamingContext

# On instancie un contexte de Streaming PySpark, avec un intervalle de temps de 1s (ie toutes les 1s on va récupérer les données dans le buffer et les traiter)

ssc = StreamingContext(sc, 1) 

# On détermine où est le serveur de streaming d'où vont provenir les données, en l'occurence ici le port 7777

lines = ssc.socketTextStream("localhost", 7777)

# On réalie les mêmes opérations que précédemment

words = lines.flatMap(lambda line: line.split(" "))
pairs = words.map(lambda word: (word, 1))
wordCounts = pairs.reduceByKey(lambda x, y: x + y)

# On affiche le résultat

wordCounts.pprint()

# Pour lancer le traitement avec Spark Streaming, il est nécessaire d'appeler la fonction start. En effet, l'exécution d'une fonction finale (map, print, etc.) ne suffit pas à lancer le traitement.

ssc.start()  

# Chaque traitement (ie du buffer d'une seconde) est lancé dans un thread. Or, il est primordial que le programme principal (ie celui qui va lancer l'ensemble des threads) continue à tourner. Pour ce faire, on utilise la fonction awaitTermination.

ssc.awaitTermination()  
```

Si maintenant on veut tester le code que l'on vient d'écrire et vérifier que toutes les secondes il récupère bien les données disponibles et es traite.

Pour ce faire, il nous faudrait tout d'abord lancer un petit serveur Web sur le port 7777.

La façon la plus simple de faire est (dans un terminal) de lancer la commande : ` nc -lk 7777`.

Lancez dans un second temps le code que l'on vient écrire.

Vous devriez déjà constater que toutes les secondes, PySpark Streaming cherche à effectuer le traitement (bien qu'il n'y ait pour l'instant pas de données sur le serveur).

Pour ajouter des données au serveur, il vous suffit simplement d'écrire dans le terminal dans lequel vous avez lancé la commande `nc`.
