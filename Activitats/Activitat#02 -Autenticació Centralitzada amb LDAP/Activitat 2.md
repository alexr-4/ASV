# Activitat 2

## Part pràctica

TODO: buscar plugin php para ldap


![image](https://user-images.githubusercontent.com/79162978/195657063-f911baaf-1742-4033-afe8-215b2b59b3fb.png)

## Part teòrica

### Que es kerberos?

**Kerberos**, donat una xarxa de comunicacions insegura, es un protocol d'autenticació que permet als ordinadors, mitjançant una identificació mutua, validar la seva identitat. Tant el client com el servidor, validen la identitat un de l'altre. Kerberos treballa amb sistema de xifrat simètric que requereix un 3r de confiança.  Uitlitza un **algoritme de xifrat molt fort**

Kerberos té una base de dades de claus secretes; cada entitat de la xarxa té una clau secreta, coneguda únicament per ella i Kerberos, amb què demostra la seva identitat. Per a una comunicació entre dues entitats, Kerberos genera una clau de sessió que poden utilitzar per xifrar les comunicacions.

### On s'utilitza?

S'empra especialment en sistemes segurs que depenen de funcions d'auditoria i d'autenticació. És un sistema alternatiu a altres com SSH, POP i SMTP. Es pot utilitzar per a autenticació Posix ia Active Directory (windows), NFS i Samba.

### Com funciona?

Un client actua amb nom d'usuari per accedir a uns determinats serveis d'un servidor. El servidor realitza aquesta autentificació que exigeix el client. Quan l'autentificació es realitza correctament, el servidor genera un **ticket**, aquest ticket es enviat al client, i quan el client el té, ja està assegurat, per la resta de servidors, que el client esta autenticat.

El servidor d'autentificació es separa en 3 parts:

- Base de dades
- Servidor d'autentificació
- Servidor de tickets

Totes elles englobades dins del **centre de distribució de claus**

## Historia

Tot i que es un sistema segur i fiable, kerberos ha rebut atacs amb el pas del temps. Els hackers han trobat metodes per falsificar els tickets, esbrinar contrassenyes o directament saltar-se el protocol.

Per norma general, per a que funcioni be aquest protocol de seguretat, caldria fer servir contrassenyes segures. Un exemple de sistema que genera claus fiables, son les contrassenyes que et genera un MAC. 

En el moment d'iniciar sessió, et dona la opció de generar una contrassenya segura, que es bastant llarga, amb combinacions de numeros, majuscules, simbols, i gens trivial.

<img width="1450" alt="Captura de Pantalla 2022-10-16 a las 14 51 32" src="https://user-images.githubusercontent.com/38278207/196036404-fed896fc-70f7-4191-88ed-aebc799a90c7.png">

``` vevmiV-hidgo5-cokdan ```


### Fonts consultades

- https://es.wikipedia.org/wiki/Kerberos
- https://www.redeszone.net/tutoriales/redes-cable/kerberos-protocolo-seguridad-redes/

