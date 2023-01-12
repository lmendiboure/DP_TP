# Découverte du traitement de données avec PySpark et Jupyter Notebook

Aujourd'hui, que l'on parle d'objets connectés, de santé, de finance ou encore de e-commerce, les volumes de données générés sont très importants. Afin de maximiser les performances (et par conséquent la rentabilité), une analyse de ces données est primordiale.

De nombreux outils (Pandas, Hadoop, Spark, etc.), des moteurs de traitement de données rapide principalement destinés au Big Data ont ainsi été développés. Chacun de ces outils possède des caractéristiques particulières et actuellement Spark est très certainement le moteur de traitement de données Open Source le plus utilisé. C'est pourquoi nous allons essayer de découvrir quelques unes des fonctionnalités de cet outil dans le cadre de ce TP. 

Ainsi ce TP se focalise plus généralement sur le traitement des données (et pas uniquement sur le traitement des données ITS) et sur comment celui ci peut être réalisé de façon efficace. L'ensemble des outils/procédures que nous allons découvrir sont bien entendu applicables dans l'environnement ITS.

**Note : A la fin de la scéance, pensez à m'envoyer un compte-rendu (court) répondant aux différentes questions présentes dans ce TP (leo.mendiboure@univ-eiffel.fr)**

## Partie 1: Questions préliminaires

**Note : Les liens proposés pour chacune des questions dirigent vers des pages contenant une réponse partielle ou entière à la question située juste au dessus** 

Afin de pouvoir avancer correctement sur la partie pratique de ce TP, il vous est conseillé de ne pas passer plus d'une quarantaine de minutes sur cette première partie théorique (des réponses courtes sont attendues).

**Q.1** Spark est actuellement un des moteurs de traitement de données les plus utilisés. Pourquoi (donnez différentes raisons) ? Quel semble être le gros avantage du traitement en mémoire ?

Liens: 
  - https://fr.blog.businessdecision.com/spark-traitements-big-data/
  - https://databricks.com/blog/2014/11/05/spark-officially-sets-a-new-record-in-large-scale-sorting.html
  
**Q.2** On parle de Stream Processing et Batch processing. Que signifient ces deux termes, en quoi sont ils différents ? Dans quel cas chacune de ces approches est elle pertinente ?

Lien:
  - https://medium.com/@gowthamy/big-data-battle-batch-processing-vs-stream-processing-5d94600d8103

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

Pour réaliser l'installation de l'ensemble des composants nécessaires, ouvrez le fichier d'installation (https://github.com/lmendiboure/DP_TP/blob/master/InstallationGuide.md) et suivez l'ensemble des étapes décrites (dans l'idéal avc une distro Debian !).

**Note : Alternativement, vous pouvez utiliser la VM dont le lien vous a été transmis. Dans cette VM, l'ensemble du processus d'installation a été réalisé. De plus, le dossier utilisé dans le cadre de ce projet (DP_TP) est également installé à la racine de la machine**

Rappel, lien vers la VM : https://drive.google.com/file/d/1qb597XwReUj1UuJNS2BuoZf8puDh6drj/view?usp=sharing 

Infos de connexion de la VM : user:user | root:root

### 2.2 Prise en main et premiers traitements

#### 2.2.1 Manipulations de RDDs

L'exemple basique d'utilisation de PySpark (et de nombreux autres moteurs de traitement de données) consiste à réaliser des opérations sur un fichier texte. Il s'agit notamment d'extraction/sélection/comptage de mots.

On va donc commencer avec cet exemple simple : on va télécharger un fichier en mémoire sous la forme de RDD et chercher à compter le nombre de mots dans ce fichier.

Pour ce faire, si ce n'est pas déjà fait, commencez par vous placer dans le dossier contenant le projet (DP_TP).

Lancez également Pyspark si ce n'est pas déjà fait (`pyspark`).

Dans votre navigateur internet, Jupyter Notebook devrait s'être ouvert. Si ce n'est pas le cas, accédez à l'URL http://localhost:8888/tree.

Une fois que c'est fait, cliquez sur `Nouveau` > `Python 3`.

A partir de ce moment, vous vous trouvez dans une fenêtre vous permettant d'entrer/exécuter du code en Python (il est possible que le noyeau de PySpark mette quelques secondes/minutes à se lancer).

On va maintenant rentrer les lignes de codes suivantes:

```console
# On récupère le fichier

text_file = sc.textFile("./word_count_text.txt") # Il est possible que ce chemin ne fonctionne pas : os.path peut être utilisé pour trouver le bon chemin 

# counts correspond à des données stockées dans le format de base de Spark: une RDD.

counts = text_file.flatMap(lambda line: line.split(" ")) \
             .map(lambda word: (word, 1)) \
             .reduceByKey(lambda a, b: a + b)

# On stocke le résultat

counts.saveAsTextFile("./output")
```

**Q.9** Qu'est ce qu'une fonction lambda en Python ? (https://www.guru99.com/python-lambda-function.html)

Dans le bout de code précédent (plus particulièrement dans la définition de `counts`) on fait appel à 3 fonctions. Une première qui sépare le texte de départ en mots, une seconde qui va identifier chaque mot comme une entrée (clé, valeur) et une troisième qui va associer deux entrées si elles ont une même clé (ie si c'est le même mot). 

Exécutez le bout de code précédent (à l'aide de la commande `Exécuter`).

**Q.10** Si vous accédez au contenu du répertoire `output` situé dans le répertoire courant que contient-t-il ? Pourquoi y a-t-il donc plusieurs fichiers ? Que ce passe-t-il si vous cherchez à nouveau à exécuter le bout de code précédent ? A quoi correspond cette erreur ?

On peut directement afficher le résultat du count en utilisant la fonction `counts.collect()`. Ceci peut vous permettre de visualiser les différentes étapes menant au comptage du nombre de mots.

**Q.11** On peut également utiliser les fonctions `first()` ou `count()`. Que permettent elles de faire ? 

Ajoutez les lignes 
```console
.map(lambda x: (x[1],x[0])) \
.sortByKey(False)
```
Que permettent-elles de faire ?

Dans le code précédent on peut constater que certains mots ne sont pas encore correctements traités (ie par exemple `English.`, `English`, `English;`). En effet, `split()` ne prend en compte que les espaces et non les `";.,`. Modifiez le code précédent pour que tous les mots soient traités correctements (ie par exemple `English.` devra être traité comme `English`).

*Note: Pour ce faire, il sera peut être pertinent d'utiliser une fonction comme `.replace('!','')` et `.lower()`.

**Q.12** Indiquez la ligne de commande que vous venez d'utiliser.

Une autre chose pertinente pourrait être de traiter les résultats que l'on veut afficher à l'écran. On va ici essayer de les trier en fonction de la longueur des mots. Ainsi, on ne va plus vouloir afficher que des mots avec une longueur supérieure à 3.

*Note: Pour ce faire, on pourra utiliser la fonction filter: rdd.filter(lambda x: x[1] > 0)*
*x[1] correspond ici à la value de la paire key-value. Il ne s'agit pas nécessairement de l'élément sur lequel nous devons nous agir ici.*

**Q.13**  Indiquez la ligne de commande que vous venez d'utiliser.

#### 2.2.2 Manipulations de DataFrames

Et si l'on voulait maintenant faire la même chose avec des DataFrames et non des RDDs ?

La principale différence avec des RDDs est qu'une DataFrame est une collection de données RDDs structurée. 

C'est à dire qu'au lien d'être simplement stockées dans "une grosse boite", les données vont maintenant être stockées sous forme de tableau (dans un ensemble de colonnes nommées). 

On connait maintenant le schéma des données (ie telle colonne correspond à tel type d'information) et éventuellement le type des données (int, string, etc.). 

Ceci vise à permettre avant tout un traitement bien plus rapide des données (ie on peut filtrer en fonction de la valeur d'un champ) mais également d'établir des relations entre les différentes colonnes (tables relationnelles !) ouvrant de nombreuses possibilités par rapport aux simples RDDs. 

Il est bon de préciser que les DataFrames sont une surcouche (ie une façon de visualiser les RDDs) et non un autre type de données de PySpark.

En exécutant le code ci-dessous, vous pourrez noter des différences importantes dans l'affichage par rapport à la partie précédente.

```console
textFile = sc.textFile("./word_count_text.txt")

# Comme tout à l'heure on définit une RDD

rdd = textFile.flatMap(lambda line: line.split(" ")).map(lambda word: (word, 1))

# On ajoute une sur couche: une DataFrame

df = sqlContext.createDataFrame(rdd,["word","count"])
df.show()

# Cette DataFrame peut ensuite être manipulée très simplement

countsByAppearance = df.groupBy("word").count()
countsByAppearance.orderBy("count",ascending=False).show(1000, False)
```

On peut noter notamment ici la définition de colonnes (word, count) mais surtout la facilité avec laquelle on peut agir sur ces colonnes pour: compter le nombre de mots, ordonner ces colonnes par exemple en fonction du nombre d'apparitions, etc.

C'est donc là le gros avantage des DataFrames: la possibilité de manipuler plus simplement les données.

Grâce à cela, les DataFrames permettent des manipulations de données plus rapides ainsi qu'une meilleure gestion du cache en mémoire (on peut stocker moins de données).

****


## Partie 3: Apprentissage machine et PySpark: Un exemple concret

Commencez par récupérer le fichier csv que nous allons utiliser dans toute cette partie et affichez son schéma à l'écran :

```console
df = spark.read.csv("iris.data", inferSchema=True).toDF("sep_len", "sep_wid", "pet_len", "pet_wid", "label")

df.printSchema()
```

**Q.14** Que semble contenir ce fichier ? Si vous modifiez la valeur de la variable `inferSchema` et que vous la mettez à `False`, quelle différence observez vous ? Quel semble être donc l'intérêt de cette variable ?

On peut également décider de modifier le type d'une colonne sans l'utilisation de ce paramètre. Pour ce faire, il faut utiliser la fonction `df.withColumn("name", df[name].cast(newType))`.

**Q.15** Comment faudrait il faire pour changer le type de la colonne `sep_wid` en flottant ? Donnez la ligne de code permettant d'y parvenir.

Pour pouvoir visualiser le contenu d'un ensemble de N lignes, nous pouvez utiliser la fonction show `show(N)`.

En combinant cette fonction avec la fonction `select`, on peut choisir de ne visualiser que certaines colonnes, par exemple pour les colonnes `sep_wid` et `pet_len`: `df.select('sep_wid','pet_len').show(5)`.

**Q.16** Quels type d'informations permet de récupérer la fonction `describe` (`df.describe("sep_wid").show()`) ?

On peut également réaliser bien d'autres types d'opérations comme:
  1. `df.groupBy("sep_len").count().sort("count",ascending=True).show()`	
  2. `df.drop('sep_len').columns`
  3. `df.filter(df["sep_len"] > 6).count()`
  4. `df.groupby('sep_len').agg({'sep_wid': 'mean'}).show()`
  5. `df.filter(df['label'] == 'Iris-setosa').count()`

**Q.17** Que permettent de faire chacune des lignes ci-dessus ?

La classification des espèces d'Iris (fleurs) est un problème utilisé très régulièrement pour les TPs/mises en pratiques d'algorithmes d'apprentissage. 

Ceci est dû au fait que la problématique est simple (3 espèces) et les paramètres peu nombreux (4 au total). 

Si vous souhaitez en apprendre un peu plus sur cette classification (réalisée par le botaniste Ronald Fisher) : https://makina-corpus.com/blog/metier/2017/initiation-au-machine-learning-avec-python-pratique.

Notre objectif ici va donc d'être d'appliquer des algorithmes d'apprentissage machine dans le but de déterminer de quelle espèce d'Iris il s'agit.

**Q.18** Une chaine de traitement d'apprentissage est composée de deux grands types d'éléments, lesquels ?

Vous pourrez trouver la réponse à cette question ici (https://www.slideshare.net/MichrafyMustafa/apache-spark-mlib-principes-et-concepts-pour-la-mise-en-uvre-des-mthodes-dapprentissage) notamment dans les slides 8-10.

La première opération que l'on va réaliser est une transformation. 

Ceci va nous permettre de pouvoir comparer en même temps les 4 paramètres identifiés par le botaniste (`sep_len`, `sep_wid`, `pet_len`, `pet_wid`). 

En effet, de nombreux algorithmes d'IA (notamment ceux utilisés par la suite) ne sont capables de traiter que des données de type vecteur: on va donc rassembler l'ensemble des features dans un seul vecteur.

```console
df = spark.read.csv("iris.data", inferSchema=True).toDF("sep_len", "sep_wid", "pet_len", "pet_wid", "label")

from pyspark.ml.linalg import Vectors

from pyspark.ml.feature import VectorAssembler


vector_assembler = VectorAssembler(inputCols=["sep_len", "sep_wid", "pet_len", "pet_wid"],outputCol="vector_features")
df_temp = vector_assembler.transform(df)
df_temp.show(3)
```

Vous pouvez visualiser dans la colonne `vector_features` les données vectorisées.

Une fois les données vectorisées, il va falloir les normaliser (nouvelle transformation !). Ceci va permettre de standardiser la moyenne et l'écart type des données, simplifiant leur analyse (https://dataanalyticspost.com/Lexique/normalisation/).

Pour ce faire, ajoutez les lignes ci dessous:

```console
from pyspark.ml.feature import StandardScaler

# On définit les paramètres de la normalisation: colonne sur laquelle l'appliquer, nom de la nouvelle colonne
standardscaler=StandardScaler().setInputCol("vector_features").setOutputCol("Scaled_features")

# On applique la normalisation

df_temp=standardscaler.fit(df_temp).transform(df_temp)

df_temp.select("vector_features","Scaled_features").show(5,False)
```

Dans les données actuelles, une seule colonne va nous intéresser (au delà du label évidemment): celle que l'on vient de créer contenant les données normalisées et vectorisées. En sachant que l'on peut supprimer une colonne avec la fonction `drop(nom_de_la_colonne)`. 

**Q.19** Quelle ligne de commande va nous permettre de supprimer l'ensemble des colonnes inutiles ?

Les algorithmes d'IA pour pouvoir fonctionner nécessitent de travailler sur des nombres, or, dans l'état actuel, la colonne label correspond à une chaine de caractères. On va donc ajouter les lignes de code suivantes :

```console
from pyspark.ml.feature import StringIndexer

l_indexer = StringIndexer(inputCol="label", outputCol="labelIndex")

df = l_indexer.fit(df).transform(df)

df.select("label","labelIndex").show(140)
```
**Q.20** Que permet donc de faire la fonction `StringIndexer` ?

Maintenant que nos données sont correctement labelisées, on va les séparer en deux "tas", un premier qu'on va utiliser pour l'apprentissage de nos algorithmes et un second qu'on utilisera pour vérifier que l'apprentissage à bien fonctionné.

On parle d'un côté de `training` et de l'autre de `test`.

Pour ce faire, il va suffire d'ajouter la ligne suivante: 

```console
(trainingData, testData) = df.randomSplit([0.7, 0.3])
```
On va maintenant appliquer un premier algorithme d'IA et en évaluer les performances: les arbres de décision (http://cedric.cnam.fr/vertigo/Cours/ml2/coursArbresDecision.html).

Pour ce faire, on va avoir besoin des lignes de code suivantes:

```console

# On ajoute les librairies nécessaires

from pyspark.ml.classification import DecisionTreeClassifier
from pyspark.ml.evaluation import MulticlassClassificationEvaluator

# On indique les colonnes sur lequelle on veut appliquer l'algorithme
dt = DecisionTreeClassifier(labelCol="labelIndex", featuresCol="Scaled_features")

# On applique l'algorithme d'arbre de décision sur les données d'entrainement

model = dt.fit(trainingData)

# On test le modèle sur les données prévues à cet effet

predictions = model.transform(testData)

predictions.select("prediction", "labelIndex").show(5)

# on veut maintenant évaluer les performances de l'algorithme

# On commence par indiquer quelles données on veut comparer et en fonction de quelles métriques (ie différence entre la vraie espèce d'iris et l'espèce estimée)

evaluator = MulticlassClassificationEvaluator(labelCol="labelIndex", predictionCol="prediction",metricName="accuracy")

# On applique

accuracy = evaluator.evaluate(predictions)
print("Test set accuracy = %g " % accuracy)
```
On va maintenant appliquer une seconde méthode de classification: la méthode Naive Bayésienne (https://fr.wikipedia.org/wiki/Classification_na%C3%AFve_bay%C3%A9sienne).

Ceci vise avant tout à montrer une chose : quel que soit l'algorithme sélectionné, les étapes à suivre sont les mêmes. 

```console
#On sépare à nouveau les données
train = df.randomSplit([0.7, 0.3])
train = splits[0]
test = splits[1]

# On fait l'import approprié
from pyspark.ml.classification import NaiveBayes

# On définit les paramètres de l'algorithme
nb = NaiveBayes(labelCol="labelIndex",featuresCol="Scaled_features", smoothing=1.0,modelType="multinomial")

# On l'applique
model = nb.fit(train)

# On le teste

predictions = model.transform(test)
predictions.select("label", "labelIndex","probability", "prediction").show()

# On le compare à la réalité

evaluator =MulticlassClassificationEvaluator(labelCol="labelIndex",predictionCol="prediction", metricName="accuracy")
accuracy = evaluator.evaluate(predictions)
print("Test set accuracy = " + str(accuracy))
```
**Conclusion de cette partie :** Même sans connaissance en IA, l'outil de Machine Learning de Spark permet d'appliquer des méthodes d'IA entièrement gérées par la machine (l'humain n'a qu'à paramétrer des options de très haut niveau). Grâce à cela, il est possible pour toute personne de sélectionner l'outil le plus approprié/les paramètres les plus appropriés en fonction de ses besoins et de ses contraintes (temps de traitement, données à disposition, capacité de calcul, etc.)

## Partie 5 : Un outil supplémentaire pour la visualisation de données - GraphFrames

**Q.21** Qu'est ce que GraphFrames ? Quel intérêt et quelles applications ?

(Source potentielle : https://graphframes.github.io/graphframes/docs/_site/index.html)

Afin de comprendre comment un package peut être intégré à PySpark, nous allons procéder à l'ajout du package correspondant à GraphFrames.

Pour parvenir à ceci, deux étapes principales vont être nécessaires :
  1. Télécharger le Package correspondant à GraphFrames et enregistrez le dans le dossier jar de spark : `/usr/lib/spark/jar/` (Attention il faut télécharger la version correspondant à Scala et Spark, pour ce faire, vérifiez également leur version dans ce même dossier !)
  Pour le téléchargement : https://spark-packages.org/package/graphframes/graphframes 
  2. Suivez les étapes décrites ici (https://stackoverflow.com/questions/50286139/no-module-named-graphframes-jupyter-notebook) pour ajouter le package GraphFrame et le rendre accessible dans Jupyter 

A ce moment là, vous devriez être capable dans Jupyter de lancer la commande suivante : `from graphframes import *`

Nous allons maintenant tester sur un exemple simple des fonctionnalités basiques de GraphFrames.

Pour ce faire, ajoutez le code suivant à Jupyter :

```
from graphframes import *
import networkx as nx
import matplotlib.pyplot as plt
vertices = spark.createDataFrame([
    ("Alice", 45),
    ("Jacob", 43),
    ("Roy", 21),
    ("Ryan", 49),
    ("Emily", 24),
    ("Sheldon", 52)],
    ["id", "age"]
)
edges = spark.createDataFrame([("Sheldon", "Alice", "Sister"),
                              ("Alice", "Jacob", "Husband"),
                              ("Emily", "Jacob", "Father"),
                              ("Ryan", "Alice", "Friend"),
                              ("Alice", "Emily", "Daughter"),
                              ("Alice", "Roy", "Son"),
                              ("Jacob", "Roy", "Son")],
                             ["src", "dst", "relation"])
vertices.show()
edges.show()
family_tree = GraphFrame(vertices, edges)
 ```

**Q.22** A quoi correspondent les vertices et les edges ? 

Nous allons maintenant tenter de visualiser le Graphe correspondant (orienté et non orienté).

Pour le graphe non orienté, ajoutez les lignes suivantes : 
```
def plot_undirected_graph(edge_list):
    plt.figure(figsize=(9,9))
    gplot=nx.Graph()
    for row in edge_list.select("src", "dst").take(1000):
        gplot.add_edge(row["src"], row["dst"])
    nx.draw(gplot, with_labels=True, font_weight="bold", node_size=3500)
plot_undirected_graph(family_tree.edges)
```
Pour le graphe orienté, ajoutez les lignes suivantes :

```
def plot_directed_graph(edge_list):
    plt.figure(figsize=(9,9))
    gplot=nx.DiGraph()
    edge_labels = {}
    for row in edge_list.select("src", "dst", "relation").take(1000):
        gplot.add_edge(row["src"], row["dst"])
        edge_labels[(row["src"], row["dst"])] = row["relation"]
    pos = nx.spring_layout(gplot)
    nx.draw(gplot, pos, with_labels=True, font_weight="bold", node_size=3500)
    nx.draw_networkx_edge_labels(gplot, pos, edge_labels=edge_labels, font_color="green", font_size=11, font_weight="bold")
plot_directed_graph(family_tree.edges)
```
**Q.23** Quelle est la différence entre un Graphe Orienté et un Graphe Non Orienté ?

Un autre concept important avec les graphes est la notion de Degré des noeuds. 

**Q.24** A quoi correspond cette notion ? Quelle est la différence entre Degré Entrant et Degré Sortant ?

(Source potentielle : https://fr.wikipedia.org/wiki/Degr%C3%A9_(th%C3%A9orie_des_graphes))

Dans le cas présent, nous pouvons afficher les degrés  des différents noeuds à l'aide des lignes suivantes :

```
tree_degree = family_tree.degrees
tree_degree.show()
degree_edges = edges.filter(("src = 'Alice' or dst = 'Alice'"))
degree_edges.show()
plot_directed_graph(degree_edges)

# Degré entrant
tree_inDegree = family_tree.inDegrees
tree_inDegree.show()
indegree_edges = edges.filter(("dst = 'Jacob'"))
plot_directed_graph(indegree_edges)

# Degré sortant

tree_outDegree = family_tree.outDegrees
tree_outDegree.show()
```


## Partie 6 : Un petit exemple de traitement de données en autonomie

L'idée est à présent, en vous appuyant sur les fonctions vues précédemment, que vous réalisiez en autonomie certains traitements de données sur un jeu de données que vous pourrez trouver ici (à télécharger dans la VM donc) : https://github.com/CODAIT/redrock/blob/master/twitter-decahose/src/main/resources/Location/worldcitiespop.txt.gz

*Note* : Le code de cette partie devra être joint au rapport qui sera fourni à la fin de cette séance.

Les traitement de données qui devront être réalisés par votre programme sont les suivants :
  1. Retirez les lignes pour lesquelles l'information relative au nombre d'habitants n'est pas fournie
  2. Affichez, pour les lignes restantes, differentes informations relatives au nombre d'habitant : valeur minimale, valeur maximale, valeur moyenne. (Pour ce faire, la fonction describe pourrait vous être utile)
  3. Effectuez un tri sur les données afin de pouvoir afficher les 15 villes avec le nombre d'habitants le plus faible
  4. Retirez les doublons : Certaines villes apparaissent plusieurs fois sous différents noms dans le fichier qu'il vous reste (exemple : Delhi). Si deux villes sont situées au même endroit (même coordonnées géographiques), retirez de la liste la ville avec le plus petit nombre d'habitants


## Partie 6 : Un petit exemple plus complet en autonomie

## Partie 7 : ITS et PySpark : Petit travail de réflexion

Beaucoup de villes mettent à disposition des données concernant leur infrastructures: listes de gares, aires de covoiturage, liste d'équipements sportifs, aménagements cyclables, etc.

C'est le cas de la métropole de Bordeaux par exemple (https://opendata.bordeaux-metropole.fr/explore/?disjunctive.publisher&disjunctive.frequence&disjunctive.territoire&sort=title)

**Q.21** En considérant le tableau ci dessous:

https://opendata.lillemetropole.fr/explore/dataset/comptage_siredo_historique/table/?sort=-annee&dataChart=eyJxdWVyaWVzIjpbeyJjaGFydHMiOlt7InR5cGUiOiJjb2x1bW4iLCJmdW5jIjoiU1VNIiwieUF4aXMiOiJtam8iLCJzY2llbnRpZmljRGlzcGxheSI6dHJ1ZSwiY29sb3IiOiJyYW5nZS1BY2NlbnQifV0sInhBeGlzIjoidmlsbGUiLCJtYXhwb2ludHMiOm51bGwsInNvcnQiOiIiLCJzZXJpZXNCcmVha2Rvd24iOiJhbm5lZSIsInN0YWNrZWQiOiJub3JtYWwiLCJzZXJpZXNCcmVha2Rvd25UaW1lc2NhbGUiOiJ5ZWFyIiwiY29uZmlnIjp7ImRhdGFzZXQiOiJjb21wdGFnZV9zaXJlZG9faGlzdG9yaXF1ZSIsIm9wdGlvbnMiOnsic29ydCI6Ii1hbm5lZSJ9fX1dLCJ0aW1lc2NhbGUiOiIiLCJkaXNwbGF5TGVnZW5kIjp0cnVlLCJhbGlnbk1vbnRoIjp0cnVlfQ%3D%3D

Quel type d'applications de Spark et plus particulièrement de Machine Learning peut on imaginer ? Donnez au moins 3 idées.
