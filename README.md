# Découverte du traitement de données avec PySpark et Jupyter Notebook

Aujourd'hui, que l'on parle d'objets connectés, de santé, de finance ou encore de e-commerce, les volumes de données générés sont très importants. Afin de maximiser les performances (et par conséquent la rentabilité), une analyse de ces données est primordiale.

De nombreux outils (Pandas, Hadoop, Spark, etc.), des moteurs de traitement de données rapide principalement destinés au Big Data ont ainsi été développés. Chacun de ces outils possède des caractéristiques particulières et actuellement Spark est très certainement le moteur de traitement de données Open Source le plus utilisé. C'est pourquoi nous allons essayer de découvrir quelques unes des fonctionnalités de cet outil dans le cadre de ce TP.

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


## Partie 3: Machine learning et PySpark



## Partie 4: A vous de jouer

