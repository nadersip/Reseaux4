
# Laboratoire 6 - Configuration GRE, NAT, SSH 
# Topologie

![Topo](../../topo/rack-e/topo6.png)

# Table d’adressage :

|Equipments|Interface     | IP Address     | Subnet Mask     | Default Gateway | Description
|----------|--------------|---------------|----------------|------------------|------------------|
|ISP |G1/0/1   |10.10.10.34       |255.255.255.248         | N/A|Connexion a internet 
|          |G1/0/2   |10.0.0.37   |255.255.255.252| N/A|Connexion a RACK-E-R1-MTL
|          |G1/0/3   |10.0.0.41   |255.255.255.252| N/A|Connexion a RACK-E-R2-Ottawa
|RACK-E-R1-MTL |G0/0/1   |10.0.0.38       |255.255.255.252           | N/A|Connexion a ISP
|          |G0/0/0   |172.16.90.1   |255.255.255.0| N/A|Connexion au switch RACK E-SW-MTL
|          |Tunnel 1   |172.16.105.1   |255.255.255.252| N/A|Connexion Tunnel au RACK-E-R2-Ottawa
|RACK-E-R2-Ottawa |G0/0/1   |10.0.0.42   |255.255.255.252| N/A|Connexion a ISP
|          |G0/0/0|172.16.100.1|255.255.255.0  | N/A|Connexion au switch RACK E-SW-Ottawa
|          |Tunnel 1   |172.16.105.2   |255.255.255.252| N/A|Connexion Tunnel au RACK-E-R1-MTL
|RACK-E-PC1|Fa0      |172.16.90.100       |255.255.255.0  | 172.16.90.1   |    |
|RACK-E-PC2|Fa0      |172.16.100.100       |255.255.255.0  | 172.16.100.1   |    |

Note: utiliser le serveur 192.168.50.200 pour DNS

# Étape 1 – Configuration des paramètres de base
a. Configurez les noms d’hôte (hostname)

# Étape 2 – Configuration des adresses IP
a. À l’aide du tableau d’adresses IP, configurez les adresses IP.

# Étape 3 – Configuration du routage statique
a. Sur ISP, configurez une route par défaut route entièrement spécifiée pointant vers SW-Internet.

b. Sur RACK-E-R1-MTL, configurez une route par défaut route entièrement spécifiée pointant vers ISP.

c. Sur RACK-E-R2-Ottawa, configurez une route par défaut route entièrement spécifiée pointant vers ISP.

# Étape 4 – Configuration du tunnel GRE
a. Configurer le tunnel GRE entre les routeurs RACK-E-R1-MTL et RACK-E-R2-Ottawa

# Étape 5 – Configuration du routage dynamique 
a. Configurez le routage OSPF sur tous les routeurs RACK-E-R1-MTL et RACK-E-R2-Ottawa.

•   Utilisez le numéro de processus ID 1 et la zone 0.

•   Annoncez dans OSPF uniquement les réseaux connectés, sauf les réseaux qui mène vers ISP.

•   Configurez les interfaces passives aux endroits appropriés.

# Étape 6 – Configuration du NAT sur RACK-E-R1-MTL et RACK-E-R2-Ottawa
a.	Créer une liste d’accès standard nommée NAT sur RACK-E-R1-MTL pour permettre le réseau
172.16.90.0/24 et interdire tout autres réseaux.

b.	Configurer le NAT avec PAT sur l'interface de sortie de RACK-E-R1-MTL.

a.	Créer une liste d’accès standard nommée NAT sur RACK-E-R2-Ottawa pour permettre le réseau
172.16.100.0/24 et interdire tout autres réseaux.

b.	Configurer le NAT avec PAT sur l'interface de sortie de RACK-E-R2-Ottawa.

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

a. Vous devez effectuer un traceroute entre le PC RACK-E-PC1 et le PC RACK-E-PC2. Le trafic doit passer à travers le tunnel.

b. Vous devez effectuer un traceroute entre le PC RACK-E-PC1 et google.com. Le trafic ne doit pas passer dans le tunnel.

c. Vous devez effectuer un traceroute entre le PC RACK-E-PC2 et google.com. Le trafic ne doit pas passer dans le tunnel.