
# Laboratoire 1 - Configuration des ACL étendues et standards, OSPF, SSH

# Topologie

![Topo](../../topo/rack-a/topo1-4.png)

# Table d’adressage :


|Equipments|Interface     | IP Address     | Subnet Mask     | Default Gateway | description
|----------|--------------|---------------|----------------|------------------|------------------|
|RACK-A-R1 |G0/0/1   |192.168.70.2       |255.255.255.248           | N/A|Connexion a internet via la switch
|          |G0/0/0   |10.0.0.1   |255.255.255.252| N/A|Connexion au routeur R2
|RACK-A-R2 |G0/0/1   |10.0.0.2   |255.255.255.252| N/A|Connexion au routeur R1
|          |G0/0/0.10|172.16.10.1|255.255.255.0  | N/A|Connexion au switch SW1 - VLAN 10
|          |G0/0/0.20|172.16.20.1|255.255.255.0  | N/A|Connexion au switch SW1 - VLAN 20
|RACK-A-PC1|Fa0      |DHCP       |DHCP  | DHCP   |    |
|RACK-A-PC2|Fa0      |DHCP       |DHCP  | DHCP   |    |


