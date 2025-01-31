# projet-esme

# Projet Real Time Data Streaming 

## 📌 Contexte
Notre entreprise a récemment lancé une **application de monitoring météo en temps réel** permettant aux utilisateurs de suivre l’évolution de la météo dans différentes régions et villes. 

Ce projet met en place un **pipeline de collecte et traitement des données en temps réel**, en utilisant des outils Big Data.

## 🎯 Objectifs
1. **Collecter des données météorologiques** depuis l’API **OpenWeatherMap** et les envoyer vers un **topic Kafka** (`topic-weather`).
2. **Traiter les données en temps réel** via **Spark Streaming**, générer de nouvelles variables et publier les résultats dans un **nouveau topic Kafka** (`topic-weather-final`).
3. **Développer un pipeline opérationnel**, automatisé et optimisé pour l’analyse des données météo en temps réel.

---

## 🛠️ Outils et Technologies Utilisés
-  **Kafka** – Message broker utilisé pour la collecte et la transmission des données.  
-  **Spark Streaming** – Traitement des flux de données en temps réel.  
-  **API OpenWeatherMap** – Source des données météorologiques.  
-  **GitHub Codespaces** – Environnement de développement distant.  
-  **Java JDK 11** – Nécessaire pour exécuter Kafka et Spark.  
-  **Python 3.10** – Langage utilisé pour le développement des scripts (notamment `kafka-python` pour l’intégration avec Kafka).  

---

## 🚀 Installation et Configuration

### 1️⃣ Configuration de l’Environnement

#### 📌 Installation de Java
```bash
sudo apt-get update
sudo apt-get install openjdk-11-jdk-headless
java --version
```

#### 📌 Configuration de Java
```bash
echo 'export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64' >> ~/.bashrc
echo 'export PATH=$JAVA_HOME/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

### 2️⃣ Installation de Kafka
```bash
wget https://archive.apache.org/dist/kafka/2.6.0/kafka_2.12-2.6.0.tgz
tar -xzf kafka_2.12-2.6.0.tgz
```

#### 📌 Lancer Zookeeper et Kafka
```bash
./kafka_2.12-2.6.0/bin/zookeeper-server-start.sh ./kafka_2.12-2.6.0/config/zookeeper.properties
./kafka_2.12-2.6.0/bin/kafka-server-start.sh ./kafka_2.12-2.6.0/config/server.properties
```

#### 📌 Création des Topics Kafka
```bash
./kafka_2.12-2.6.0/bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic topic-weather
./kafka_2.12-2.6.0/bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic topic-weather-final
```

### 3️⃣ Installation de Spark
```bash
wget https://archive.apache.org/dist/spark/spark-3.2.3/spark-3.2.3-bin-hadoop2.7.tgz
tar -xvf spark-3.2.3-bin-hadoop2.7.tgz
export SPARK_HOME=/workspaces/<votre-repertoire>/spark-3.2.3-bin-hadoop2.7
export PATH=$SPARK_HOME/bin:$PATH
```

### 4️⃣ Installation de Python et des Bibliothèques
```bash
sudo apt update
sudo apt install -y python3.10 python3.10-venv python3.10-distutils
python3.10 -m pip install kafka-python
```

---

## 🏗️ Exécution des Scripts

### ✅ Démarrer le producteur Kafka
```bash
python3.10 producer.py
```

### ✅ Lancer le traitement Spark Streaming
```bash
$SPARK_HOME/bin/spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.2.3 spark.py
```
