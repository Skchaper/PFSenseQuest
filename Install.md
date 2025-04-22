# Installation du pare-feu pfSense

## Pré-requis

- Une VM hébergeant pfSense avec deux interfaces réseau (une pour le LAN et une pour le WAN)  
- Deux machines clientes (ici une machine Ubuntu24.04LTS et une machine Windows Pro 10)  
- Les deux machines clientes ont une unique interface réseau en mode "réseau interne"  

## Installation

Consulter ce [lien](https://www.it-connect.fr/installation-de-pfsense%EF%BB%BF/)  
ou la documentation officielle [ici](https://docs.netgate.com/pfsense/en/latest/install/netinstaller.html)  

# Configuration réseau valide permettant aux machines internes d’accéder à l'extérieur

## Attribution de l'adresse IP des clients via le DHCP de pfSense

![]()

On peut voir que le client Ubuntu a obtenu la première adresse IP de l'étendue DHCP de pfSense (192.168.1.100).  

## Accès à l'interface web d'administration de pfSense

![]()

# Tester que la machine client peut accéder à l'extérieur

![]()

# Mettre en place une règle de filtrage réseau pour interdire à la machine client de sortir du réseau interne



# Vérifier que la machine client ne peut plus communiquer avec l'extérieur, mais que le poste d'administration peut encore communiquer avec l'extérieur



# Expliquer la règle de filtrage mise en place dans le bloc de texte solution de la quête
