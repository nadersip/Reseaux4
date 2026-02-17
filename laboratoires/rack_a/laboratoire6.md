
# Laboratoire 6 - Configuration des ACL étendues, OSPF, SSH et NAT

# Topologie

![Topo](../../topo/rack-a/topo6.png)

# Table d’adressage :

|Equipments|Interface     | IP Address     | Subnet Mask     | Default Gateway | Description
|----------|--------------|---------------|----------------|------------------|------------------|
|ISB |G1/0/1   |10.10.10.2       |255.255.255.248         | N/A|Connexion a internet 
|          |G1/0/2   |10.0.0.5   |255.255.255.252| N/A|Connexion a RACK-A-R1-MTL
|          |G1/0/3   |10.0.0.9   |255.255.255.252| N/A|Connexion a RACK-A-R2-Ottawa
|RACK-A-R1-MTL |G0/0/1   |10.0.0.6       |255.255.255.252           | N/A|Connexion a ISP
|          |G0/0/0   |172.16.10.1   |255.255.255.0| N/A|Connexion au switch RACK A-SW-MTL
|RACK-A-R2-Ottawa |G0/0/1   |10.0.0.10   |255.255.255.252| N/A|Connexion a ISP
|          |G0/0/0|172.16.20.1|255.255.255.0  | N/A|Connexion au switch RACK A-SW-Ottawa
|RACK-A-PC1|Fa0      |DHCP       |DHCP  | DHCP   |    |
|RACK-A-PC2|Fa0      |DHCP       |DHCP  | DHCP   |    |



# Étape 1 – Configuration des paramètres de base
a. Configurez les noms d’hôte (hostname)

# Étape 2 – Configuration des adresses IP
a. À l’aide du tableau d’adresses IP, configurez les adresses IP.

# Étape 3 – Configuration du routage statique
a. Sur ISP, configurez une route par défaut route entièrement spécifiée pointant vers SW-Internet.

# Étape 4 – Configuration du tunnel GRE
a. Configurer le tunnel GRE entre les routeurs RACK-A-R1-MTL et RACK-A-R2-Ottawa

# Étape 5 – Configuration du routage dynamique 
a. Configurez le routage OSPF sur tous les routeurs et ISP.

•   Utilisez le numéro de processus ID 1 et la zone 0.

•   Annoncez dans OSPF uniquement les réseaux connectés, sauf le réseau qui mène vers SW-Internet.

•   Configurez les interfaces passives aux endroits appropriés.

b. Sur ISP, utilisez la commande appropriée pour propager cette route par défaut à ses voisins OSPF.

# Étape 6 – Configuration du NAT
a.	Créer une liste d’accès standard nommée NAT pour permettre les réseaux
172.16.10.0/24, 172.16.20.0/24 et interdire tout autres réseaux.

b.	Créer un NAT pool nommée NAT-POOL entre les adresses 10.10.10.3 et 10.10.10.5.

c.	Créer un NAT statique pour le routeur RACK-A-R1-MTL avec l’adresse 10.10.10.6.

d.	Tester le NAT avant de continuer.

# Étape 7 – Configuration du DHCP 
Le serveur DHCP est déjà configuré pour vous. Son adresse IP est la suivante : 192.168.10.200
Vous devez configurer IP Helper pour qu’il pointe vers ce serveur DHCP.

# Étape 8 – Configuration de SSH 					
a. Configurez SSH sur le routeur RACK-A-R1-MTL.

b. Définissez le nom de domaine à rack-a.local

c. Créez un utilisateur cisco avec le mot de passe cisco1234.

d. Créez une clé RSA 2048 bits.

e. Version 2

f. Paramétrez toutes les lignes vty 0 4 pour utiliser SSH et un login local

