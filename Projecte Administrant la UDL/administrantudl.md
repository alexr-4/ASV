# Administrant la UDL
### Paula, Samantha, Alex

## Servidor LDAP

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




VM1 : Servidor LDAP (ldap-server.udl.cat)

~~dc=udl,dc=cat~~

~~Únicament root pot accedir per SSH utilitzant PUBKEY.~~

– Cada alumne de la classe d’ASV ha de tenir el seu compte amb permisos de sudo.

– La base de dades únicament acceptarà connexions TLS.

~~S’inclourà un servei LAM per mantenir i gestionar els comptes.~~

– El servei LAM únicament podrà ser accessible per SSL.

– Els certificats TLS i SSL hauran de ser self-signed.

~~La base de dades LDAP ha d’estar en una partició diferent del Sistema Operatiu.~~

## Servidor NFS

### Els directoris home dels usuaris estaran en una RAID5 o en una RAID10.
	- Configurem els tres discos de la màquina: (''''mkfs.xfs /dev/vdb'''', ''''mkfs.xfs /dev/vdc'''', ''''mkfs.xfs /dev/vdd''''):
	![image](https://user-images.githubusercontent.com/83337658/203839115-2c98f88e-7b4c-4299-92c2-3356d8226c2c.png)
	- inslatar el mdadm: ''''yum install -y mdadm''''
	- fer: ''''mdadm --create --verbose /dev/md5 --level=5 --raid-devices=3 /dev/vdb /dev/vdc /dev/vdd'''':
	![image](https://user-images.githubusercontent.com/83337658/203839753-4f2fe590-b75f-494d-bdf3-1309c4f46e97.png)
	- muntem la raid 5 al punt de muntatge /mnt/home: ''''mount /mnt/home/ /dev/md5'''', ''''mkfs.xfs /dev/md5'''', ''''mount /dev/md5 /mnt/home/''''

	![image](https://user-images.githubusercontent.com/83337658/203841870-6b43e0bc-e5eb-4523-a878-b7da0ea42765.png)
	- amb ''''blkid'''' busquem la raid i la enganchem a '''''vi /etc/fstab'''':
	![image](https://user-images.githubusercontent.com/83337658/203841964-bc5d3915-baee-4fdf-b37e-660576766c2c.png)
	![image](https://user-images.githubusercontent.com/83337658/203842635-7edec2d4-ad10-42e8-a183-b91d6b2cf480.png)

	
### Únicament root pot accedir per SSH utilitzant doble factor de verificació (password + codi).

- Per veure el fitxer de configuració ```` vim /etc/ssh/sshd_config ````, haurem de canviar les següents linies: 

	![image](https://user-images.githubusercontent.com/83337658/205112244-57aed6a5-68be-4cc0-9a8d-6931e12e497e.png)

- Se li ha d'assignar al root una password amb ````passwd```` --> 1234
- Després fem un ````systemctl restart sshd```` per reiniciar el sistema. 
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
![image](https://user-images.githubusercontent.com/83337658/205117262-303293b3-3c47-43de-b0f5-25cf10e619bf.png)
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

## 
