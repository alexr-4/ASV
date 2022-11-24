# Administrant la UDL
### Paula, Samantha, Alex

## Servidor LDAP

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
