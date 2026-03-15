# 🌐 Architecture Réseau : MPLS L3VPN Multi-Tenancy

<div align="center">
  <img src="https://img.shields.io/badge/GNS3-Simulation-blue?style=for-the-badge&logo=gns3" alt="GNS3">
  <img src="https://img.shields.io/badge/Cisco-IOS-red?style=for-the-badge&logo=cisco" alt="Cisco">
  <img src="https://img.shields.io/badge/MPLS-L3VPN-lightgrey?style=for-the-badge" alt="MPLS">
  <img src="https://img.shields.io/badge/MP--BGP-Overlay-orange?style=for-the-badge" alt="BGP">
</div>

---

## 👤 Auteur
**Nelson Bandos** - *Administrateur Réseau | Sécurité Réseau*
* 🔗 **Portfolio** : [nelson-bandos.vercel.app](https://nelson-bandos.vercel.app)
* 💼 **LinkedIn** : [nelson-bandos](https://www.linkedin.com/in/nelson-bandos)
* 🐙 **GitHub** : [Nelson2410](https://github.com/Nelson2410)

---

## Description du Projet
Ce laboratoire illustre le déploiement d'une architecture de type **Service Provider** offrant un service **L3VPN** à deux clients distincts (**Entreprise A** et **Entreprise B**).

L'objectif est de garantir une isolation stricte des flux sur un backbone partagé en utilisant :
- **Underlay** : OSPF & LDP pour la connectivité interne.
- **Overlay** : MP-BGP (VPNv4) pour le transport des routes clients.
- **Virtualisation** : Instances VRF sur les routeurs PE.

## Topologie
![Topologie MPLS VPN L3](1%20-%20Documentation/1%20-%20DAT_Topologie/Topo%20MPLS.png)

## 📂 Structure du Projet
```bash
.
├── 1 - Documentation/
│   ├── 1 - DAT_Topologie/       # DAT, Topologie
│   └── 2 - Resultats/           # Preuves de fonctionnement
├── 2 - Configurations/
│   ├── 1- Backbone/             # Configs P, PE-1, PE-2
│   └── 2 - Clients/             # Configs CE (Entreprise A & B)
└── README.md                    # Documentation principale
```

## Plan d'Adressage

### Backbone (Interface Loopback 0)
| Équipement | IP (Router-ID) | AS |
| :--- | :--- | :--- |
| **PE-1** | 1.1.1.1/32 | 65000 |
| **P**    | 2.2.2.2/32 | 65000 |
| **PE-2** | 3.3.3.3/32 | 65000 |

### Interconnexions PE-CE
| Client | Liaison | Sous-réseau |
| :--- | :--- | :--- |
| **Entreprise A** | PE-1 <-> CE-A1 | 172.16.10.0/30 |
| **Entreprise A** | PE-2 <-> CE-A2 | 172.16.20.0/30 |
| **Entreprise B** | PE-1 <-> CE-B1 | 192.168.10.0/30 |

## Méthodologie de Déploiement

1. **Infrastructure Underlay** : Connectivité IP (OSPF) et activation de la commutation de labels (LDP).
2. **Virtualisation (VRF)** : Création des instances `VPN_CLIENT_A` (RD 100:1) et `VPN_CLIENT_B` (RD 200:1).
3. **Control Plane Overlay** : Configuration des sessions iBGP VPNv4 entre les PE.
4. **Data Plane Client** : Configuration du routage statique et redistribution dans BGP.

## Preuves de Fonctionnement (Captures GNS3)

### 1. Analyse du Trafic (Underlay)
L'activation d'OSPF et LDP est confirmée par la capture Wireshark. On y voit les paquets Hello circulant entre les équipements du cœur de réseau.

![Capture Wireshark OSPF/LDP](1%20-%20Documentation/2%20-%20Resultats/capture1.png)
*Flux de contrôle : Adjacences OSPF et découvertes de voisins LDP.*

![Détail Hello Message LDP](1%20-%20Documentation/2%20-%20Resultats/Capture2.png)
*Détail protocolaire : Header LDP Hello Message (LSR ID : 2.2.2.2).*

### 2. État du Plan de Contrôle (Backbone)
Vérification des adjacences MPLS et de la session MP-BGP.

![Voisinage LDP](1%20-%20Documentation/2%20-%20Resultats/capture3.png)
*Sortie `show mpls ldp neighbor` : Session opérationnelle entre les routeurs P et PE.*

![Session MP-BGP VPNv4](1%20-%20Documentation/2%20-%20Resultats/capture4.png)
*Sortie `show bgp vpnv4 unicast all summary` : État des voisins BGP.*

### 3. Routage Client (Isolation VRF)
Validation de la table de routage spécifique au client A sur le routeur PE-1.

![Table de Routage VRF A](1%20-%20Documentation/2%20-%20Resultats/capture5.png)
*Sortie `show ip route vrf VPN_CLIENT_A` : Les routes LAN sont apprises et isolées des autres clients.*

<br><b><i>Merci pour votre attention !</i></b><br>
<br><b><i>Hâte de connaître vos retours et suggestions pour améliorer ce laboratoire.</i></b><br>