### Treball de recerca‐Laboratori Core network

### Tardor  2018 ‐ 2019 

```
Assignatura: Tecnologies de Xarxes de Computadors (TXC)
```
L’objectiu d’aquest laboratori és proporcionar a l’estudiant la possibilitat de fer una
pràctica que tingui en compte les tecnologies de xarxes corresponent al Core Network.
Les tecnologies disponibles en aquest àmbit són Frame Relay, ATM i Ethernet tenint la
possibilitat de col∙locar sobre d'elles a MPLS. Algunes d'aquestes tecnologies han anat
substituint a altres ja sigui per l'eficiència, velocitats de transmissió o l'aplicació de la
qualitat de servei. La solució adoptada en les xarxes reals actualment es basa en MPLS
sobre Ethernet i en alguns casos encara sobre FR i ATM. Hem de tenir en compte que
MPLS proporciona qualitat de servei amb possibilitat d'enginyeria de trànsit que
permet optimitzar l'ús dels recursos en funció de la demanda de servei requerida.

Condicions generals:
a) En aquest laboratori s'haurà de dissenyar una xarxa d'àrea extensa programant els
dispositius de què consta utilitzant el IOS de Cisco amb el **simulador de xarxes
GNS3**. Inclou tecnologies Ethernet, Frame Relay, ATM i MPLS.
b) El disseny de la solució es farà en grups de treball prèviament configurats
c) S'ha d'escriure una memòria seguint la plantilla proporcionada amb una descripció
del treball realitzat incloent els dibuixos (indicant totes les dades necessàries de
@IP, ports i interfases) i strings de programació realitzats (exclusivament el
programat per vosaltres) amb els comentaris personals que es creguin oportuns.
Es lliurarà en format PDF, “ **memoria_TR‐Lab_grup_XX.pdf** ”, per Atenea abans del
segon control en la data prefixada. El lliurament de la memòria en el termini fixat
és la **condició per poder accedir al test‐examen**. No és imprescindible el fet de
que el treball funcioni correctament, no obstant el professor determinarà quins
grups no poden accedir al test‐examen per no tenir la memòria un mínim de
qualitat o per no estar el treball suficientment desenvolupat.
d) La nota corresponent a aquest TR‐Lab (10% nota final) es donarà en base al test‐
examen individual sobre el laboratori que es realitzarà el dia del segon control. El
contingut de la memòria i l’èxit del funcionament del laboratori es valorarà per
part del professor per obtenir fins a **0,5 punts addicionals** que es sumarà a la
mitjana de controls.


## Laboratori a realitzar

La xarxa que s'haurà de configurar en GNS3 en aquest laboratori és la següent (tots els valors
de @IPv4 s’hauran de canviar, encara que les identificacions dels ports i interfases es poden
mantenir si es vol)

**Aspectes generals:**
 Aquesta documentació indica exemples similars a les configuracions necessàries però no
és definitiva. Caldrà investigar a Internet els dubtes que sorgeixin (aquesta és la part de
recerca).
 L'objectiu del laboratori és programar tots els elements en IOS de Cisco i els switch FR i
ATM de forma que es pugui fer un ping entre TA i TB i viceversa. A més s'ha de poder
visualitzar el trajecte del ping amb Traceroute.
 R1 està connectat amb R4 amb un circuit virtual Frame Relay, R7 està connectat amb R
amb un circuit virtual ATM, i R5 està connectat amb R7 amb una interfase sèrie i HDLC. La
resta són connexions FastEthernet.
 A GNS3 en els routers les connexions amb el switch FR són PA‐4T +, les connexions amb el
switch ATM són PA‐A1, la connexió entre R5 i R7 és sèrie PA‐4T +, i les restants són
FastEthernet del tipus PA‐2FE‐TX per exemple. Per defecte a GNS3 els routers tenen una
connexió FastEthernet.

 La xarxa troncal MPLS Core Network està formada per R4, R5, R6 i R7.
 El protocol d'enrutament necessàriament serà OSPF i s’aplica a tots els routers. Si un grup
de treball tingués dificultats per programar OSPF debut a la manca de coneixements previs
caldrà consultar amb el professor.
 S’aplicarà enginyeria de trànsit a la xarxa MPLS (MPLS‐TE) per crear un túnel unidireccional
de R4 a R7 passant per R5 a  50  Kbps. Això farà que la ruta no sigui igual en els dos sentits.
 Afegir els Port/DLCI que es cregui convenient en el switch FR (Ex. Input  1 ‐101, output  10 ‐
202). Recordeu que el primer número és el Port i el segon el DLCI. En GNS3 els Virtual
Circuits són bidireccionals tant en FR com en ATM.
 Afegir els Port/VP/VC que es creguin convenients en el switch ATM (P.ex. 1/10/
10/10/200).
 Els valors de les adreces de xarxa IPv4 s’han de triar de forma arbitrària. Es mostra un
exemple en el dibuix però cada grup ha d’agafar adreces pròpies. No es poden utilitzar les
indicades al dibuix.
 S'utilitzarà la imatge del router **c7200 de Cisco**
 S’ha de configurar en GNS3 els terminals TA i TB **com un router** canviant el nom i la figura
(botó dret). Llavors es programen com un router. Així no caldrà fer servir Linux.


 Amb “show run” es pot saber el que està programat a cada router i així es pot revisar i
imprimir per fer la memòria.
 Amb “show interfaces” es veuen totes les interfaces d’un router.
 Amb “show ip route” es veuen les taules d’encaminament dels routers.
 **Important: A GNS3 recordar de concloure cada vegada que es modifica un router amb
"wr" per gravar les dades abans de sortir, sinó es perden les modificacions. Si es vol
rectificar alguna cosa es posa “no” al davant.**

# Passos a seguir per fer el laboratori

1. Configuració @IPv4 a TA i TB i rutes per defecte.
2. Configuració switch FR i ATM. Indicar els circuits virtuals entrada/sortida i ports.
3. Configuració @IPv4 als routers. També es configura loopback a cada router.
4. Comprovació dels pings locals. Visualització de les taules d’enrutament.
5. Configuració OSPF a tots els routers. Les interfases de R1 i R2 amb TA i TB
    respectivament amb “passive‐interface”. També s’anuncia per OSPF el loopback.
6. Comprovació dels pings a poc a poc des de TA fins TB. Comprovació de les taules
    d’enrutament de tots els routers.
7. Comprovació del Traceroute de TA a TB i viceversa veient que la ruta triada és R4‐R6‐
    R7 en el Core Network en els dos sentits.
8. Configuració del MPLS als routers R4, R5,R6 i R7 en les interfases internes del Core
    Network.
9. Configuració de MPLS‐TE a R4,R5 i R7.
10. Preparació del túnel explícit a  50  Kbps a R4, R5 i R
11. Comprovació de les taules d’enrutament dels routers del core network. Comprovar la
    aparició del túnel.
12. Ping TA‐TB i TB‐TA.
13. Traceroute entre TA i TB. Comprovar que fa la ruta R1, R4, R5, R7 i R2.
14. Traceroute entre TB i TA. Comprovar que fa la ruta R2, R7, R6, R4, R1.


## Ajuts per al desenvolupament del laboratori.

## 1. Download GNS

Es poden obtenir diversos tutorials a internet per veure com es descarrega GNS3 i es posa a
funcionar. Caldrà descarregar també la image del router Cisco c7200 e incorporar‐la al
programa.

Podeu trobar a Internet la descàrrega de GNS3 https://www.gns3.com/ i el manual
d’utilització i programació de GNS3 a

[http://demay.iut.lr.free.fr/doc/GNS3/GNS3%20Network%20Simulation%20Guide.pdf](http://demay.iut.lr.free.fr/doc/GNS3/GNS3%20Network%20Simulation%20Guide.pdf)

## 2. Exemple de programació d’Ethernet I OSPF

La xarxa que es proposa d’exemple és:

```
La programació de T1 (en realitat és un router) serà:
```
T1# configure terminal
T1(config)#interface f0/
T1(config-if)#ip address 140.68.100.1 255.255.255.
R1(config-if)#ip route 0.0.0.0 0.0.0.0 140.68.100.
R1(config-if)#no shutdown
R1(config-if)#exit

```
La programació de R1 serà:
```
R1# configure terminal
R1(config)#interface f0/
R1(config-if)#ip address 140.68.100.2 255.255.255.
R1(config-if)#no shutdown
R1(config)#interface f1/
R1(config-if)#ip address 10.1.0.1 255.255.255.
R1(config-if)#no shutdown
R1(config-if)#exit
R1(config)#router ospf 1
R1(config-router)#network 140.68.100.0 0.0.0.255 area 0
R1(config-router)#network 10.1.0.0 0.0.0.255 area 0
R1(config-router)#exit
R1(config)#exit


## 3.Exemple de programació de Frame Relay

La xarxa que es proposa d’exemple és:

Per configurar una xarxa amb routers i switch FR, el primer pas serà configurar els routers. En
cada un fer clic dret‐> configure‐> slots i al desplegable de l'Slot  1  afegir el següent adaptador
PA‐4T +. Aquest adaptador ens afegirà  4  entrades de tipus serial al router, necessàries per a
una connexió FR.

Un cop configurat ençà, s'ha de configurar el switch FR, per a això clic dret‐> configure i
després s'ha d'afegir el port d'entrada i un de sortida amb el respectiu DLCI, això és important,
ja que és el camí que seguirà el paquet a la xarxa FR. Es pot seleccionar qualsevol valor del rang
de  0  a 1023, per exemple s'ha seleccionat el següent:
‐ Port origen / DLCI: 1:  100 
‐ Port destí / DLCI: 10:  200 
Cal afegir aquest camí en el switch i acceptar els canvis.
Ara s'ha de configurar els routers amb IOS per Frame Relay. **Caldrà crear subinterface point‐
to‐point** y a la configuració habitual cal afegir en les interfícies corresponents la connexió amb
el switch Frame Relay indicant el DLCI corresponent:

R1# configure terminal
R1(config)#interface f0/
R1(config-if)#ip address 140.68.100.2 255.255.255.
R1(config-if)#no shutdown
R1(config)#interface s1/
R1(config-if)#encapsulation frame-relay
R1(config-if)#exit
R1(config)#interface s1/0.1 point-to-point
R1(config-if-sub)#ip address 10.1.0.1 255.255.255.
R1(config-if-sub)#frame-relay interface-dlci 100
R1(config-fr-sub-dlci)#exit
R1(config-if)#no shutdown
R1(config-if)#exit

Verificació :
show frame-relay map  Mostra la taula de mapeig FR.


## 4.Exemple de programació d’ATM

La xarxa que es proposa d’exemple és:

El primer pas serà configurar cada un dels routers per al funcionament d'ATM. En aquest cas
s'ha d'habilitar la interfície que disposa el router c7200 per a aquest tipus de commutació. En
concret es tracta de l'slot PA‐A
Un cop habilitada la interfície s'ha de configurar el switch ATM amb els VPI i VCI. Es triaran els
que surtin per defecte o es poden modificar (botó dret sobre el dibuix del switch). Aquí triem
Port/VP/VC 1/10/100 10/10/
Ara s'ha de configurar cada router de la xarxa amb el protocol ATM per commutar paquets:
**Aquí també s’ha de programar un subinterface per a que funcioni el OSPF**
Per exemple un router amb un sol circuit virtual ATM:

R1# configure terminal
R1(config)#interface f0/
R1(config-if)#ip address 140.68.100.2 255.255.255.
R1(config-if)#no shutdown
R1(config-if)#exit
R1(config)#interface a1/
R1(config-if)#no shutdown
R1(config-if)#exit
R1(config)#interface a1/0.1 point-to-point
R1(config-if-sub)#ip address 10.1.0.1 255.255.255.
R1(config-if-sub)#pvc 10/
R1(config-if-sub-atm-vc)#protocol ip 10.1.0.2 broadcast
R1(config-if-sub-atm-vc)#encapsulation aal5snap
R1(config-if-sub-atm-vc)#exit
R1(config-if)#no shutdown
R1(config-if)#exit

Verificació:
Show atm map -> Mostra els VC configurats actualment
show ip route -> Mostra la taula de routing.


## 5. Exemple de programació d’MPLS

**A) Activació MPLS**

La xarxa que és proposa d’exemple és:

On el domini MPLS és entre R1 i R2.

Primer s'ha de configurar cada router de la xarxa MPLS amb el protocol LDP, per a la
commutació d'etiquetes MPLS:

R1(config)#ip cef
R1(config)#mpls label protocol ldp
R1(config)#interface f1/
R1(config-if)#mpls ip
R1(config)#exit

Verificació:
show ip cef -> Permet veure la taula de forwarding
show mpls interfaces -> Permet veure quines interfaces usen MPLS i el seu estat
show mpls ldp Discovery -> Permet obtener información de LDP local i dels veíns.
show mpls ldp neighbor -> permet veure les adjacencies LDP i coneixer el seu estat

**B) Activació MPLS‐TE**

En els apunts de classe es pot veure la programació de MPLS‐TE en una configuració en la que
hi ha diferents túnels. En general els passos a seguir són:

1. Activació de les extensions MPLS‐TE en les interfícies afectades de tots els routers per on
passarà el túnel.

R1(config)# mpls traffic-eng tunnels

Comandaments per activar TE a les interfases

R1(config)# interface f1/
R1(config-if)# mpls traffic-eng tunnels

2. Comandaments per activar las extensions TE en OSPF en tots els routers del túnel

R1(config)# router ospf 1
R1(config-router)# mpls traffic-eng area 0
R1(config-router)# mpls traffic-eng router-id loopback0 -> farà servir el loopback

3. Comandament per activar RSVP‐TE fixant el màxim ampla de banda reservable per als túnels
en totes les interfases dels routers del camí del túnel

R1(config)# interface f1/
R1(config-if)# ip rsvp bandwidth 100 -> assigna 100 kpbs de capacitat total a la
interfase f1/


4. Creació del túnel

Exemple per configurar un túnel de  100  Kbps. Això només es fa al router inici del túnel.

R1(config)# interface tunnel10 -> es crea el túnel anomenat tunnel
R1(config-if)# ip unnumbered loopback0 -> s’assigna la interfase de loopback0 como ip
del túnel
R1(config-if)# tunnel mode mpls traffic-eng -> habilita el mode MPLS-TE en el túnel
R1(config-if)# tunnel destination 10.0.1.103 -> es crea el túnel fins la loopback final
del túnel
R1(config-if)# tunnel mpls traffic-eng bandwidth 100 -> bitrate del túnel en kbps
R1(config-if)# tunnel mpls traffic-eng autoroute announce -> s’anuncia el túnel per OSPF

Atenció! Els túnels són unidireccionals.

Els túnels es poden crear de manera dinámica o explicita. En el cas dinámic, el camí es
determina per OSPF‐TE i no és el cas del present laboratori. En el cas explícit, es fixa el camí.

R1(config-if)# tunnel mpls traffic-eng path-option 1 explicit name LP1 -> túnel explícit
anomenat LP1 i el path-option indica l’ordre en que s’agafaria l’opció suposant que hi
hagués més opcions

Caldrà definir el camí explícit (aquest és un exemple teòric).
R1(config-if)# ip explicit-path name LP
R1(cfg-ip-expl-path)# next-address 10.0.1.2 -> @IP de la primera interfase del camí
explícit
R1(cfg-ip-expl-path)# next-address 10.0.2.2 -> @IP de la segona i última interfase del
camí explicit
R1(cfg-ip-expl-path)# next-address 10.0.1.103 -> loopback final inclosa en el camí
explicit

Verificació:
show mpls traffic-eng tunnels destination @IP ->Visualitza detalls dels túnels fins @IP
show mpls traffic-eng tunnels brief -> Visualitza els túnels creats


