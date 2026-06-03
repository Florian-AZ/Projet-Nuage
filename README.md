# Projet-Nuage
Infrastructure de Cloud Privé sécurisée combinant Nextcloud pour le partage de fichiers et Active Directory pour la gestion centralisée des utilisateurs. L'ensemble est interconnecté et rendu accessible à distance pour les collaborateurs via le VPN Mesh Tailscale, garantissant une architecture Zero-Trust.

# ☁️ Secure Enterprise Cloud Infrastructure (Nextcloud + Active Directory + Tailscale)

## 📝 Description du Projet

Ce projet consiste en la mise en place d'une infrastructure de **Cloud Privé Souverain** et sécurisé pour l'entreprise. Il combine la puissance collaborative de **Nextcloud** pour la gestion de fichiers, la centralisation des identités via **Active Directory (Windows Server)**, et un maillage réseau sécurisé "Zero-Trust" grâce au VPN Mesh **Tailscale**.

L'objectif principal est de permettre à des collaborateurs distants de se connecter au domaine et d'accéder aux outils collaboratifs de manière totalement transparente, sans jamais exposer les serveurs sur l'internet public.

---

## 🏗️ Architecture du Réseau



L'infrastructure repose sur trois piliers technologiques :

1. **Gestion des Identités (IAM) :** Un contrôleur de domaine **Windows Server (Active Directory)** qui centralise les comptes utilisateurs, les politiques de sécurité (GPO) et les droits d'accès.
2. **Cloud Collaboratif :** Une instance **Nextcloud** interconnectée avec l'Active Directory (via LDAP/AD) pour permettre un accès unifié (Single Sign-On - SSO) aux documents de l'entreprise.
3. **Sécurité & Connectivité :** Un réseau privé virtuel basé sur **Tailscale (WireGuard)**. Toutes les machines (serveurs et postes clients des collaborateurs) font partie d'un même *Tailnet*, sécurisant les flux DNS et de données de bout en bout.

---

## 🚀 Fonctionnalités Clés

* 🔐 **Architecture Zero-Trust :** Aucun port ouvert sur la box/routeur public. Tout passe par le tunnel chiffré de Tailscale.
* 👤 **Authentification Centralisée :** Les utilisateurs se connectent à Nextcloud avec leurs identifiants de session Windows (AD).
* 📁 **Partage de Fichiers Souverain :** Alternative sécurisée à Google Drive / OneDrive, avec un contrôle total sur l'hébergement des données.
* 🌐 **Split DNS distant :** Intégration transparente du DNS de l'Active Directory via la console Tailscale pour une résolution de nom interne automatique chez les clients.

---

## 🛠️ Technologies Utilisées

* **Systèmes :** Windows Server 2022 / Linux (pour Nextcloud)
* **Services Réseau :** Active Directory (AD DS), DNS, LDAP
* **VPN / Réseau :** Tailscale (Protocole WireGuard)
* **Application :** Nextcloud Hub