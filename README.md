 Projet IoT : ESP32 + Serveur Web Ubuntu

![ESP32 Banner](https://images.unsplash.com/photo-1518770660439-4636190af475?q=80\&w=1200\&auto=format\&fit=crop)

Description

Ce projet consiste à créer un **
objet connecté (IoT)** utilisant une **carte ESP32**, un **serveur web Ubuntu**, et un **site web dynamique**.

L’objectif principal est de permettre à l’ESP32 :

*  d’envoyer des données à un serveur web
* de contrôler une LED à distance
* d’activer un buzzer depuis une interface web
* d’afficher les données en temps réel sur un site web



#Fonctionnement du système

#Architecture globale

text
ESP32 → WiFi → Serveur Ubuntu (Apache + PHP) → Site Web


Schéma du projet

![Architecture IoT](https://upload.wikimedia.org/wikipedia/commons/3/3b/Internet_of_Things.jpg)



Technologies utilisées

| Technologie | Rôle                   |
| ----------- | ---------------------- |
| ESP32       | Microcontrôleur WiFi   |
| Ubuntu VM   | Hébergement du serveur |
| Apache2     | Serveur Web            |
| PHP         | Traitement des données |
| HTML/CSS    | Interface utilisateur  |
| WiFi        | Communication réseau   |



#Machine Virtuelle Ubuntu

Une machine virtuelle Ubuntu est utilisée comme serveur local.

#Avantages

* Aucun risque pour le PC principal
* Facile à réinstaller
* Méthode professionnelle
* Hébergement local du site web

#Logiciels recommandés

* VirtualBox
* VMware



# Installation du serveur web

# Installation Apache + PHP

```bash
sudo apt update
sudo apt install apache2 php libapache2-mod-php
```

# Répertoire du site

```bash
/var/www/html
```

---

# Rôle du serveur PHP

Le fichier PHP agit comme un **réceptionniste numérique**.

Il permet :

* de recevoir les données envoyées par l’ESP32
* d’enregistrer les informations
* d’afficher les données sur le site web
* de contrôler les composants à distance



# Partie électronique

# Composants utilisés

| Composant     | Description                |
| ------------- | -------------------------- |
| ESP32         | Carte microcontrôleur WiFi |
| LED           | Indicateur lumineux        |
| Résistance    | Protection LED             |
| Buzzer        | Signal sonore              |
| Breadboard    | Prototype                  |
| Câbles Dupont | Connexions                 |

---

# Test de la LED

# Objectif

Vérifier :

* le fonctionnement de l’ESP32
* les GPIO
* le téléversement du programme

# Code de test LED

```cpp
int led = 2;

void setup() {
  pinMode(led, OUTPUT);
}

void loop() {
  digitalWrite(led, HIGH);
  delay(1000);
  digitalWrite(led, LOW);
  delay(1000);
}
```

# Exemple LED

![LED ESP32](https://images.unsplash.com/photo-1553406830-ef2513450d76?q=80\&w=1200\&auto=format\&fit=crop)



# Test du buzzer

# Objectif

Tester les sorties numériques et le signal sonore.

# Code de test Buzzer

```cpp
int buzzer = 15;

void setup() {
  pinMode(buzzer, OUTPUT);
}

void loop() {
  digitalWrite(buzzer, HIGH);
  delay(1000);
  digitalWrite(buzzer, LOW);
  delay(1000);
}
```

---

# Connexion WiFi ESP32

L’ESP32 se connecte au réseau WiFi pour communiquer avec le serveur.

# Étapes

1. Connexion au WiFi
2. Envoi des données HTTP
3. Réception par PHP
4. Affichage sur le site

---

# Interface Web

Le site web permet :

* d’afficher la dernière valeur reçue
* de rafraîchir automatiquement la page
* d’allumer la LED
* d’activer le buzzer

# Interface HTML/CSS

```html
<title>Valeur Arduino</title>
<style>
body {
    font-family: Arial, sans-serif;
    text-align: center;
    margin-top: 50px;
}

.valeur {
    font-size: 2em;
    color: #f87171;
}
</style>
```

# Exemple d’interface Web

![Dashboard Web](https://images.unsplash.com/photo-1555949963-aa79dcee981c?q=80\&w=1200\&auto=format\&fit=crop)

---

# Fonctionnement complet

# Cycle du système

```text
1. L’ESP32 démarre
2. Connexion au WiFi
3. Activation LED/Buzzer
4. Envoi des données au serveur
5. PHP reçoit les données
6. Le site affiche les valeurs
7. L’utilisateur contrôle les composants
```

---

# Structure du projet

```text
📁 Projet-IoT
 ┣ 📂 esp32
 ┃ ┗ 📜 main.ino
 ┣ 📂 web
 ┃ ┣ 📜 index.php
 ┃ ┣ 📜 style.css
 ┃ ┗ 📜 save.php
 ┣ 📜 README.md
 ┗ 📜 schema.png
```

---

# Sécurité et améliorations futures

# Améliorations possibles

* Ajouter une base de données MySQL
* Utiliser MQTT
* Ajouter un capteur de température
* Ajouter un système de login
* Héberger le serveur sur le cloud
* Ajouter HTTPS
* Contrôle en temps réel avec WebSocket

---

# Résultat final

Communication ESP32 ↔ Serveur

Affichage temps réel

Contrôle LED et buzzer

ébergement sur Ubuntu

Projet IoT complet

---

# Auteur

# TORIX200

Projet réalisé dans le cadre d’un apprentissage IoT avec ESP32 et serveur web.

---

# ⭐ Soutenir le projet

Si le projet vous plaît :

⭐ Mettez une étoile au dépôt GitHub

🍴 Forkez le projet

📢 Partagez-le

---

# 📜 Licence

Projet open-source sous licence MIT.
