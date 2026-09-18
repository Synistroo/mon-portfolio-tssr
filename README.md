# Portfolio Technique — Technicien Supérieur Systèmes & Réseaux

> **À la recherche d'une alternance TSSR** | Reconversion professionnelle

## 👤 À propos de moi
Après **7 ans d'expérience dans le secteur de la couverture**, j'ai développé une grande rigueur, le sens de la sécurité et une forte capacité d'adaptation en travail d'équipe. Passionné par le numérique et l'administration système, j'ai entrepris une reconversion professionnelle vers les métiers de l'informatique pour valider le titre professionnel **TSSR (Technicien Supérieur Systèmes et Réseaux)**.

Ce dépôt regroupe mes travaux pratiques, mes maquettes d'infrastructures (VMs, serveurs AD DS/DHCP/DNS, topologies Cisco Packet Tracer) ainsi que la documentation technique associée.

---

## 🛠️ Compétences & Technologies
- **Systèmes :** Windows Server 2019 (Active Directory DS, DNS, DHCP, Gestion des droits NTFS / Partages), Windows 10
- **Réseau & Interconnexion :** Cisco Packet Tracer (Commutation L2, Routage L3, IP Statiques & Passerelles)
- **Virtualisation :** VirtualBox (Réseau interne / Isolation)
- **Sécurité & Analyse :** Notions d'attaque L2/L3 (ARP Spoofing, IP Spoofing) et stratégies de sécurisation (DAI, ACL, Segmentation)
- **Méthodologie :** Documentation technique, fiches de procédure, recette et validation client

---

## 📂 Mes Projets pratiques

---

### 📁 Projet 1 : Interconnexion de Réseaux & Analyse de Sécurité (Cisco Packet Tracer)

Mise en place d'une infrastructure de réseau local interconnectant deux sous-réseaux d'entreprise via un routeur central.

#### 📐 Topologie Réseau
- **LAN 1 (Agence / Réseau d'origine) — `192.168.1.0/24` :**
  - Switch Cisco 2960 interconnectant `PC1` (`192.168.1.1`) et `PC2` (`192.168.1.2`).
  - Passerelle par défaut : Interface `Gi0/0/0` du routeur (`192.168.1.254`).
- **LAN 2 (Extension / Nouveau secteur) — `192.168.2.0/24` :**
  - Switch Cisco 2960 interconnectant `PC3` (`192.168.2.1`) et `PC4` (`192.168.2.2`).
  - Passerelle par défaut : Interface `Gi0/0/1` du routeur (`192.168.2.254`).

#### 💡 Configuration & Rôles des Équipements
1. **Terminaux (PC) :** Configuration statique des IP, masques (`255.255.255.0`) et passerelles par défaut.
2. **Switches (Niveau 2) :** Commutation locale via adresses MAC.
3. **Routeur (Niveau 3) :** Routage inter-LAN via l'activation (`no shutdown`) et l'adressage des interfaces virtuelles/physiques.

#### 🛡️ Analyse des Menaces & Contre-Mesures TSSR
- **Attaque 1 : ARP Spoofing (Man-In-The-Middle)**
  - *Risque :* Empoisonnement du cache ARP pour intercepter le trafic entre un poste et la passerelle.
  - *Contre-mesure :* Activation du **DAI (Dynamic ARP Inspection)** sur les commutateurs Cisco.
- **Attaque 2 : IP Spoofing & Absence de filtrage**
  - *Risque :* Absence d'ACL permettant la libre circulation de flux suspects (ex: propagation de ransomware).
  - *Contre-mesure :* Mise en place d'**ACL (Access Control Lists)** sur le routeur et segmentation par **VLANs**.

---

### 📁 Projet 2 : Déploiement d'une Infrastructure Windows Server 2019 (Entreprise "Rue25")

Création d'un environnement d'entreprise complet sous VirtualBox intégrant un contrôleur de domaine, un serveur DHCP/DNS et une politique d'accès sécurisée aux dossiers partagés.

#### 🖥️ Architecture VirtualBox
- **SRV-DC01 (Windows Server 2019) :** IP fixe `192.168.1.2/24` — Domaine `lab.local` (Suffixe UPN : `rue25.com`).
- **CL-WIN10 (Windows 10) :** Configuration réseau automatique (DHCP).
- **Réseau :** Carte réseau interne isolée (`intnet`).

#### ⚙️ Services & Rôles Configurés
1. **AD DS & DNS :** Création du domaine d'entreprise, résolution de noms locale.
2. **DHCP :** Étendue d'adresses configurée de `192.168.1.100` à `192.168.1.200`.
3. **Organisation de l'Active Directory (`Entreprise_OU`) :**
   - **GRP_Direction :** S. BIEN (`sbien`), L. RAZOU (`lrazou`), S. BIEN (`sabiene`)
   - **GRP_Commerciaux :** A. FIRMERIE (`afirmerie`), J. LONGTEMPS (`jlongtemps`), M. TEZ (`mtez`), P. DUNORD (`pdunord`)
   - **GRP_Comptabilité :** V. TYME (`vtyme`), C. DEMER (`cdemer`)
4. **Sécurisation des Partages (Droits Partage & Sécurité NTFS) :**
   - Création de l'arborescence `C:\Partages` (`Direction`, `Commerciaux`, `Comptabilité`).
   - Désactivation de l'héritage NTFS, suppression des accès globaux et attribution stricte des permissions par groupe de sécurité.

#### ✅ Recette & Validation des Tests (Poste Client)
- Intégration du poste `CL-WIN10` au domaine `lab.local` via bail DHCP automatique.
- Connexion avec l'utilisateur `pdunord` (Commercial) :
  - **Succès :** Accès autorisé au dossier `\\SRV-DC01\Commerciaux`.
  - **Sécurité validée :** Refus d'accès (Accès refusé) sur les dossiers `Direction` et `Comptabilité`.

---
