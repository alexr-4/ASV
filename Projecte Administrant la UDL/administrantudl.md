# Administrant la UDL
### Paula, Samantha, Alex

## Servidor LDAP

El nostre servidor LDAP es trobarà a la màquina amb IP: 192.168.101.77

Primerament configurarem un disc dur nou que contindrà la partició de la BBDD: 

- Farem la comanda ```` lsblk ```` per veure els discs que té la màquina i seguidament farem la comanda mkfs.xfs /dev/vdb per executar el disc: 

	![image](https://user-images.githubusercontent.com/79162978/203837076-a7040b97-418b-46dd-acd6-3bb9edd3bea0.png)

- A continuació, crearem el directori que contindrà el disc dur muntat: 

	![image](https://user-images.githubusercontent.com/79162978/203837002-3f8630c3-fda9-4f24-9789-1d94de54e886.png)


- Per veure on és la bbdd:  ```` less /var/lib/openldap/ ```` 
- 

VM1 : Servidor LDAP (ldap-server.udl.cat)
– dc=udl,dc=cat
– Únicament root pot accedir per SSH utilitzant PUBKEY.
– Cada alumne de la classe d’ASV ha de tenir el seu compte amb permisos de sudo.
– La base de dades únicament acceptarà connexions TLS.
– S’inclourà un servei LAM per mantenir i gestionar els comptes.
– El servei LAM únicament podrà ser accessible per SSL.
– Els certificats TLS i SSL hauran de ser self-signed.
– La base de dades LDAP ha d’estar en una partició diferent del Sistema Operatiu.

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
