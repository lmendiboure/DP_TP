# Découverte du traitement de données avec PySpark et Jupyter Notebook

Aujourd'hui, que l'on parle d'objets connectés, de santé, de finance ou encore de e-commerce, les volumes de données générés sont très importants. Afin de maximiser les performances (et par conséquent la rentabilité), une analyse de ces données est primordiale.

De nombreux outils (Pandas, Hadoop, Spark, etc.), des moteurs de traitement de données rapide principalement destinés au Big Data ont ainsi été développés. Chacun de ces outils possède des caractéristiques particulières et actuellement Spark est très certainement le moteur de traitement de données Open Source le plus utilisé. C'est pourquoi nous allons essayer de découvrir quelques unes des fonctionnalités de cet outil dans le cadre de ce TP. Ainsi ce TP ce focalise sur le traitement des données (et pas sur le traitement des données ITS). Toutefois, l'ensemble des outils/procédures que nous allons décrouvrir sont applications dans l'environnement ITS.

**Note : A la fin de la scéance, pensez à m'envoyer un compte-rendu répondant aux différentes questions présentes dans ce TP (leo.mendiboure@labri.fr)**

## Partie 1: Questions préliminaires

**Note : Les liens proposés pour chacune des questions dirigent vers des pages contenant une réponse partielle ou entière à la question située juste au dessus** 

**Q.1** Spark est actuellement un des moteurs de traitement de données les plus utilisés. Pourquoi (donnez différentes raisons) ? Quel semble être le gros avantage du traitement en mémoire ?

Liens: 
  - https://fr.blog.businessdecision.com/spark-traitements-big-data/
  - https://databricks.com/blog/2014/11/05/spark-officially-sets-a-new-record-in-large-scale-sorting.html
  
**Q.2** On parle de Stream Processing et Batch processing. Que signifient ces deux termes. Dans quel cas chacune de ces approches est elle pertinente ?

Liens:
  - https://medium.com/@gowthamy/big-data-battle-batch-processing-vs-stream-processing-5d94600d8103
  - https://blog.syncsort.com/2017/07/big-data/big-data-101-batch-stream-processing/

*Note : Hadoop, le principal concurrent de Spark au départ offre des performances intéressantes en Batch Processing mais très faibles en Stream Processing (lié au non traitement en mémoire)*

  
**Q.3** Les outils de traitement de données s'appuient sur des techniques de partitionnement des données. Quel est l'intérêt de telles techniques ? Qu'est ce que le HDFS ? Quels sont les avantages de cette technologie ? Si un dossier contient un historique de fichiers de logs des 4 derniers années, quelle métrique pourra être utilisée pour le diviser en sous dossiers ? 

Liens :
  - https://www.datio.com/iaas/understanding-the-data-partitioning-technique/
  - https://www.hdfstutorial.com/why-hdfs-needed/
  
**Q.4** Lorsque l'on utilise un environnement HDFS, on le combine généralement avec une technologie nommée MapReduce ? Que permet de faire cette technologie ? Qu'est ce qu'un Mapper (et donc la fonction Map) ? Un Reducer (et donc la fonction Reduce) ? Illustrez le fonctionnement de ces deux fonctions au travers d'un exemple.

Liens :
  - https://fr.talend.com/resources/what-is-mapreduce/
  - https://blog.xebia.fr/2014/07/22/article-programmez-developper-un-job-mapreduce-pour-hadoop/
  - https://blog.soat.fr/2015/05/comprendre-mapreduce/
  
**Q.5** La principale différence entre Spark et la technologie de MapReduce est que le traitement des données est réalisé en mémoire avec Spark (améliorant fortement les performances !). On parle de RDD. Qu'est ce qu'une RDD ? On parle également de DataFrame et Dataset ? Quelles différences avec une RDD ? 

Liens : 
  - http://b3d.bdpedia.fr/files/slspark.pdf
  - https://www.slideshare.net/LiliaSfaxi/bigdatatp3-nosql-avec-cassandra
  - http://b3d.bdpedia.fr/spark-batch.html

**Q.6** Ces différents types d'abstrations de données (notamment les RDD) peuvent supporter deux types d'opérations. Quel est leur nom ? A quoi correspondent elles ? On parle souvent d'ETL, que signifie ce sigle ?

Liens:
  - https://www.toptal.com/spark/introduction-to-apache-spark
  - https://www.synaltic.fr/blog/faire-un-job-etl-avec-apache-spark-partie-1/
  - https://databricks.com/glossary/extract-transform-load


**Q.7** Un avantage important de PySpark est de pouvoir s'intégrer avec de nombreux outils destinés aux personnes travaillant dans le domaine du traitement de données. On parle notamment de Streaming, SQL, Machine Learning et Graphes. A quoi correspondent ces différents outils ? Que permettent ils ? Donnez un exemple d'utilisation contenant l'ensemble de ces étapes.

Liens :
  - https://fr.blog.businessdecision.com/spark-traitements-big-data/
  - https://data-flair.training/blogs/apache-spark-ecosystem-components/
  - https://www.toptal.com/spark/introduction-to-apache-spark

**Q.8** Dans le cadre de ce TP on va se servir non seulement de PySpark mais également de Jupyter Notebook. Qu'est ce que Jupyter Notebook ? Quels sont les avantages de cet outil ? Pourquoi l'utiliser ici ?

Liens :
  - https://www.sicara.ai/blog/2017-05-02-get-started-pyspark-jupyter-notebook-3-minutes
  - https://www.nature.com/articles/d41586-018-07196-1

## Partie 2: Installation et prise en main

### 2.1 Installation de l'environnement

Pour réaliser l'installation de l'ensemble des composants nécessaires, ouvrez le fichier d'installation (https://github.com/lmendiboure/DP_TP/blob/master/InstallationGuide.md) et suivez l'ensemble des étapes décrites.

### 2.2 Prise en main et premiers traitements

#### 2.2.1 Manipulations de RDDs

L'exemple basique d'utilisation de PySpark (et de nombreux autres moteurs de traitement de données) consiste à réaliser des opérations dans sur fichier texte. Il s'agit notamment d'extraction/sélection/comptage de mots.

On va donc commencer avec cet exemple simple.

Pour ce faire, si ce n'est pas déjà fait, commencez par vous placer dans le dossier contenant le projet (DP_TP).

Lancez également Pyspark si ce n'est pas déjà fait (`pyspark`).

Dans votre navigateur internet, Jupyter Notebook devrait s'être ouvert. Si ce n'est pas le cas, accédez à l'URL http://localhost:8888/tree.

Une fois que c'est fait, cliquez sur `Nouveau` > `Python 2`.

A partir de ce moment vous vous trouvez dans une fenêtre vous permettant d'entrer/exécuter du code avec PySpark (il est possible que le noyeau de PySpark mette quelques secondes/minutes à se lancer).

On va maintenant rentrer les lignes de codes suivantes:

```console
text_file = sc.textFile("./word_count_text.txt") # Il est possible que ce chemin ne fonctionne pas
counts = text_file.flatMap(lambda line: line.encode("ascii", "ignore").split()) \
             .map(lambda word: (word, 1)) \
             .reduceByKey(lambda a, b: a + b)
counts.saveAsTextFile("./output")
```

**Q.9** Qu'est ce qu'une fonction lambda en Python ? (https://www.guru99.com/python-lambda-function.html)

Dans le bout de code précédent on fait appel à 3 fonctions. Une première qui sépare le texte de départ en mots (et l'encode en UTF-8), une seconde qui va identifier chaque mot comme une entrée (clé, valeur) et une troisième qui va associer deux entrées si elles ont une même clé (ie si c'est le même mot). 

Exécutez le bout de code précédent (à l'aide de la commande `Exécuter`).

**Q.10** Si vous accédez au contenu du répertoire `output` situé dans le répertoire courant que contient-t-il ? Pourquoi y a-t-il donc plusieurs fichiers ? Que ce passe-t-il si vous cherchez à nouveau à exécuter le bout de code précédent ? A quoi correspond cette erreur ?

On peut directement afficher le résultat du count en utilisant la fonction `counts.collect()`. Ceci peut vous permettre de visualiser les différentes étapes menant au comptage du nombre de mots.

**Q.11** On peut également utiliser les fonctions `first()` ou `count()`. Que permettent elles de faire ? En sachant que l'on peut trier une liste à l'aide de la fonction `sortByKey()` donnez la ligne de commande permettant d'afficher une liste triée.

Dans le code précédent on peut constater que certains mots ne sont pas encore correctements traités (ie par exemple `English.`, `English`, `English;`). En effet, `split()` ne prend en compte que les espaces et non les `";.,`. Modifiez le code précédent pour que tous les mots soient traités correctements (ie par exemple `English.` devra être traité comme `English`).

*Note: Pour ce faire, il sera peut être pertinent d'utiliser une fonction comme replace.*

**Q.12** Indiquez la ligne de commande que vous venez d'utiliser.

Une autre chose pertinente pourrait être de traiter les résultats que l'on veut afficher à l'écran. On va ici essayer de les trier en fonction de la longueur des mots. Ainsi, on ne va plus vouloir afficher que des mots avec une longueur supérieure à 3.

*Note: Pour ce faire, on pourra utiliser la fonction filter: rdd.filter(lambda x: x[1] > 0)*

*Note 1: x[1] correspond ici à la value de la paire key-value, peut être pas l'élément sur lequel nous devons nous agir.*

**Q.13**  Indiquez la ligne de commande que vous venez d'utiliser.

#### 2.2.2 Manipulations de DataFrames

Et si l'on voulait maintenant faire la même chose avec des DataFrames et non des RDDs ?

La principale différence avec des RDDs est qu'une DataFrame est une collection de données RDDs structurée. C'est à dire qu'au lien d'être simplement stockées dans "une grosse boite", les données vont maintenant être stockées sous forme de tableau (dans un ensemble de colonnes nommées). On connait maintenant le schéma des données (ie telle colonne correspond à tel type d'information) et éventuellement le type des données (int, string, etc.). Ceci vise à permettre avant tout un traitement bien plus rapide des données (ie on peut filtrer en fonction de la valeur d'un champ) mais également d'établir des relations entre les différentes colonnes (tables relationnelles !) ouvrant de nombreuses possibilités par rapport aux simples RDDs. Il est bon de préciser que les DataFrames sont une surcouche (ie une façon de visualiser les RDDs) et non un autre type de données de PySpark.


#### 2.2.3 PySpark Streaming

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

****


## Partie 3: Apprentissage machine et PySpark: Un exemple concret

Commencez par récupérer le fichier csv que nous allons utiliser dans toute cette partie et affichez en son schéma à l'écran:

```console
from pyspark import SparkFiles

url = "https://raw.githubusercontent.com/guru99-edu/R-Programming/master/adult_data.csv"
sc.addFile(url)
df = sqlContext.read.csv(SparkFiles.get("adult_data.csv"), header=True, inferSchema= True)
df.printSchema()
```

**Q.14** Que semble contenir ce fichier ? Si vous modifiez la valeur de la variable `inferSchema` et que vous la mettez à `False`, quelle différence observez vous ? Quel semble être donc l'intérêt de cette variable ?

On peut également décider de modifier le type d'une colonne sans l'utilisation de ce paramètre. Pour ce faire, il faut utiliser la fonction `df[name].cast(newType)`.

**Q.15** Comment faudrait il faire pour changer le type de la colonne `age` en flottant ? donnez la ligne de code permettant d'y parvenir.

Pour pouvoir visualiser le contenu d'un ensemble de N lignes, nous pouvez utiliser la fonction show `show(N)`.

En combinant cette fonction avec la fonction `select`, on peut choisir de ne visualiser que certaines colonnes, par exemple pour les colonnes `age` et `genre`: `df.select('age','gender').show(5)`.

**Q.16** Quels type d'informations permet de récupérer la fonction `describe` (`df.describe("age").show()`) ?

On peut également réaliser bien d'autres types d'opérations comme:
  1. `df.crosstab('age', 'income').sort("age_income").show(100)`
  2. `df.groupBy("education").count().sort("count",ascending=True).show()`	
  3. `df.drop('education-num').columns`
  4. `df.filter(df.age > 40).count()`
  5. `df.groupby('marital').agg({'capital-gain': 'mean'}).show()`			
  
**Q.17** Que permettent de faire chacune des lignes ci-dessus ?

On va maintenant ajouter une nouvelle colonne à notre schéma: le carré de l'âge.

En effet, l'âge n'a pas une évolution linéaire par rapport au revenu: une personne jeune aura tendance à gagner peu, une personne en milieu/fin de carrière à avoir un salaire bien plus élevé et une personne retraitée aura tendance à voir son salaire diminuer fortement. C'est donc souvent le carré de l'âge qui est utilisé et non l'âge lui même (pour mettre plus en avant cette évolution).

**Q.18** En sachant que la fonction `withColumn(col_name, value)`, ajoutez une nouvelle colonne `age_square` dont la valeur est égale au carré de la colonne `age`. Donnez la ligne de commande permettant d'y parvenir.

Note: `**2` permet de calculer le carré.

Si vous souhaitez réorganiser l'ordre des colonnes, vous pouvez le faire à l'aide de la commande `select`.

Par exemple:

```console
COLUMNS = ['age', 'age_square', 'workclass', 'fnlwgt', 'education', 'education-num', 'marital',
           'occupation', 'relationship', 'race', 'sex', 'capital-gain', 'capital-loss',
           'hours-week', 'native-country', 'label']
df = df.select(COLUMNS)
```

**Q.19** Si l'on affiche le nombre de personnes venant de Hollande et qu'on le compare au nombre de personne provenant d'autres pays, que peut on constater ? Pensez vous qu'il est pertinent de garder cette personne venant de Hollande dans cette étude ? (cf code ci-dessous)

```console
df.filter(df['native-country'] == 'Holand-Netherlands').count()
df.groupby('native-country').agg({'native-country': 'count'}).sort("count(native-country)").show()
```

Retirez des données cette personne à l'aide de la commande:

`df_remove = df.filter(df['native-country'] !=	'Holand-Netherlands')`

SRC pour suite : https://www.slideshare.net/MichrafyMustafa/apache-spark-mlib-principes-et-concepts-pour-la-mise-en-uvre-des-mthodes-dapprentissage

## Partie 4 : ITS et PySpark : Petit travail de réflexion

Beaucoup de villes mettent à disposition des données concernant leur infrastructures: listes de gares, aires de covoiturage, liste d'équipements sportifs, aménagements cyclables, etc.

C'est le cas de la métropole de Bordeaux par exemple (https://opendata.bordeaux-metropole.fr/explore/?disjunctive.publisher&disjunctive.frequence&disjunctive.territoire&sort=title)

**Q.** En considérant le tableau ci dessous:

https://opendata.lillemetropole.fr/explore/dataset/comptage_siredo_historique/table/?sort=-annee&dataChart=eyJxdWVyaWVzIjpbeyJjaGFydHMiOlt7InR5cGUiOiJjb2x1bW4iLCJmdW5jIjoiU1VNIiwieUF4aXMiOiJtam8iLCJzY2llbnRpZmljRGlzcGxheSI6dHJ1ZSwiY29sb3IiOiJyYW5nZS1BY2NlbnQifV0sInhBeGlzIjoidmlsbGUiLCJtYXhwb2ludHMiOm51bGwsInNvcnQiOiIiLCJzZXJpZXNCcmVha2Rvd24iOiJhbm5lZSIsInN0YWNrZWQiOiJub3JtYWwiLCJzZXJpZXNCcmVha2Rvd25UaW1lc2NhbGUiOiJ5ZWFyIiwiY29uZmlnIjp7ImRhdGFzZXQiOiJjb21wdGFnZV9zaXJlZG9faGlzdG9yaXF1ZSIsIm9wdGlvbnMiOnsic29ydCI6Ii1hbm5lZSJ9fX1dLCJ0aW1lc2NhbGUiOiIiLCJkaXNwbGF5TGVnZW5kIjp0cnVlLCJhbGlnbk1vbnRoIjp0cnVlfQ%3D%3D

quel type d'applications de Spark et plus particulièrement de Machine Learning peut on imaginer ? Donnez au moins 3 exemples.
