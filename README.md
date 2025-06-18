# Etapes_de_validation_avant_PCB  

## Objectif Général
Avant de réaliser directement le PCB de la boîte noire et de la station de contrôle, nous avons choisi de suivre une démarche progressive. L’objectif était de bien maîtriser la communication I2C et le fonctionnement du microcontrôleur ATmega328P.  
Tester les fonctionnalités sur breadboard avec des composants simples (comme un bouton, une LED, un MPU6050 ou un LCD) permet plus de flexibilité et facilite le débogage. Contrairement au PCB, où les composants sont soudés, la breadboard permet des modifications rapides.  
Cette approche nous a permis de valider chaque étape avant l'intégration finale sur le PCB, en réduisant les risques d’erreurs matérielles ou logicielles.

---

## Étapes de Réalisation 

###  Étape 1 : Communication I2C entre deux Arduino (Test de base)

####  Objectif :
Valider le **fonctionnement de la communication I2C** entre deux microcontrôleurs en utilisant un exemple simple : un bouton poussoir et une LED.

####  Composants utilisés :
- 2 cartes **Arduino UNO** 
- 1 bouton poussoir (sur le maître)  
- 1 LED (sur l’esclave)  
- Câblage SDA/SCL entre les deux cartes  

####  Fonctionnement :
- L’Arduino **maître** lit l’état d’un bouton poussoir connecté en entrée.
- Cet état (appuyé ou relâché) est transmis à l’Arduino **esclave** via le protocole I2C.
- L’esclave reçoit cette donnée et **contrôle une LED** : elle s’allume si le bouton est appuyé, s’éteint sinon.

####  But de l'étape :
- Apprendre à configurer le bus I2C (maître/esclave).
- Vérifier la synchronisation et la fiabilité de la communication.
- Observer une réponse simple à un signal I2C.
  
#### le montage 
(![WhatsApp Image 2025-06-18 at 11 28 38 (1) (2)](https://github.com/user-attachments/assets/88f6527a-9f2b-40c0-a4ea-c1e3489a3cf6) 

#### le resultat
[inserer la video ici](https://github.com/user-attachments/assets/2d7efab8-e485-40d1-af62-1af35d8c8034)

---

###  Étape 2 : Remplacement par des modules réels (MPU6050 et LCD)

####  Objectif :
Simuler une application plus réaliste en utilisant des **capteurs réels(MPU6050)** et un **afficheur(lCD)**, tout en gardant la communication I2C entre deux cartes.

####  Composants utilisés :
- MPU6050 (capteur accéléromètre/gyroscope) sur le **maître**
- Écran LCD (type I2C 16x2) sur l’**esclave**
- Deux cartes Arduino

####  Fonctionnement :
- Le capteur **MPU6050** collecte les données d’accélération et de rotation.
- Ces données sont lues par l’Arduino **maître** via I2C.
- Le maître envoie ensuite les valeurs traitées à l’**esclave**.
- L’Arduino esclave reçoit les données et les affiche sur le **LCD**.

####  But de l'étape :
- Remplacer des composants de test par des modules **intelligents**.
- Manipuler un **capteur complexe** avec acquisition de données.
- Gérer l'affichage distant d'informations, toujours via I2C.
- Approfondir le protocole I2C dans un cas concret (multi-esclaves potentiels, synchronisation).
- 
#### Le montage
![WhatsApp Image 2025-06-18 at 11 45 24](https://github.com/user-attachments/assets/4bf55be3-fb1c-43e9-98be-2359a4609619)  

#### Le resultat
[la video ](https://github.com/user-attachments/assets/ff466a56-6247-4dd7-9b3b-220b9bc93346)

---

###  Étape 3 : Intégration avec ATmega328P (préparation au PCB)

####  Objectif :
Remplacer la carte Arduino par le **microcontrôleur brut** (ATmega328P), afin de simuler les conditions réelles d’un circuit imprimé.

####  Composants utilisés :
- 2× ATmega328P   
- 2× Quartz   
- 4× Condensateurs 22 pF   
- 1× MPU6050  
- 1× Écran LCD 16x2 avec interface I2C   
- 2× Boutons poussoirs  
- 2× Résistances 10 kΩ   
- Fils de connexion (Dupont)  
- Breadboard  

####  Fonctionnement :
- L’ATmega328P est programmé avec le même code que celui utilisé sur une carte Arduino, à l’aide d’un programmateur externe (comme USBasp ou Arduino as ISP).  
- Les deux ATmega328P communiquent via le protocole I2C :
    - L’un joue le rôle de maître (elle collecte les données du MPU6050).  
    - L’autre joue le rôle d’esclave (elle affiche les données sur un écran LCD I2C).  
- Les microcontrôleurs sont utilisés en mode "standalone" (hors carte de développement) :
- Connectés sur breadboard avec :
    - Un quartz et deux condensateurs 22 pF pour chaque ATMEGA328P pour générer l’horloge.
    - Une alimentation 5V stable.
    - Un bouton poussoir relié à la broche RESET de chaque ATmega.
    - Une résistance de 10 kΩ connectée entre la broche RESET et VCC, pour garantir un redémarrage stable.

####  But de l'étape :
- S’assurer que le microcontrôleur fonctionne correctement en **mode autonome**.
- Tester la communication I2C dans les **conditions matérielles réelles** du futur PCB.
- Préparer l’intégration finale des composants sur un **PCB personnalisé**.

####  Le montage
l'image de montage

####  Le resultat
la video

---

##  Pourquoi cette Démarche ?
La réalisation d’un PCB nécessite des choix précis de composants et un bon fonctionnement garanti **en amont**. Cette démarche par étapes nous a permis de :

- Identifier les erreurs éventuelles (bruit sur la ligne I2C, mauvais câblage, alimentation instable…).
- Tester progressivement les modules dans un environnement de développement.
- Réduire le risque d’erreur lors de la conception du PCB.
- Avoir une base fonctionnelle avant le passage à la fabrication.

---




---


