# TP1-BootCamp

## Sommaire:
[I. Présentation du sujet](#Présentation-du-sujet)  
        [I.a. Matériel](#Matériel)  
        [I.b. Conditions](#Conditions)  
[II. Mise en place des Vlans et IPs](#Mise-en-place-des-Vlans-et-IPs)  
[III. Configuration des switchs](#Configuration-des-switchs)   
    [III.a. Switchs d'accès](#Switchs-d'accès)  
    [III.b. Switch de distribution](#Switch-de-distribution)  
[IV. Configuration du routeur](#Configuration-du-routeur)  
[V. Configuration des serveurs](#Configuration-des-serveurs) 
    [V.a. Serveur WEB](#Serveur-WEB)  
    [V.b. Serveur DHCP](#Serveur-DHCP)
[VI. Conclusion](#Conclusion)

## Présentation du sujet  
### Matériel  
### Conditions  

## Mise en place des Vlans et IPs  
![topo](topo.png)
Pour mettre en place le vlan des RH avec une place de 29 posts:
```bash
Router(config)#interface gigabitEthernet 0/2
Router(config-if)#no shut
Router(config-if)#exit
Router(config)#interface gigabitEthernet 0/2.2
Router(config-subif)#encapsulation dot1Q 2
Router(config-subif)#ip address 192.168.2.30 255.255.255.224
```

## Configuration des switchs  
### Switchs d'accès  
```bash
interface FastEthernet0/2
 switchport mode access
!
interface FastEthernet0/3
 switchport access vlan 2
 switchport mode access
!
interface FastEthernet0/4
 switchport access vlan 3
 switchport mode access
!
interface FastEthernet0/5
 switchport access vlan 4
 switchport mode access
!
```
### Switch de distribution  
```bash
interface FastEthernet0/2
 switchport trunk allowed vlan 1-4
 switchport mode trunk
!
interface FastEthernet0/3
 switchport trunk allowed vlan 1-4
 switchport mode trunk
!
interface FastEthernet0/4
 switchport trunk allowed vlan 1-4
 switchport mode trunk
!
interface FastEthernet0/5
 switchport trunk allowed vlan 1-4
 switchport mode trunk
!
```
## Configuration du routeur  
```bash
Router(config)#interface gigabitEthernet 0/1
Router(config-if)#no shutdown 
Router(config-if)#exit
Router(config)#interface gigabitEthernet 0/1.3
Router(config-subif)#no shutdown 
Router(config-subif)#encapsulation dot1Q 3
Router(config-subif)#ip address dhcp
```
Pour n'autoriser que 15 ip à passer par ici:
```bash
Router(config)#interface gigabitEthernet 0/2.4
Router(config-subif)#no shut
Router(config-subif)#encapsulation dot1Q 4
Router(config-subif)#ip address 10.1.1.14 255.255.255.240
```
## Configuration des serveurs  
### Serveur WEB  
![serveurweb](serveurweb.png)
### Serveur DHCP  
![serveurdhcp](serveurdhcp.png)

## Conclusion  