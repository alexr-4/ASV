# Administrant la UDL
### Paula, Samantha, Alex

## Servidor LDAP

Des de la Universitat de Lleida ens han contractat perquè creem un sistema d'administració que sigui segur i amb el que puguin treballar tant professors com alumnes. Per començar a dissenyar aquest sistema, iniciarem amb la creació d'un Servidor LDAP (Protocol lleuger d'accés a directoris). Aquest tipus de servidor ens permetrà establir un protocol de tipus client-servidor per poder accedir a un servei de directori, és a dir, a un espai que tindrà base de dades i una estructura d'informació segura i estable. 

El nostre servidor LDAP es trobarà a la màquina amb IP: 192.168.101.77

### La base de dades LDAP ha d’estar en una partició diferent del Sistema Operatiu:

Primerament configurarem un disc dur nou que contindrà la partició de la BBDD: 

- Farem la comanda ```` lsblk ```` per veure els discs que té la màquina i seguidament farem la comanda mkfs.xfs /dev/vdb per executar el disc: 

	![image](https://user-images.githubusercontent.com/79162978/203837076-a7040b97-418b-46dd-acd6-3bb9edd3bea0.png)
	
- Per veure on és la bbdd:  ```` less /var/lib/openldap/ ```` 

- A continuació, crearem una carpeta a ```` mkdir /tmp/ldap ```` per fer una copia del que conté les dades de la carpeta openldap ```` cp -r /var/lib/openldap/ /tmp/ldap ````. La copia és necessaria per no perdre les dades a l'hora de muntar el disc dur al directori que conté les dades.

- Muntarem el directori amb la comanda ```` mount /dev/vdb /var/lib/openldap/ ````

   ![image](https://user-images.githubusercontent.com/79162978/203839728-bec71e9d-1d84-47f0-9262-820d1d7bb3f4.png)

- Revisarem que estiguin dintre les dades, veiem que les hem perdudes, per tant, copiarem tot lo que tenim a la carpeta temporal cap a la carpeta que ens interesa: 
    ````  cp -r /tmp/ldap/ /var/lib/openldap/   ````
 
    ![image](https://user-images.githubusercontent.com/79162978/203840006-3668d09f-d697-4d18-a06b-2a2088c099cb.png)

### Únicament el root podrà accedir per SSH emprant PUBKEY: 

   ![image](https://user-images.githubusercontent.com/79162978/203841545-6b08c028-9aed-4d20-9f99-b4c0334cf2cc.png)

### Cada alumne de la classe d’ASV ha de tenir el seu compte amb permisos de sudo: 

Per tal de poder afegir cada alumne i establir els permisos sudo, farem servir el servei LAM per mantenir i gestionar els comptes. En el següent punt, explicarem com incloure aquest servei dintre del servidor LDAP i com configurar-ho. 

   ![image](https://user-images.githubusercontent.com/79162978/205706006-6a529db1-3975-44b8-96c5-72bc46a54057.png)
   
   ![image](https://user-images.githubusercontent.com/79162978/206912411-e12106e6-b7f0-4721-a621-6d83d86c56a2.png)


### S’inclourà un servei LAM per mantenir i gestionar els comptes:

- Instal·lem el lam de la URL https://www.ldap-account-manager.org/lamcms/releases i amb la comanda stfp passem a la maquina el fitxer descarregat: 

   ![image](https://user-images.githubusercontent.com/79162978/204330370-0e4b7dcb-443a-4a57-a5ae-6e78cbfde90c.png)

- Dintre de la maquina, fem la comanda ```` rpm -i nom de l'arxiu copiat ```` 

- Instal·lem el dimoni httpd:

 	```` dnf install httpd -y ````

- Activem el dimoni per iniciar cada cop que el sistema arranqui:

 	```` systemctl enable httpd ````

- Arranquem i comprovem l’estat del dimoni:

	 ```` systemctl start httpd ````
	
	 ```` systemctl status httpd ````

	![image](https://user-images.githubusercontent.com/79162978/204309150-c4fc15ab-bad8-4f26-b844-bb740cbbe48b.png)


- Instal·lació de la versió 7.4 de php.

 	```` dnf module list php ````

- PHP 7.2 és el per defecte. Per modificar-ho:

 	```` dnf module reset php ````
	
 	```` dnf module install php:7.4 -y ````

- Per instal·lar extensions de PHP

	 ```` dnf install php-curl php-zip -y ````

- Comprovem la versió instal·lada

	 ```` php -v ````
	 
	 ![image](https://user-images.githubusercontent.com/79162978/204309820-119705e8-38a4-46c2-84c3-e6baa22d54c1.png)
	 
- Per arrancar el servei LAM, hem de tenir el firewall configurat: 

	![image](https://user-images.githubusercontent.com/79162978/204336001-3bb401ef-d3dd-47b1-b680-3b39bfd21bd0.png)
	
	
	![image](https://user-images.githubusercontent.com/79162978/204336094-63373e21-05bf-477e-a3c6-a3f70e0c05b1.png)
	

	![image](https://user-images.githubusercontent.com/79162978/204336214-2abdc1d9-cf45-4e18-864e-288aeecf0c31.png)
	
- Afegirem al firewall tant la connexió http com la https: 

	![image](https://user-images.githubusercontent.com/79162978/204335832-f6f2409d-8bba-4d2d-97e2-19ee9a73561f.png)


## Servidor NFS

Per poder interconectar els equips dintre de la xarxa local de la UDL, necesitarem tenir un Servidor amb el protocol NFS (Network File System) que serà el nostre Sistema d'arxius de xarxa. Aquest protcol permetrà que els diferents equips puguin conectar-se a través d'autentificació segura entre ells i poder accedir als arxius que es trobin en un altre sistema. 

Protegirem la informació dels discos durs agrupant-los en una RAID 5. 
En una matriu RAID 5 amb tres o més unitats, les dades i la paritat es distribueixen per totes les unitats. Les dades es processen en dues unitats i la informació de paritat s'emmagatzema en la tercera. En cas de pèrdua d'una de les unitats de dades, la informació de paritat garanteix la nova creació de les dades perdudes. 

### Els directoris home dels usuaris estaran en una RAID5 o en una RAID10.

- Configurem els tres discos de la màquina: (```` mkfs.xfs /dev/vdb ````, ```` mkfs.xfs /dev/vdc ````, ```` mkfs.xfs /dev/vdd ````)

	![image](https://user-images.githubusercontent.com/83337658/203839115-2c98f88e-7b4c-4299-92c2-3356d8226c2c.png)
- inslatar el mdadm: ```` yum install -y mdadm ````
- fer: ```` mdadm --create --verbose /dev/md5 --level=5 --raid-devices=3 /dev/vdb /dev/vdc /dev/vdd ````
	
	![image](https://user-images.githubusercontent.com/83337658/203839753-4f2fe590-b75f-494d-bdf3-1309c4f46e97.png)

- muntem la raid 5 al punt de muntatge /mnt/home: ```` mount /mnt/home/ /dev/md5 ````, ```` mkfs.xfs /dev/md5 ````, ```` mount /dev/md5 /mnt/home/ ````

	![image](https://user-images.githubusercontent.com/83337658/203841870-6b43e0bc-e5eb-4523-a878-b7da0ea42765.png)

- amb ```` blkid ```` busquem la raid i la enganchem a ```` vi /etc/fstab ````:
	
	![image](https://user-images.githubusercontent.com/83337658/203841964-bc5d3915-baee-4fdf-b37e-660576766c2c.png)
	![image](https://user-images.githubusercontent.com/83337658/203842635-7edec2d4-ad10-42e8-a183-b91d6b2cf480.png)

	
### Únicament root pot accedir per SSH utilitzant doble factor de verificació (password + codi).

- Per veure el fitxer de configuració ```` vim /etc/ssh/sshd_config ````, haurem de canviar les següents linies: 

	![image](https://user-images.githubusercontent.com/83337658/205112244-57aed6a5-68be-4cc0-9a8d-6931e12e497e.png)

- Se li ha d'assignar al root una password amb ```` passwd ```` --> 1234
- Després fem un ```` systemctl restart sshd ```` per reiniciar el sistema. 
- I tornarem a autentificar per descarregar el paquet de google-authenticator: 

	![image](https://user-images.githubusercontent.com/83337658/205113200-8d442f73-2195-4b34-868f-63735ef2989a.png)

- Seguidament farem google-authenticator i a la primera pregunta li direm que si: 

	![image](https://user-images.githubusercontent.com/83337658/205114538-366182e8-3646-434f-b63b-c773d96c5582.png)
	![image](https://user-images.githubusercontent.com/83337658/205114876-661cfae0-a860-4ec0-8f04-298c46b264ef.png)

- Descargar Google Autenticator en el móvil, escanear QR e insertar codigos en la terminal:

	![image](https://user-images.githubusercontent.com/83337658/205115847-571320a4-23f6-4eb8-88c3-ba1b66500aca.png)
	
- Entrem al: nano /etc/ssh/sshd_config

	![image](https://user-images.githubusercontent.com/83337658/205116206-6d20883f-4ca6-4263-bfba-057f6c1c0780.png)
	
- Entrem al: nano /etc/pam.d/sshd

	![image](https://user-images.githubusercontent.com/83337658/205659406-5ae0d913-a542-4423-bd37-8844b11274e7.png)
	![image](https://user-images.githubusercontent.com/83337658/205120657-f8c7616b-94c5-4c24-bc89-cd7be6615e29.png)
	
- En otra cmd entrar a la maquina:

	![image](https://user-images.githubusercontent.com/83337658/205120859-1961691b-8456-482f-ab6c-952022648b23.png)
	

### Configurarem un servei de dades al núvol utilitzant owncloud.

Script:
homes=$(ldapsearch -b ou=users,dc=asv,dc=udl,dc=cat -D cn=osproxy,ou=system,dc=curs,dc=asv,dc=udl,dc=cat -W -x | grep uid: )

```` echo $homes
let n=0;
for home in $homes
	let p=n%2
	if [ $p -eq 1 ] ; then
		mkhomedir_helper ${home}
	fi
	let n=n+1 
````

## Client

### Els directoris /home es muntaran sota demanda, únicament quan l’usuari accedeixi al sistema.

Seguirem el següent esquema per tal de desenvolupar l'apartat; es a la maquina client on instal·larem el servei autofs:

<img width="1440" alt="Captura de Pantalla 2022-12-15 a las 9 17 50" src="https://user-images.githubusercontent.com/38278207/207808553-649aed57-3bdc-4ccf-a509-a7e562f4d3e0.png">

- Per instal·lar, provar amb les següents comandes:


```
apt-get install autofs
yum install autofs
dnf -y install autofs
```

- Iniciem el servei amb el següent comando:

```
sudo systemctl enable --now autofs
```

- El fitxer de configuració principal es al ```/etc/auto.master``` i es alli on haurem de afegir la següent línea:

```
/home/* -fstype=nfs 192.168.101.131:/mnt/homes/*
```

## Manteniment

### Grafana

L'aplicació web de Grafana és una eina de motorització que la farem servir com a administradors per estalviar costos i identificar problemes que podrien succeir en el futur. Per a nosaltres és molt important perquè en producció, la inactivitat és inacceptable, ja que interrompria el fluxe de treball pels usuaris i ens faria perdre ingressos i reputació.

Inclourem amb Grafana un grup d'usuaris de tipus professor per tal que puguin fer servir l'eina per fer seguiment de l'alumnat.

#### Grafana com Administradors

Grafana funciona amb servidor apache 2.0, fet que ens facilita la integració de l'eina amb els nostres servidors amb sistema apache. Amb aquesta eina podrem fer seguiment dels logs i així anticipar i corregir errors de forma més eficaç, ja que ens permetrà veure la informació a través de gràfiques i escollir quins punts ens interessa controlar.

Desplegarem l'eina a través del servidor Nginx, servei que ens permetrà allotjar Grafana en HTTP a través de proxy invers i fer seguiment del caché, balancejant la carrega de dades. 

Per fer una bona gestió dels logs, farem servir el servei Loki, que és el servei principal que s'encarrega d'emmagatzemar els logs i executar les querys sobre ells. A part, està dividit en multiples components que podrem configurar de forma independent. 
Loki no indexa el contingut del registre, sino que indexa les marques de temps i un cojunt d'etiquetes per un fluxe de registre. Fa que el index sigui més petit, lo que simplifica les operiacons i redueix el cost. 

La finalitat serà crear diferents "Dashboards" (panells gràfics amb mètriques) per tal d'organitzar els logs i crear alertes per preveure errors.

Exemple: 

Visualitzariem en un panell els logs amb les alertes configurades i vinculariem les dades en un panell gràfic, podent veure en una simple ullada la informació que més ens interessa. 

   ![image](https://user-images.githubusercontent.com/79162978/211264024-8fbb565c-8019-4250-9876-92eb64f25778.png)

L'eina de Grafana no només ens podrà servir amb els logs, sinó també per controlar la seguretat del sistema, la seguretat de la xarxa, la capacitat i estat dels discos durs, l'estat del servei nginx i del servidor apache:

   ![image](https://user-images.githubusercontent.com/79162978/211281123-1c830613-ea7c-4fda-ac97-df30c5a91cb2.png)


A part, podrem tenir control de l'accés i l'ús que es fa dintre dels servidors, a través de la vinculació de la BBDD amb Grafana, podent crear dashboards pel control dels usuaris.

#### Grafana com a professors

Crearem usuaris amb permisos especials i els permetrem veure i accedir a la informació que ells tinguin permisos per veure. D'aquesta manera, cada professor podrà organitzar i gestionar les seves assignatures, amb els seus grups d'alumnes i fer seguiment de les diferents dades, com per exemple: assistència, treballs entregats, exàmens que han realitzat, notes i avaluacions. Els professors també podran crear-se alertes quan un alumne deixi d'assistir a classe X vegades, quan no es presenti a exàmens, quan no entregui activitats, quan en fer la mitja de l'assignatura estigui suspès, etc.

  ![image](https://user-images.githubusercontent.com/79162978/211284346-d9346971-f9c3-47f9-89f7-2e5266f5f84c.png)


## Plantilla

Per crear una plantilla que qualsevol pugui fer servir en OpenNebula, primerament, apagarem la màquina desitjada i un cop estigui en estat "POWEROFF", clicarem sobre l'icona de guardar: 

  ![image](https://user-images.githubusercontent.com/79162978/211297982-646bf78b-7956-4faa-af1d-a25893c7d44e.png)

En el quadre de diàleg que se'ns obrirà, ficarem el nom que volguem i aleshores guardarem: 

  ![image](https://user-images.githubusercontent.com/79162978/211298276-ebfeef21-9fd3-4809-ba3c-4dbc10c5f20e.png)

Seguidament, en el menú esquerre lateral, desplegarem Templates i farem click sobre VMs, on trobarem el template guardat: 

  ![image](https://user-images.githubusercontent.com/79162978/211298464-da9e67a9-ff18-4dbe-bf2c-14a3c24ecc18.png)

Ara haurem de canviar els permisos d'ús i accés, pemetent que qualsevol persona pertanyent al grup d'users pugui fer servir i gestionar la plantilla de la màquina: 

  ![image](https://user-images.githubusercontent.com/79162978/211299749-6f5fd981-aa69-4de9-8e1b-2504a599c251.png)

Tornarem a través del menú esquerre lateral a Instancies --> VMs, i crearem una nova màquina fent servir la plantilla que hem creada: 

  ![image](https://user-images.githubusercontent.com/79162978/211300037-a6f81a2a-b9c1-4a94-a1be-494d9671bb78.png) 

- 1 -> Trobem la plantilla que ens interesa, tenim un buscador que és útil quan tenim moltes i no és una plantilla recent.
- 2 -> Assignem un nom a la màquina que es crearà amb la plantilla. 
- 3 -> Farem click sobre crear per obtindre la nova màquina amb la configuració base de la plantilla i tota la estructura d'informació. 

  ![image](https://user-images.githubusercontent.com/79162978/211300724-a0a87d5e-655e-4b2d-ba9f-52e048a7e4c1.png)
 
