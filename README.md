# 🌐 Projet IoT : ESP32 + Serveur Web Ubuntu

![ESP32](https://images.unsplash.com/photo-1553406830-ef2513450d76?q=80\&w=1200\&auto=format\&fit=crop)

## 📌 Description

Ce projet consiste à créer un **objet connecté (IoT)** basé sur une carte **ESP32**, un **serveur Ubuntu**, et un **site web interactif**.

L’objectif :

* 📡 Envoyer des données depuis l’ESP32
* 💡 Contrôler une LED à distance
* 🔊 Activer un buzzer via le web
* 🌍 Afficher les données en temps réel

---

# 🧠 Architecture du système

## 🔄 Schéma global

![IoT Architecture](https://upload.wikimedia.org/wikipedia/commons/3/3b/Internet_of_Things.jpg)

```text
ESP32 → WiFi → Serveur Ubuntu (Apache + PHP) → Site Web
```

---

# ⚙️ Technologies utilisées

| Technologie | Rôle                   |
| ----------- | ---------------------- |
| ESP32       | Microcontrôleur WiFi   |
| Ubuntu      | Serveur web            |
| Apache      | Hébergement            |
| PHP         | Traitement des données |
| HTML/CSS    | Interface web          |

---

# 🖥️ Serveur Ubuntu (VM)

![Ubuntu Server](https://images.unsplash.com/photo-1588702547919-26089e690ecc?q=80\&w=1200\&auto=format\&fit=crop)

Installation :

```bash
sudo apt update
sudo apt install apache2 php libapache2-mod-php
```

📁 Dossier web :

```bash
/var/www/html
```

---

# 💡 Test LED

## 🔌 Câblage

![LED Circuit](https://upload.wikimedia.org/wikipedia/commons/3/3d/LED_circuit.svg)

## 🧪 Code

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

---

# 🔊 Test Buzzer

## 🔌 Câblage

![Buzzer](https://upload.wikimedia.org/wikipedia/commons/6/6e/Piezo_buzzer.svg)

## 🧪 Code

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

# 🌐 Interface Web

![Dashboard Web](https://images.unsplash.com/photo-1555949963-aa79dcee981c?q=80\&w=1200\&auto=format\&fit=crop)

### Fonctionnalités :

* 📊 Affichage des données ESP32
* 🔄 Rafraîchissement automatique
* 💡 Bouton LED
* 🔊 Bouton buzzer

---

# 🔄 Fonctionnement global

```text
1. ESP32 démarre
2. Connexion WiFi
3. Envoi des données
4. PHP reçoit les données
5. Site web affiche les infos
6. L’utilisateur contrôle LED & buzzer
```

---

# 👨‍💻 Auteur

**TORIX200**

Projet IoT complet ESP32 + serveur web Ubuntu

---

# ⭐ Améliorations possibles

* 📡 MQTT
* 🗄️ Base de données MySQL
* 🔐 Authentification
* ☁️ Cloud hosting
* 📱 Application mobile

