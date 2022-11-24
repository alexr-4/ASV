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



VM1 : Servidor LDAP (ldap-server.udl.cat)
~~dc=udl,dc=cat~~

~~Únicament root pot accedir per SSH utilitzant PUBKEY.~~

– Cada alumne de la classe d’ASV ha de tenir el seu compte amb permisos de sudo.

– La base de dades únicament acceptarà connexions TLS.

– S’inclourà un servei LAM per mantenir i gestionar els comptes.

– El servei LAM únicament podrà ser accessible per SSL.

– Els certificats TLS i SSL hauran de ser self-signed.

--> HECHO --> ~~La base de dades LDAP ha d’estar en una partició diferent del Sistema Operatiu.~~


## Servidor NFS

Els directoris home dels usuaris estaran en una RAID5 o en una RAID10.
- Únicament root pot accedir per SSH utilitzant doble factor de verificació (password + codi).
- Configurarem un servei de dades al núvol utilitzant owncloud.

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

Els directoris /home es muntaran sota demanda, únicament quan l’usuari accedeixi al sistema.

## 
