
# PySpark et Jupyter Notebook: Guide d'installation

### Etape 0: Vérifiez que Python 3 est bien installé

  - Pour ce faire: `python3 --version`
  
  - Si jamais Python 3 n'est pas installé: `sudo apt install python3 python-pip`

### Etape 1: Téléchargement de Spark

  - Choisissez la dernière version disponible de Spark : http://spark.apache.org/downloads.html

**Il s'agit normalement de la version 3** 

Note : l'accès au lien d'install peut prendre un certain temps (notamment sur les machines de l'école). Pour accélérer les choses, vous pouvez par exemple prendre un autre mirror que celui proposé
  
  - Tapez ensuite les commandes suivantes
 
```console
tar xzvf spark-2.4.4-bin-hadoop2.7.tgz # Unziper le projet
mv spark-2.4.4-bin-hadoop2.7/ spark # Renommer le projet
sudo mv spark/ /usr/lib/ # Déplacer le projet
```
### Etape 2 : Installer SBT (= maven for Java and Scala projects)
  - Pour ce faire, entrez les commandes suivantes dans un terminal
```console
echo "deb https://dl.bintray.com/sbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list  
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823  
sudo apt-get update  
sudo apt-get install sbt
```

### Etape 3 : Installer Java

  - Si jamais Java 8 n'est pas installé (`java -version`) :

**Il est essentiel que ce soit la V 8, si c'est la V7, rien ne fonctionnera par la suite !** 

  - Tapez dans un terminal de commande les lignes suivantes :
```console
echo "deb http://debian.opennms.org/ stable main" >> /etc/apt/sources.list
wget -O - http://debian.opennms.org/OPENNMS-GPG-KEY | sudo apt-key add -
sudo apt-get update
sudo apt-get install oracle-java8-installer
```
  - Suivre les instructions de l'installer (peut prendre quelques minutes)
  
  - Vérifiez que l'installation a bien fonctionné (`java -version`)

### Etape 4 : Configurer spark
  - Commencez par ouvrir le fichier de configuration adapté : 
  
```console
cd /usr/lib/spark/conf/  
cp spark-env.sh.template spark-env.sh  # On copie le fichier de conf existant pour garder une base
nano spark-env.sh
```

  - Ajoutez les deux lignes suivantes :
```console
JAVA_HOME=/usr/lib/jvm/java-8-oracle  
SPARK_WORKER_MEMORY=4g
```

### Etape 5 : Télécharger et installer Anaconda 

  - Pour télécharger Anaconda : https://www.anaconda.com/distribution/#linux
  - Une fois téléchargé, excécutez le script d'install et validez toutes les questions

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
export PYSPARK_DRIVER_PYTHON_OPTS='notebook --allow-root'
export PYSPARK_PYTHON=python3
export PYTHONPATH=$SPARK_HOME/python:$PYTHONPATH
```
  - Rechargez le fichier bashrc : `source ~/.bashrc`
  
### Etape 8 : Téléchargement du sujet de TP et du fichier de test

  - Clonez (ou téléchargez) le dossier du TP : `git clone https://github.com/lmendiboure/DP_TP.git`
  
Note: Pour installer git: `sudo apt-get install git`
  
  - Placez vous dans le dossier du TP `DP_TP`
  
**Note: Pour toute la suite du TP, on considérera que l'on travaille depuis ce dossier**
  
Si l'ensemble des étapes d'installation ont fonctionné, vous devriez pouvoir lancer PySpark et Jupyter Notebook a l'aide de la commande suivante: `pyspark` 
