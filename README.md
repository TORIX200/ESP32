Projet : Objet connecté avec ESP32 et serveur web

Dans ce projet, nous allons créer notre propre objet connecté utilisant :

Une carte ESP32 (microcontrôleur avec WiFi intégré)
Un site web créé par nous
Une machine virtuelle Ubuntu servant de serveur
Des composants électroniques simples : une LED et un buzzer

Le but est de permettre à l’ESP32 d’envoyer des données au serveur, qui les affichera sur le site web, et de contrôler des composants via des boutons.

1. Principe de fonctionnement

Le fonctionnement global du système est le suivant :

L’ESP32 exécute un programme et se connecte au réseau WiFi.
Il envoie une information vers le serveur web.
Le serveur reçoit la donnée.
Le site web affiche la valeur reçue.

Schéma :
ESP32 → Internet → Serveur Ubuntu → Site Web

2. Pourquoi utiliser une machine virtuelle Ubuntu ?

Un site web a besoin d’un serveur pour fonctionner. Au lieu d’utiliser un serveur physique, nous pouvons créer une machine virtuelle (VM).

C’est un ordinateur installé à l’intérieur de votre PC principal.
Avantages :
Aucun risque pour votre PC principal
Facile à recommencer en cas d’erreur
Très utilisé dans le monde professionnel

Logiciels pour créer une VM :

VirtualBox
VMware

La VM Ubuntu servira de serveur web local.

3. Installation du serveur web

Le serveur web permet :

D’héberger le site
De recevoir les données envoyées par l’ESP32

Installation sur Ubuntu :

Ouvrir le terminal et taper :

sudo apt update
sudo apt install apache2 php libapache2-mod-php
Apache : permet d’afficher le site web
PHP : permet de traiter les informations envoyées
libapache2-mod-php : relie Apache et PHP
4. Création du site web

Tous les fichiers du site sont stockés dans :
/var/www/html

Rôle du fichier PHP principal :

Recevoir les données envoyées par l’ESP32
Les enregistrer pour affichage sur le site

Il agit comme un réceptionniste numérique.

5. Tester le matériel étape par étape

Il est important de tester progressivement les composants pour trouver plus facilement les erreurs :

Tester la LED
Tester le buzzer
Ajouter Internet
Fusionner les programmes
6. Première étape : Câblage et test de la LED

Rôle de la LED :
Vérifier que :

L’ESP32 fonctionne
Le programme est correctement envoyé
Les sorties GPIO fonctionnent

Programme de test :

int led = 2;

void setup() {
  pinMode(led, OUTPUT);
}

void loop() {
  digitalWrite(led, HIGH); // LED allumée
  delay(1000);             // 1 seconde
  digitalWrite(led, LOW);  // LED éteinte
  delay(1000);             // 1 seconde
}
7. Deuxième étape : Test du buzzer

Rôle du buzzer :

Produire un son
Vérifier les signaux électriques et sorties numériques

Programme de test :

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

Si un son est entendu, le buzzer fonctionne.

8. Connexion WiFi de l’ESP32 et communication avec le serveur

L’ESP32 intègre le WiFi et peut donc communiquer à distance.

PHP pour recevoir et afficher les valeurs :

<?php
error_reporting(E_ALL);
ini_set('display_errors', 1);

$file = __DIR__ . "/valeur.txt";

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    if (isset($_POST['valeur'])) {
        $valeur = $_POST['valeur'];
        $result = file_put_contents($file, $valeur);
        echo ($result === false) ? "Erreur écriture fichier" : "Valeur enregistrée : $valeur";
    } else {
        echo "POST reçu mais pas de valeur";
    }
    exit;
}

if (file_exists($file)) {
    $valeur = file_get_contents($file);
    echo "Dernière valeur reçue : " . htmlspecialchars($valeur);
} else {
    echo "Aucune valeur reçue pour l'instant.";
}
?>

HTML pour le site web :

Affiche la dernière valeur reçue
Rafraîchit automatiquement toutes les 5 secondes
Boutons pour Allumer LED et Allumer Buzzer
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Valeur Arduino</title>
    <meta http-equiv="refresh" content="5">
    <style>
        body { font-family: Arial, sans-serif; text-align: center; margin-top: 50px; }
        .valeur { font-size: 2em; color: #f87171; } /* rouge néon */
    </style>
</head>
<body>
    <h1>Dernière valeur reçue de l'Arduino</h1>
    <div class="valeur"><?php echo $valeur; ?></div>
    <p>La page se rafraîchit automatiquement toutes les 5 secondes.</p>
    <button onclick="fetch('http://IP_ESP32/led')">Allumer LED</button>
    <button onclick="fetch('http://IP_ESP32/son')">Allumer Buzzer</button>
</body>
</html>
9. Programme final combiné
Allume la LED et active le buzzer
Envoie les données au serveur
Les boutons sur le site déclenchent LED ou buzzer
10. Fonctionnement complet du système
L’ESP32 démarre
Il rejoint le WiFi
Il allume la LED et le buzzer
Il envoie une donnée au serveur Ubuntu
PHP enregistre la donnée
Le site web affiche la valeur
L’utilisateur peut contrôler LED et buzzer via le site
