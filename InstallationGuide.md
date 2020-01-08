
# PySpark et Jupyter Notebook: Guide d'installation

### Etape 1: Téléchargement de Spark

  - Choisissez la dernière version disponible de Spark: http://spark.apache.org/downloads.html
  - Tapez ensuite les commandes suivantes
 
```console
tar xzvf spark-2.0.1-bin-hadoop2.7.tgz # Unziper le projet
mv spark-2.0.1-bin-hadoop2.7/ spark # Renommer le projet
sudo mv spark/ /usr/lib/ # Déplacer le projet
```
### Etape 2 : Installer SBT
  - Pour ce faire, entrez les commandes suivantes dans un terminal
```console
echo "deb https://dl.bintray.com/sbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list  
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823  
sudo apt-get update  
sudo apt-get install sbt
```

### Etape 3 : Installer Java

  - Si jamais Java n'est pas installé (`java -version`):

```console
sudo apt-add-repository ppa:webupd8team/java  
sudo apt-get update  
sudo apt-get install oracle-java8-installer
```

# Etape 4 : Configurer spark
  - Commencez par ouvrir le fichier de configuration
```console
cd /usr/lib/spark/conf/  
cp spark-env.sh.template spark-env.sh  # On copie le fichier de conf existant pour garder une base
nano spark-env.sh
```

  - Ajoutez les deux lignes suivantes:
```console
JAVA_HOME=/usr/lib/jvm/java-8-oracle  
SPARK_WORKER_MEMORY=4g
```

### Etape 5 : Télécharger et installer Anaconda

  - Pour télécharger Anaconda : https://www.anaconda.com/distribution/#linux
  - Une fois téléchargé, excécutez le script d'install

### Etape 6 : Configurer le fichier _bash_
  - Ouvrir le fichier bashrc: `nano ~/.bashrc`
  - Ajouter les lignes suivantes :
 
```console
export JAVA_HOME=/usr/lib/jvm/java-8-oracle  
export SBT_HOME=/usr/share/sbt-launcher-packaging/bin/sbt-launch.jar  
export SPARK_HOME=/usr/lib/spark
export PATH=$PATH:$JAVA_HOME/bin
export PATH=$PATH:$SBT_HOME/bin:$SPARK_HOME/bin:$SPARK_HOME/sbin
export PYSPARK_DRIVER_PYTHON=jupyter
export PYSPARK_DRIVER_PYTHON_OPTS='notebook'
export PYSPARK_PYTHON=python2.7
export PYTHONPATH=$SPARK_HOME/python:$PYTHONPATH
```
  - Rechargez le fichier bashrc : `source ~/.bashrc`
  
Si l'ensemble des étapes d'installation ont fonctionné, vous devriez pouvoir lancer PySpark et Jupyter Notebook a l'aide de la commande suivante: `pyspark`
 
 
_Note :_ https://medium.com/@brajendragouda/installing-apache-spark-on-ubuntu-pyspark-on-juputer-ca8e40e8e655 (source) 
