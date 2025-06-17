# communication-I2C  
# 🛠️ Projet : Réalisation d’un PCB avec Communication I2C

## 📌 Objectif Général

Ce projet vise à concevoir et réaliser un circuit imprimé (PCB) intégrant une communication I2C entre deux microcontrôleurs. Avant d'arriver à la phase de fabrication, un processus progressif en trois étapes a été suivi. Chaque étape a permis de tester un aspect particulier du système, en remplaçant progressivement les composants jusqu'à atteindre une version miniaturisée et intégrable sur PCB.

---

## 🔁 Étapes de Réalisation

### 🧪 Étape 1 : Communication I2C entre deux Arduino (Test de base)

#### ✅ Objectif :
Valider le **fonctionnement de la communication I2C** entre deux microcontrôleurs en utilisant un exemple simple : un bouton poussoir et une LED.

#### 🧰 Composants utilisés :
- 2 cartes **Arduino UNO**
- 1 bouton poussoir (sur le maître)
- 1 LED (sur l’esclave)
- Câblage SDA/SCL entre les deux cartes

#### ⚙️ Fonctionnement :
- L’Arduino **maître** lit l’état d’un bouton poussoir connecté en entrée.
- Cet état (appuyé ou relâché) est transmis à l’Arduino **esclave** via le protocole I2C.
- L’esclave reçoit cette donnée et **contrôle une LED** : elle s’allume si le bouton est appuyé, s’éteint sinon.

#### 🎯 But de l'étape :
- Apprendre à configurer le bus I2C (maître/esclave).
- Vérifier la synchronisation et la fiabilité de la communication.
- Observer une réponse simple à un signal I2C.

---

### 📈 Étape 2 : Remplacement par des modules réels (MPU6050 et LCD)

#### ✅ Objectif :
Simuler une application plus réaliste en utilisant des **capteurs réels** et un **afficheur**, tout en gardant la communication I2C entre deux cartes.

#### 🧰 Composants utilisés :
- MPU6050 (capteur accéléromètre/gyroscope) sur le **maître**
- Écran LCD (type I2C 16x2) sur l’**esclave**
- Deux cartes Arduino

#### ⚙️ Fonctionnement :
- Le capteur **MPU6050** collecte les données d’accélération et de rotation.
- Ces données sont lues par l’Arduino **maître** via I2C.
- Le maître envoie ensuite les valeurs traitées à l’**esclave**.
- L’Arduino esclave reçoit les données et les affiche sur le **LCD**.

#### 🎯 But de l'étape :
- Remplacer des composants de test par des modules **intelligents**.
- Manipuler un **capteur complexe** avec acquisition de données.
- Gérer l'affichage distant d'informations, toujours via I2C.
- Approfondir le protocole I2C dans un cas concret (multi-esclaves potentiels, synchronisation).

---

### ⚙️ Étape 3 : Intégration avec ATmega328P (préparation au PCB)

#### ✅ Objectif :
Remplacer la carte Arduino par le **microcontrôleur brut** (ATmega328P), afin de simuler les conditions réelles d’un circuit imprimé.

#### 🧰 Composants utilisés :
- Microcontrôleur **ATmega328P** (standalone)
- Oscillateur 16 MHz (ou interne)
- Résistances de pull-up pour I2C
- Programmateur (USBasp, Arduino as ISP, etc.)
- Modules I2C (MPU6050 ou LCD selon les tests)

#### ⚙️ Fonctionnement :
- L’ATmega est programmé avec le même code que celui utilisé sur Arduino.
- Il communique directement avec l’autre Arduino ou avec un autre ATmega via I2C.
- L’objectif est de tester le comportement du microcontrôleur **sans carte de développement**.

#### 🎯 But de l'étape :
- S’assurer que le microcontrôleur fonctionne correctement en **mode autonome**.
- Tester la communication I2C dans les **conditions matérielles réelles** du futur PCB.
- Préparer l’intégration finale des composants sur un **PCB personnalisé**.

---

## 📐 Pourquoi cette Démarche ?

La réalisation d’un PCB nécessite des choix précis de composants et un bon fonctionnement garanti **en amont**. Cette démarche par étapes nous a permis de :

- Identifier les erreurs éventuelles (bruit sur la ligne I2C, mauvais câblage, alimentation instable…).
- Tester progressivement les modules dans un environnement de développement.
- Réduire le risque d’erreur lors de la conception du PCB.
- Avoir une base fonctionnelle avant le passage à la fabrication.

---

## 🎯 Résultat Attendu

À la fin de ces trois étapes, tous les modules sont fonctionnels et la communication I2C est stable. Le passage au PCB peut donc se faire en toute confiance, avec un **design compact** et optimisé autour de l’ATmega328P.

---

## 📷 Images et Schémas (à ajouter par la suite)

- 🧾 Schéma de câblage I2C étape 1
- 📷 Prototype avec MPU6050 + LCD
- 💡 Montage de l’ATmega sur breadboard
- 📘 Schéma PCB final (KiCad, EasyEDA…)

---

## 👩‍💻 Réalisé par

**Hiba El Goumri**  
Étudiante en systèmes embarqués et commande  
ENSA Marrakech

---

## ⚖️ Licence

Ce projet est publié sous licence MIT.  
Vous êtes libre de le modifier, distribuer ou l’utiliser dans vos propres projets.

