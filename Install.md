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

![VirtualBoxVM_LdEGLAqs8W.png](https://github.com/Skchaper/PFSenseQuest/blob/main/Screens/pfSense_Install/VirtualBoxVM_LdEGLAqs8W.png)

On peut voir que le client Ubuntu a obtenu la première adresse IP de l'étendue DHCP de pfSense (192.168.1.100).  

## Accès à l'interface web d'administration de pfSense

Dans un navigateur web, sur le client, taper l'adresse IP de l'interface LAN du pfSense :  

![VirtualBoxVM_8Fhk07khMg.png](https://github.com/Skchaper/PFSenseQuest/blob/main/Screens/pfSense_Install/VirtualBoxVM_8Fhk07khMg.png)

Lors de la première connexion avec le compte "admin", le mot de passe est "pfsense", il vous sera demandé de le modifier après la connexion réussie.  

# Tester que la machine client peut accéder à l'extérieur

Test avec un ping de google (IPv4 et résolution de nom) :  

![VirtualBoxVM_tsr6v0NEC1.png](https://github.com/Skchaper/PFSenseQuest/blob/main/Screens/pfSense_Install/VirtualBoxVM_tsr6v0NEC1.png)

Les pings sont fonctionnels, la machine cliente peut donc accéder vers l'extérieur.  

# Mettre en place une règle de filtrage réseau pour interdire à la machine client de sortir du réseau interne

Pour cette partie, il faut ajouter une règle, ici sur l'interface LAN (celle qui gère le réseau interne), cliquer sur **Firewall** ==> **Rules** ==> **LAN** ==> **Add** :  

![VirtualBoxVM_FkDpJoVrKi.png](https://github.com/Skchaper/PFSenseQuest/blob/main/Screens/pfSense_Install/VirtualBoxVM_FkDpJoVrKi.png)

On souhaite bloquer l'accès à l'extérieur, dans le champ **Action**, sélectionner **Block**. Dans le champ **Interface** choisir **LAN**. Dans le champ **Address Family** choisir **IPv4**. Et enfin dans le champ **Protocol** sélectionner **Any** :   

![VirtualBoxVM_qMccQVoX97.png](https://github.com/Skchaper/PFSenseQuest/blob/main/Screens/pfSense_Install/VirtualBoxVM_qMccQVoX97.png)

Dans la section **Source** sélectionner **Address or Alias** et renseigner l'adresse IPv4 du client. Dans la section suivante **Destination** sélectionner **Any**. Dans la partie **Extra Options** cocher **Log packets that are handled by this rule** pour afficher les logs en lien avec cette règle :  

![VirtualBoxVM_RnXq8hkUfi.png](https://github.com/Skchaper/PFSenseQuest/blob/main/Screens/pfSense_Install/VirtualBoxVM_RnXq8hkUfi.png)

# Vérifier que la machine client ne peut plus communiquer avec l'extérieur, mais que le poste d'administration peut encore communiquer avec l'extérieur

Test d'un ping 8.8.8.8 et d'accès à Youtube par le navigateur :  

![VirtualBoxVM_Cb08k2BC1r.png](https://github.com/Skchaper/PFSenseQuest/blob/main/Screens/pfSense_Install/VirtualBoxVM_Cb08k2BC1r.png)

Test Youtube :  

![VirtualBoxVM_i0bd5yKtk0.png](https://github.com/Skchaper/PFSenseQuest/blob/main/Screens/pfSense_Install/VirtualBoxVM_i0bd5yKtk0.png)

Le client ne peut plus accéder à l'extérieur du LAN.  

# Expliquer la règle de filtrage mise en place dans le bloc de texte solution de la quête
