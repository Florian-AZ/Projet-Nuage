# ☁️ Secure Enterprise Cloud Infrastructure (Nextcloud + Active Directory + Tailscale)

## 📝 Description du Projet

Ce projet consiste en la mise en place d'une infrastructure de **Cloud Privé Souverain** et sécurisé pour l'entreprise. Il combine la puissance collaborative de **Nextcloud** pour la gestion de fichiers, la centralisation des identités via **Active Directory (Windows Server)**, et un maillage réseau sécurisé "Zero-Trust" grâce au VPN Mesh **Tailscale**.

L'objectif principal est de permettre à des collaborateurs d'accéder au domaine et aux outils de manière transparente, qu'ils soient sur le réseau physique de l'entreprise ou en télétravail, sans jamais exposer les serveurs sur l'internet public.

---

## 🏗️ Architecture du Réseau

L'infrastructure repose sur un modèle hybride LAN / WAN :

1. **Gestion des Identités (IAM) :** Un contrôleur de domaine **Windows Server (Active Directory)** qui centralise les comptes utilisateurs, les politiques de sécurité (GPO) et les droits d'accès.
2. **Cloud Collaboratif :** Une instance **Nextcloud** interconnectée avec l'Active Directory (via LDAP/AD) pour permettre un accès unifié (Single Sign-On - SSO) aux documents de l'entreprise.
3. **Connectivité Hybride (Local vs Distant) :** * **En Local :** Les clients situés sur le réseau de l'entreprise communiquent et s'authentifient **en direct** avec l'Active Directory via le commutateur/routeur local.
   * **À Distance :** L'interconnexion sécurisée est assurée par un réseau privé virtuel basé sur **Tailscale (WireGuard)**. Toutes les machines distantes font partie du *Tailnet*, acheminant les flux de manière transparente.

---

## 🚀 Fonctionnalités Clés

* 🌐 **Routage Intelligent (LAN/VPN) :** Connexion directe et rapide au bureau, bascule automatique et sécurisée sur Tailscale à l'extérieur.
* 🔐 **Architecture Zero-Trust (Distant) :** Aucun port ouvert sur la box/routeur public pour les accès distants. Tout passe par le tunnel chiffré.
* 👤 **Authentification Centralisée :** Les utilisateurs se connectent à Nextcloud avec leurs identifiants de session Windows (AD).
* 📁 **Partage de Fichiers Souverain :** Alternative sécurisée à Google Drive / OneDrive, avec un contrôle total sur l'hébergement des données.
* 🛠️ **Split DNS distant :** Intégration transparente du DNS de l'Active Directory via la console Tailscale pour une résolution de nom interne automatique chez les clients hors site.

---

## 🛠️ Technologies Utilisées

* **Systèmes :** Windows Server 2022 / Linux (pour Nextcloud)
* **Services Réseau :** Active Directory (AD DS), DNS, LDAP
* **VPN / Réseau :** Tailscale (Protocole WireGuard)
* **Application :** Nextcloud Hub


---

## 🏢 Focus : Fonctionnement en Connexion Locale (LAN)

Lorsque les utilisateurs sont présents physiquement dans les locaux de l'entreprise, l'infrastructure passe automatiquement en flux direct, maximisant les performances et la vitesse de transfert.

### 📝 Définition du Scénario Local

La **connexion locale directe** désigne la situation où un poste client (ex: *Client 1* ou *Client 2*) est connecté au même réseau privé physique que les serveurs. 

Dans ce cas de figure, les paquets de données transitent uniquement par les équipements de commutation internes (**Switch / Wi-Fi**). Les flux n'ont pas besoin de sortir sur l'internet public : ils s'affranchissent totalement du VPN Tailscale et ne sollicitent ni le routeur ni le modem de l'entreprise.

### 🧭 Cheminement Réseau Étape par Étape

Lorsqu'un utilisateur initie une connexion depuis l'intérieur de l'entreprise, le trafic suit le parcours suivant :


[ Client 1 / 2 ] ──(Wi-Fi / Câble)──> [ Switch / Wi-Fi ] ────> [ Serveur AD Entreprise ]

<img width="640" height="675" alt="lan" src="https://github.com/user-attachments/assets/c8be77ff-0f95-458e-9c8e-5aa05f3078c9" />
