
# Laboratoire 6 - Configuration GRE, NAT, SSH 
# Topologie

![Topo](../../topo/rack-d/topo6.png)

# Table d’adressage :

|Equipments|Interface     | IP Address     | Subnet Mask     | Default Gateway | Description
|----------|--------------|---------------|----------------|------------------|------------------|
|ISP |G1/0/1   |10.10.10.18       |255.255.255.248         | N/A|Connexion a internet 
|          |G1/0/2   |10.0.0.29   |255.255.255.252| N/A|Connexion a RACK-D-R1-MTL
|          |G1/0/3   |10.0.0.33   |255.255.255.252| N/A|Connexion a RACK-D-R2-Ottawa
|RACK-D-R1-MTL |G0/0/1   |10.0.0.30       |255.255.255.252           | N/A|Connexion a ISP
|          |G0/0/0   |172.16.70.1   |255.255.255.0| N/A|Connexion au switch RACK D-SW-MTL
|          |Tunnel 1   |172.16.85.1   |255.255.255.252| N/A|Connexion Tunnel au RACK-D-R2-Ottawa
|RACK-D-R2-Ottawa |G0/0/1   |10.0.0.34   |255.255.255.252| N/A|Connexion a ISP
|          |G0/0/0|172.16.80.1|255.255.255.0  | N/A|Connexion au switch RACK D-SW-Ottawa
|          |Tunnel 1   |172.16.85.2   |255.255.255.252| N/A|Connexion Tunnel au RACK-D-R1-MTL
|RACK-D-PC1|Fa0      |172.16.70.100       |255.255.255.0  | 172.16.70.1   |    |
|RACK-D-PC2|Fa0      |172.16.80.100       |255.255.255.0  | 172.16.80.1   |    |

Note: utiliser le serveur 192.168.40.200 pour DNS

# Étape 1 – Configuration des paramètres de base
a. Configurez les noms d’hôte (hostname)

# Étape 2 – Configuration des adresses IP
a. À l’aide du tableau d’adresses IP, configurez les adresses IP.

# Étape 3 – Configuration du routage statique
a. Sur ISP, configurez une route par défaut route entièrement spécifiée pointant vers SW-Internet.

b. Sur RACK-D-R1-MTL, configurez une route par défaut route entièrement spécifiée pointant vers ISP.

c. Sur RACK-D-R2-Ottawa, configurez une route par défaut route entièrement spécifiée pointant vers ISP.

# Étape 4 – Configuration du tunnel GRE
a. Configurer le tunnel GRE entre les routeurs RACK-D-R1-MTL et RACK-D-R2-Ottawa

# Étape 5 – Configuration du routage dynamique 
a. Configurez le routage OSPF sur tous les routeurs RACK-D-R1-MTL et RACK-D-R2-Ottawa.

•   Utilisez le numéro de processus ID 1 et la zone 0.

•   Annoncez dans OSPF uniquement les réseaux connectés, sauf les réseaux qui mène vers ISP.

•   Configurez les interfaces passives aux endroits appropriés.

# Étape 6 – Configuration du NAT sur RACK-D-R1-MTL et RACK-D-R2-Ottawa
a.	Créer une liste d’accès standard nommée NAT sur RACK-D-R1-MTL pour permettre le réseau
172.16.70.0/24 et interdire tout autres réseaux.

b.	Configurer le NAT avec PAT sur l'interface de sortie de RACK-D-R1-MTL.

a.	Créer une liste d’accès standard nommée NAT sur RACK-D-R2-Ottawa pour permettre le réseau
172.16.80.0/24 et interdire tout autres réseaux.

b.	Configurer le NAT avec PAT sur l'interface de sortie de RACK-D-R2-Ottawa.

d.	Tester le NAT avant de continuer.

# Étape 7 – Configuration du QoS
a.	Créer une liste d’accès standard nommée NAT sur RACK-A-R1-MTL pour permettre le réseau
172.16.10.0/24 et interdire tout autres réseaux.

b.	Configurer le NAT avec PAT sur l'interface de sortie de RACK-A-R1-MTL.

a.	Créer une liste d’accès standard nommée NAT sur RACK-A-R2-Ottawa pour permettre le réseau
172.16.20.0/24 et interdire tout autres réseaux.

b.	Configurer le NAT avec PAT sur l'interface de sortie de RACK-A-R2-Ottawa.

d.	Tester le NAT avant de continuer.

# Captures à remettre dans le pigeonnier

a. Vous devez effectuer un traceroute entre le PC RACK-D-PC1 et le PC RACK-D-PC2. Le trafic doit passer à travers le tunnel.

b. Vous devez effectuer un traceroute entre le PC RACK-D-PC1 et google.com. Le trafic ne doit pas passer dans le tunnel.

c. Vous devez effectuer un traceroute entre le PC RACK-D-PC2 et google.com. Le trafic ne doit pas passer dans le tunnel.