# Homelab NAS

Serveur NAS personnel sous **OpenMediaVault**, avec des services hébergés dans des conteneurs **Docker**, et un réseau local monté sans routeur : un câble Ethernet entre le NAS et un PC sous Linux, et un partage de connexion Windows pour accéder à Internet.

## Services
| Service | Rôle | Port |
|---|---|---|
| OpenMediaVault | Administration du NAS | 80 |
| Nextcloud | Cloud personnel (fichiers) | selon la configuration |
| Jellyfin | Médiathèque vidéo | 8096 |
| Immich | Sauvegarde des photos et vidéos | 2283 |
| Tailscale | Accès distant sécurisé | – |

## Le réseau
| Machine | Rôle |
|---|---|---|
| PC Windows 11 | Passerelle Internet (partage de connexion) |
| NAS (OpenMediaVault) | Serveur des services |
| HP (Linux Arch, Omarchy) | Client d'administration |

Deux modes de fonctionnement :
- **Mode NAS direct :** un câble relie le Linux au NAS, avec des IP fixes dans le réseau, sans passerelle ni DNS. Aucun routeur ni Internet n'est nécessaire.
- **Mode Internet :** le Linux (ou le NAS) est branché au PC Windows et reçoit une adresse par le partage de connexion, ce qui permet les mises à jour.

## Ce que j'ai mis en place
- Installation et configuration d'OpenMediaVault, avec une IP fixe configurée par `omv-firstaid`
- Deux profils réseau **NetworkManager** sur le Linux (`nmcli`) : IP fixe pour le NAS, DHCP pour Internet
- Passage d'un profil à l'autre avec de simples alias (`nas-mode`, `internet-mode`)
- Services Nextcloud, Jellyfin et Immich lancés avec Docker
- Diagnostic avec `ping`, `ip -br a` et `nmcli device status`
  
---
© 2026 Enzo Pustoc’h. Tous droits réservés. Ce dépôt est publié pour présenter mon travail : toute réutilisation est interdite sans mon autorisation.
