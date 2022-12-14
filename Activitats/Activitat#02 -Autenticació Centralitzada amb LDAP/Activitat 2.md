# Activitat 2

## Part pràctica

### Instal·lació d’un servei web apache.(0,5 punts)

- Instal·lem el dimoni httpd:

 ```` dnf install httpd -y ````

- Activem el dimoni per iniciar cada cop que el sistema arranqui:

 ```` systemctl enable httpd ````

- Arranquem i comprovem l’estat del dimoni:

 ```` systemctl start httpd ````

 ```` systemctl status httpd ````

### Instal·lació de la versió 7.4 de php. (0,5 punts)

 ```` dnf module list php ````

- PHP 7.2 és el per defecte

- Per modificar-ho

 ```` dnf module reset php ````
 ```` dnf module install php:7.4 -y ````

- Per instal·lar extensions de PHP

 ```` dnf install php-curl php-zip -y ````

- Comprovem la versió instal·lada

 ```` php -v ````

### Instal·lació i configuració del paquet. (2 punts)

- Abans d'instal·lar paquets: 
 ![image](https://user-images.githubusercontent.com/79162978/195657063-f911baaf-1742-4033-afe8-215b2b59b3fb.png)

- Fem instal·lació dels paquets: 
 ```` dnf install php-gd php-ldap php-gmp -y ````

- Després d'instal·lar:

  ![image](https://user-images.githubusercontent.com/79162978/196219768-82ac20ab-4169-4798-b91f-b379e4fdfc98.png)
 
 - Ldap el tenim a la màquina 192.168.101.77 que és el que allotja la bbdd
 - Lam el tenim a la màquina 192.168.101.61 que és el que té el servei lam.
 - Client el tenim a la màquina 192.168.101.72. 

 Per apuntar a la bbdd hem hagut de modificar en la configuració la següent adreça: 
 ![image](https://user-images.githubusercontent.com/79162978/196994504-f582c746-eb60-4b56-92bc-4c7b7c4f8006.png)

 https://www.ldap-account-manager.org/lamcms/

- Introduïr contrassenya: lam
  cd /var/lib/

 ![image](https://user-images.githubusercontent.com/79162978/196223430-991760a2-bafc-48c2-bb02-fa9b46ef8a42.png)
 
 ![image](https://user-images.githubusercontent.com/79162978/196227764-30bb129b-8ccf-4985-9edf-6dc734677e95.png)

- Configurar el paquet:

 ![Captura](https://user-images.githubusercontent.com/83337658/196234664-f4a499de-5e64-47ac-afb0-0d39e60af929.PNG)
 ![Captura2](https://user-images.githubusercontent.com/83337658/196234693-c6d5283b-835a-4256-acf3-a9e617155a52.PNG)

- Canviar la contrasenya per cmd: ```` ldappasswd -H ldapi:/// -Y EXTERNAL -S \ "cn=osproxy,ou=system,dc=curs,dc=asv,dc=udl,dc=cat" ````

### Protegiu el servei LAM, eliminant els comptes per defecte. (1 punt)

- Canviem la contrasenya del server ldap 192.168.101.77 que conté la bbdd: 
- La nova pass serà: asv01

 ![image](https://user-images.githubusercontent.com/79162978/196996583-21fde96a-a62f-43fc-9a66-e2f7907234af.png)
 
 - Si intentem accedir amb 1234 ens sortirà aquest error: 
 
  ![image](https://user-images.githubusercontent.com/79162978/196997670-30262425-7f19-45d4-b920-d80e94872cfe.png)
  
 -Modifiquem el password de les següents seccions de lam a asv01:
 
  ![image](https://user-images.githubusercontent.com/79162978/196998357-d7b7e284-c83c-4456-b4af-0e84ba9796f2.png)
  ![image](https://user-images.githubusercontent.com/79162978/196998268-7d337dd0-487e-49dd-a4ef-7a539b9ef589.png)
  ![image](https://user-images.githubusercontent.com/79162978/196998661-71e86637-26a6-4ddd-927d-d562bc2f577f.png)
  
  - Si intentem accedir amb la pass de lam, sortiran els següents errors: 
   
    ![image](https://user-images.githubusercontent.com/79162978/196999020-86ea022e-f9bb-414a-a37c-9847602242e9.png)
    ![image](https://user-images.githubusercontent.com/79162978/196999319-8bc06fd0-9c13-4d56-b2a6-db8c487e3845.png)



### L’únic usuari que pot iniciar sessió al servei ha de ser l’osproxy. (1 punt)

<img width="1436" alt="Captura de Pantalla 2022-10-20 a las 11 52 52" src="https://user-images.githubusercontent.com/38278207/196917239-48e0cf5b-566b-45db-ad8e-6a6dfccbbb28.png">

Per configurar això, entenem que hem de modificar parametres del següent apartat

<img width="1436" alt="Captura de Pantalla 2022-10-20 a las 11 55 49" src="https://user-images.githubusercontent.com/38278207/196918011-10039f3f-e75f-42d0-a3b7-b2483d36b514.png">



### Afegiu a l’usuari el mòdul SSH publickey. (1 punt)

- Afegir el servei SSH public key (ldapPublicKey) amb un sol click: 

 ![image](https://user-images.githubusercontent.com/79162978/197000832-a1a25d7c-d0af-4114-b077-341b512715b1.png)


## Part teòrica

### Que es kerberos?

![image](https://user-images.githubusercontent.com/38278207/196037245-84458df1-3d7c-43d4-b43b-4c1e2d199c2d.png)


**Kerberos**, donat una xarxa de comunicacions insegura, es un protocol d'autenticació que permet als ordinadors, mitjançant una identificació mutua, validar la seva identitat. Tant el client com el servidor, validen la identitat un de l'altre. Kerberos treballa amb sistema de xifrat simètric que requereix un 3r de confiança.  Uitlitza un **algoritme de xifrat molt fort**

Kerberos té una base de dades de claus secretes; cada entitat de la xarxa té una clau secreta, coneguda únicament per ella i Kerberos, amb què demostra la seva identitat. Per a una comunicació entre dues entitats, Kerberos genera una clau de sessió que poden utilitzar per xifrar les comunicacions.

### On s'utilitza?

S'empra especialment en sistemes segurs que depenen de funcions d'auditoria i d'autenticació. És un sistema alternatiu a altres com SSH, POP i SMTP. Es pot utilitzar per a autenticació Posix ia Active Directory (windows), NFS i Samba.

### Com funciona?

Utilitza sistema de clau simètrica, de manera que cal un 3r de confiança.

Un client actua amb nom d'usuari per accedir a uns determinats serveis d'un servidor. El servidor realitza aquesta autentificació que exigeix el client. Quan l'autentificació es realitza correctament, el servidor genera un **ticket**, aquest ticket es enviat al client, i quan el client el té, ja està assegurat, per la resta de servidors, que el client esta autenticat.

Una explicació més tècnica: 

<img width="1436" alt="Captura de Pantalla 2022-10-16 a las 15 12 21" src="https://user-images.githubusercontent.com/38278207/196037344-ec166b5c-b665-4df4-93ae-aa09c75cd5e6.png">


El servidor d'autentificació es separa en 3 parts:

- Base de dades
- Servidor d'autentificació
- Servidor de tickets

Totes elles englobades dins del **centre de distribució de claus**

![image](https://user-images.githubusercontent.com/38278207/196037193-6f041289-07ec-4569-9f2a-217c012137ce.png)


## Historia

Kerberos ja fa dècades que esta en funcionament i, tot i que es un sistema segur i fiable, kerberos ha rebut atacs amb el pas del temps. Els hackers han trobat metodes per falsificar els tickets, esbrinar contrassenyes o directament saltar-se el protocol.

Per norma general, per a que funcioni be aquest protocol de seguretat, caldria fer servir contrassenyes segures. Un exemple de sistema que genera claus fiables, son les contrassenyes que et genera un MAC. 

En el moment d'iniciar sessió, et dona la opció de generar una contrassenya segura, que es bastant llarga, amb combinacions de numeros, majuscules, simbols, i gens trivial.

<img width="1450" alt="Captura de Pantalla 2022-10-16 a las 14 51 32" src="https://user-images.githubusercontent.com/38278207/196036404-fed896fc-70f7-4191-88ed-aebc799a90c7.png">

``` vevmiV-hidgo5-cokdan ```

Mètodes per vulnerar Kerberos:

- Pass the ticket:  Amb aquest mètode, un atacant falsifica la clau de sessió i fa servir credencials falses. Els pirates informàtics falsificaran una butlleta daurada o platejada per obtenir accés al domini o accés a un servei.
- Atac de força bruta: Anar provant contrassenyes per esbrinar la usada 
- Degradació del xifrat: Es realitza una degradació de xifratge amb codi maliciós de clau mestra, un tipus de codi maliciós que passa per alt Kerberos si el ciberatacant té accés d'administrador.
- Dc shadow attack: Aquest atac té lloc quan els pirates informàtics obtenen l'accés necessari per configurar el propi controlador de domini (DC) que s'utilitzarà per a una infiltració més gran

Actualment Kerberos es la solucio back-end mes optima, i a priori no sembla que tinguem una solucio futura inminent millor que aquest protocol 😁

### En que ens beneficia utilitzar Kerberos?

- Control d'accés
- Autenticació mutual
- Duració concreta del ticket
- Autentificació reutilitzable
- Seguretat

### Kerberos vs LDAP

LDAP. Kerberos i LDAP s'uneixen comunament (fins i tot a Active Directory) per proporcionar un directori d'usuaris centralitzat (LDAP) i serveis d'autenticació (Kerberos).

LDAP conté els usuaris, grups, i demés metadata sobre aquests. El principal punt feble es que introdueixen la contrassenya a través de xarxa, de manera que una combinació molt òptima es juntar-los tots 2.

Kerberos proporciona la funcionalitat d'inici de sessió única. Quan un usuari s'ha autenticat al KDC, cap altre servei (com ara un lloc d'intranet o un recurs compartit de fitxers) no necessita la contrasenya de l'usuari. El KDC, aquest tercer de confiança, és responsable d'emetre tickets en què confia cada servei. 

La combinació de LDAP i Kerberos proporciona autenticació i administració d'usuaris centralitzades, i en xarxes grans es fonamental tenir aquest valor de seguretat que ens dona Kerberos.

### Fonts consultades

- https://es.wikipedia.org/wiki/Kerberos
- https://www.redeszone.net/tutoriales/redes-cable/kerberos-protocolo-seguridad-redes/
- https://ciberseguridad.com/guias/prevencion-proteccion/kerberos/ (molt recomanable)
 
