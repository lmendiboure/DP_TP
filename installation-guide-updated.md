### 1. Prérequis
Assurez-vous que vous avez déjà installé Java sur votre système. Vous pouvez le faire en utilisant les commandes suivantes :
```bash
sudo apt update
sudo apt install openjdk-8-jdk
```

Si Python 3 n'est pas déjà installé sur votre machine, vous pouvez l'installer en suivant ces étapes avant de procéder à l'installation d'Anaconda, PySpark et Jupyter Notebook :

### 2. Installation de Python 3

2.1. Ouvrez un terminal.

2.2. Pour vérifier si Python 3 est déjà installé, exécutez la commande suivante :
```bash
python3 --version
```

Si Python 3 est déjà installé, la version devrait s'afficher. Sinon, vous devrez l'installer.

2.3. Pour installer Python 3, utilisez la commande suivante :
```bash
sudo apt update
sudo apt install python3
```

Attendez que l'installation soit terminée. Vous pouvez à nouveau exécuter `python3 --version` pour vérifier que Python 3 est maintenant installé sur votre système.

### 3. Installation d'Anaconda

3.1. Téléchargez la dernière version d'Anaconda depuis le site officiel (https://www.anaconda.com/products/distribution#download-section) en sélectionnant la version pour Linux.

3.2. Une fois le téléchargement terminé, ouvrez un terminal et allez dans le répertoire où vous avez téléchargé le fichier Anaconda :
```bash
cd ~/Téléchargements # Remplacez par le chemin où vous avez téléchargé le fichier Anaconda
```

3.3. Installez Anaconda en exécutant le script d'installation (remplacez `Anaconda3-2021.05-Linux-x86_64.sh` par le nom du fichier que vous avez téléchargé) :
```bash
bash Anaconda3-2021.05-Linux-x86_64.sh
```

Suivez les instructions à l'écran pour terminer l'installation. Assurez-vous d'accepter l'ajout d'Anaconda à votre `PATH` lorsqu'on vous le demande.

### 4. Configuration de l'environnement

4.1. Pour que les modifications du `PATH` prennent effet, rechargez votre profil shell :
```bash
source ~/.bashrc
```

### 5. Installation de Spark 

5.1. Téléchargez Spark depuis le site officiel (https://spark.apache.org/downloads.html). Sélectionnez la dernière version précompilée pour Hadoop.

5.2. Extraites le fichier téléchargé :
```bash
tar -zxvf spark-3.1.2-bin-hadoop3.2.tgz
```
Assurez-vous de remplacer "spark-3.1.2-bin-hadoop3.2.tgz" par le nom de fichier correct que vous avez téléchargé.

5.3. Déplacez le dossier extrait dans un emplacement approprié (par exemple, `/opt` ou `/usr/local`) :
```bash
sudo mv spark-3.1.2-bin-hadoop3.2 /opt/spark
```

### 6. Configuration de l'environnement

6.1. Ajoutez Spark au PATH en éditant le fichier `.bashrc` ou `.zshrc` (selon votre shell) :
```bash
nano ~/.bashrc
```

Ajoutez les lignes suivantes à la fin du fichier (assurez-vous de mettre le bon chemin vers votre installation de Spark) :
```bash
export SPARK_HOME=/opt/spark
export PATH=$PATH:$SPARK_HOME/bin
```

Enregistrez le fichier et rechargez votre profil shell avec la commande :
```bash
source ~/.bashrc
```

### 7. Installation de PySpark

7.1. Vous pouvez installer PySpark en utilisant `pip` :
```bash
pip install pyspark
```

### 8. Installation de Jupyter Notebook

8.1. Installez Jupyter Notebook en utilisant conda (qui est inclus avec Anaconda) :
```bash
conda install jupyter
```

### 9. Vérification de l'installation

Pour vérifier que tout est correctement installé, vous pouvez lancer Jupyter Notebook en exécutant la commande suivante dans un terminal :
```bash
jupyter notebook
```

Cela devrait ouvrir une fenêtre de navigateur web avec l'interface Jupyter Notebook. Vous pouvez maintenant créer de nouveaux notebooks et utiliser PySpark et d'autres bibliothèques Python pour l'analyse de données et le calcul distribué.

Assurez-vous que Spark est toujours configuré comme décrit précédemment pour l'utiliser dans vos notebooks Jupyter.
