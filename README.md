<p align="center">
  <img src="Logo%20CallMe.png" alt="Logo CallMe" width="300">
</p>


# Infrastructure CallMe

## Infrastructure hybride, virtualisée et sécurisée d’un centre d’appel

CallMe est un projet de conception et de déploiement d’une infrastructure informatique pour un centre d’appel de 60 collaborateurs.

Le projet couvre les systèmes, les réseaux, la virtualisation, la cybersécurité, la supervision, l’automatisation et la mise en place d’un PRA dans AWS.



## Contexte du projet

## 🎯 Contexte du projet

CallMe est un centre d’appel présent sur plusieurs sites en France.

Le projet concerne le site de Narbonne, composé de 45 agents, 10 superviseurs et 5 administrateurs.

Le site de Narbonne a été choisi comme **site pilote pour la mise en place d’une infrastructure hybride**. Celle-ci combine une infrastructure locale virtualisée sous **Proxmox VE** et un environnement **AWS** utilisé pour le plan de reprise d’activité (PRA).

Cette architecture pilote permet de tester et de valider les solutions techniques, la sécurité, la supervision et le PRA avant d’envisager leur déploiement sur les autres sites de CallMe.

L’objectif est de disposer d’une infrastructure sécurisée, segmentée, supervisée et facile à administrer, capable de maintenir ou de reprendre les services essentiels en cas d’incident majeur.



## Architecture technique

L’infrastructure CallMe combine un environnement virtualisé local et un environnement de reprise dans AWS.

Les principales solutions utilisées sont :

- **Virtualisation** : Proxmox VE
- **Réseau** : pfSense, VLAN & DHCP
- **Annuaire et DNS** : Windows Server AD DS
- **Gestion du parc et support** : GLPI
- **Administration distante** : Apache Guacamole
- **Supervision** : Centreon
- **Automatisation** : Ansible
- **Sécurité** : Wazuh, Suricata, Fail2ban et GPO
- **PRA** : AWS et WireGuard



## 🌐 Segmentation réseau

Le réseau est séparé en plusieurs VLAN. Cette segmentation permet d’isoler les différents usages et de mieux contrôler les communications.


| VLAN 10 | Agents | 192.168.10.0/24 |

| VLAN 20 | DMZ | 192.168.20.0/24 |

| VLAN 30 | Administration | 192.168.30.0/24 |

| VLAN 40 | Wi-Fi Entreprise | Réseau dédié |

| VLAN 50 | BYOD | Réseau isolé |

**pfSense** assure le routage entre les VLAN et contrôle les flux autorisés



## 🔐 Sécurisation de l’infrastructure

Plusieurs niveaux de sécurité ont été mis en place pour protéger l’infrastructure

Les **VLAN** permettent de séparer les différents réseaux

**pfSense** contrôle les communications entre ces réseaux et assure également le service **DHCP sur certaines interfaces**

**Suricata** détecte les activités réseau suspectes

**Wazuh** centralise et analyse les événements de sécurité

**Fail2ban** bloque certaines tentatives d’accès malveillantes

Les **GPO** permettent de renforcer la sécurité et d’appliquer des règles aux postes Windows

**WireGuard** sécurise la connexion entre l’infrastructure locale et le PRA hébergé dans **AWS**



## Automatisation

**Ansible** est utilisé pour automatiser certaines tâches d’administration sur les serveurs Linux.

Des playbooks ont été créés pour :

- déployer les agents **Wazuh**
- effectuer les mises à jour des serveurs Linux

Cette automatisation permet de gagner du temps et de limiter les erreurs de configuration.



## ☁️ Plan de reprise d’activité AWS

Un **PRA (Plan de Reprise d’Activité)** a été mis en place dans AWS afin de pouvoir restaurer les services essentiels en cas d’incident majeur sur l’infrastructure locale.

L’environnement AWS comprend :

- un **VPC** dédié au PRA
- un **sous-réseau public** pour la passerelle WireGuard
- un **sous-réseau privé** pour les serveurs de reprise
- un serveur **GLPI de reprise**
- un serveur **Active Directory de reprise**
- une passerelle **WireGuard** permettant de relier AWS à l’infrastructure locale

Les communications entre le site de Narbonne et AWS passent par un **tunnel VPN WireGuard sécurisé**.

Des sauvegardes des données et configurations critiques sont également stockées dans **Amazon S3** afin de faciliter la restauration des services.



## 🏗️ Schéma de l’infrastructure

<p align="center">
  <img src="Annexe_B_Architecture_Infrastructure_CallMe.png" alt="Schéma de l'infrastructure CallMe" width="900">
</p>



## ✅ Tests et validation

L’infrastructure a été testée afin de vérifier le fonctionnement des différents services.

Plusieurs tests ont été réalisés :

- communication entre les VLAN et contrôle des règles pfSense — **Annexe N**
- fonctionnement d’AD DS et DNS — **Annexe H**
- application des GPO sur les postes Windows — **Annexes I et O**
- accès et fonctionnement de GLPI — **Annexe E**
- accès distant avec Guacamole — **Annexe G**
- supervision des services avec Centreon — **Annexe J**
- remontée des événements de sécurité dans Wazuh — **Annexe L**
- détection des activités réseau suspectes avec Suricata — **Annexes O et P**
- détection et blocage avec Fail2ban — **Annexes O et P**
- automatisation et mises à jour avec Ansible — **Annexes K et M**
- connexion WireGuard et fonctionnement du PRA AWS — **Annexe Q**

Les principaux tests de sécurité et les preuves de validation de l’infrastructure sont regroupés dans **l’Annexe P — Tests de sécurité et validation de l’infrastructure**.



## 📚 Documentation du projet

Le projet CallMe est accompagné d’une documentation complète comprenant le rapport principal, les procédures techniques, les configurations, les tests et les captures de validation.



### 📄 Rapport principal

Le rapport présente la conception, le déploiement et la validation de l’infrastructure hybride du site pilote CallMe.

➡️ **[Consulter le rapport complet du projet](Rapport_CallMe.pdf)**



### 📘 Annexes complètes

Les annexes viennent en complément du rapport principal. Elles apportent des détails sur les configurations, les procédures de déploiement, les tests réalisés et les preuves de validation de l’infrastructure.

➡️ **[Consulter les annexes complètes du projet](Annexes_CallMe.pdf)**



