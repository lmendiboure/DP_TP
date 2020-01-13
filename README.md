# Découverte du traitement de données avec PySpark et Jupyter Notebook

Aujourd'hui, que l'on parle d'objets connectés, de santé, de finance ou encore de e-commerce, les volumes de données générés sont très importants. Afin de maximiser les performances (et par conséquent la rentabilité), une analyse de ces données est primordiale.

De nombreux outils (Pandas, Hadoop, Spark, etc.), des moteurs de traitement de données rapide principalement destinés au Big Data ont ainsi été développés. Chacun de ces outils possède des caractéristiques particulières et actuellement Spark est très certainement le moteur de traitement de données Open Source le plus utilisé. C'est pourquoi nous allons essayer de découvrir quelques unes des fonctionnalités de cet outil dans le cadre de ce TP.

**Note : A la fin de la scéance, pensez à m'envoyer un compte-rendu répondant aux différentes questions présentes dans ce TP (leo.mendiboure@labri.fr)**

## Partie 1: Questions préliminaires

**Note : Les liens proposés pour chacune des questions dirigent vers des pages contenant une réponse partielle ou entière à la question située juste au dessus** 

**Q.1** Spark est actuellement un des moteurs de traitement de données les plus utilisés. Pourquoi ? Quel semble être le gros avantage du traitement en mémoire ?

Liens: 
  - https://fr.blog.businessdecision.com/spark-traitements-big-data/
  - https://databricks.com/blog/2014/11/05/spark-officially-sets-a-new-record-in-large-scale-sorting.html
  
**Q.2** Les outils de traitement de données d'appuient sur des techniques de partitionnement des données. Quel est l'intérêt de telles techniques ? Qu'est ce que le HDFS ? Quels sont les avantages de cette technologie ? Si un dossier contient un historique de fichiers de logs des 4 derniers années, quelle métrique pourra être utilisée pour le diviser en sous dossiers ? 

Liens :
  - https://www.datio.com/iaas/understanding-the-data-partitioning-technique/
  - https://www.hdfstutorial.com/why-hdfs-needed/
  
**Q.3** Lorsque l'on utilise un environnement HDFS, on le combine généralement avec une technologie nommée MapReduce ? Que permet de faire cette technologie ? Qu'est ce qu'un Mapper (et donc la fonction Map) ? Un Reducer (et donc la fonction Reduce) ? Illustrez le fonctionnement de ces deux fonctions au travers d'un exemple.

Liens :
  - https://fr.talend.com/resources/what-is-mapreduce/
  - https://blog.xebia.fr/2014/07/22/article-programmez-developper-un-job-mapreduce-pour-hadoop/
  - https://blog.soat.fr/2015/05/comprendre-mapreduce/
  
**Q.3** La principale différence entre Spark et la technologie de MapReduce est que le traitement des données est réalisé en mémoire avec Spark (améliorant fortement les performances !). On parle de RDD. Qu'est ce qu'une RDD ? On parle également de DataFrame et Dataset ? Quelles différences avec une RDD ? 

Liens : 
  - http://b3d.bdpedia.fr/files/slspark.pdf
  - https://www.slideshare.net/LiliaSfaxi/bigdatatp3-nosql-avec-cassandra
  - http://b3d.bdpedia.fr/spark-batch.html

**Q.4** Ces différents types d'abstrations de données (notamment les RDD) peuvent supporter deux types d'opérations. Quel est leur nom ? A quoi correspondent elles ?

Liens:
  - https://www.toptal.com/spark/introduction-to-apache-spark

**Q.5** MapReduce

Qu'est ce que MapReduce ? Qu'est sont les étapes du traitement de données ? Pourquoi ça marche mieux avec spark ? https://i.pinimg.com/originals/15/2b/79/152b7931555b284af0dbd3446636b059.png

**Q.6** Un avantage important de PySpark est de pouvoir s'intégrer avec de nombreux outils destinés aux personnes travaillant dans le domaine du traitement de données. On parle notamment de Streaming, SQL, Machine Learning et Graphes. A quoi correspondent ces différents outils ? Que permettent ils ? Donnez un exemple d'utilisation contenant l'ensemble de ces étapes.

Liens :
  - https://fr.blog.businessdecision.com/spark-traitements-big-data/
  - https://data-flair.training/blogs/apache-spark-ecosystem-components/
  - https://www.toptal.com/spark/introduction-to-apache-spark

**Q.7** Dans le cadre de ce TP on va se servir non seulement de PySpark mais également de Jupyter Notebook. Qu'est ce que Jupyter Notebook ? Quels sont les avantages de cet outil ? Pourquoi l'utiliser ici ?

Liens :
  - https://www.sicara.ai/blog/2017-05-02-get-started-pyspark-jupyter-notebook-3-minutes
  - https://www.nature.com/articles/d41586-018-07196-1

## Partie 2: Installation et prise en main

### 2.1 Installation

Pour réaliser l'installation de l'ensemble des composants nécessaires, ouvrez le fichier d'installation (https://github.com/lmendiboure/DP_TP/blob/master/InstallationGuide.md) et suivez l'ensemble des étapes décrites.

### 2.2 Prise en main

L'exemple basique d'utilisation de PySpark (et de nombreux autres moteurs de traitement de données) consiste à réaliser des opérations dans un fichier texte. Il s'agit notamment d'extraction et de comptage de mots.

http://b3d.bdpedia.fr/spark-batch.html#reprise-sur-panne

https://realpython.com/pyspark-intro/#big-data-concepts-in-python

http://cedric.cnam.fr/vertigo/Cours/RCP216/tpDonneesNumeriques.html


## Partie 3: Machine learning et PySpark

## Partie 4: A vous de jouer

