# Examen Parcial Novembre

### Paula Uber, Alex Ramon, Samantha Roldán

### 192.168.101.77 (BBDD)
### 192.168.101.74 (CLIENT)
### 192.168.101.61 (LAM SERVER)

- Introduïm els usuaris de Jordi i Manel dintre del sudo visudo: 

  ![image](https://user-images.githubusercontent.com/79162978/200648345-57f479cd-febd-4324-9210-bae548c61e8c.png)

- Canviem la pass de Jordi: 

  ![image](https://user-images.githubusercontent.com/79162978/200648828-f4000d9b-63d7-4417-b0fd-f729c7c3f951.png)

- Canviem la pass de Manel: 

  ![image](https://user-images.githubusercontent.com/79162978/200649110-29e43095-1297-48b6-a4a2-0f3fe12ce659.png)
  
- Creem directoris pel manel i el jordi dintre del /home: 

  ![image](https://user-images.githubusercontent.com/79162978/200649749-253cfdf8-49a9-4a42-995c-4782cb6d0634.png)

- A la màquina del client, entrem com a Manel: 
  
  ![image](https://user-images.githubusercontent.com/79162978/200650143-38a9a1d6-3345-48d6-adb6-12c0f835ac12.png)

### SERVIDOR:

- Ens situem a ````/etc/openldap```` i creem el fitxer ````sudoers.ldif````, i posem el següent contingut:

````
version: 1
dn: ou=sudoers,dc=curs,dc=asv01,dc=udl,dc=cat
objectClass: organizationalUnit
objectClass: top
ou: sudoers

dn: cn=manel,ou=sudoers,dc=curs,dc=asv06,dc=udl,dc=cat
objectClass: sudoRole
objectClass: top
cn: manel
sudoCommand: ALL
sudoHost: ALL
sudoRunAsUser: ALL
sudoUser: manel
sudoOrder: 2

dn: cn=jordi,ou=sudoers,dc=curs,dc=asv06,dc=udl,dc=cat
objectClass: sudoRole
objectClass: top
cn: jordi
sudoCommand: ALL
sudoHost: ALL
sudoRunAsUser: ALL
sudoUser: jordi
sudoOrder: 2

dn: cn=defaults,ou=sudoers,dc=curs,dc=asv06,dc=udl,dc=cat
objectClass: sudoRole
objectClass: top
cn: defaults
sudoOption: env_reset
sudoOption: mail_badpass
sudoOption: secure_path=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin
sudoOrder: 1
````

<img width="1017" alt="Captura de Pantalla 2022-11-10 a las 9 44 51" src="https://user-images.githubusercontent.com/38278207/201044948-8ba2c862-a4ed-4470-b66e-17af25b5dc71.png">

- Ara fem un ````cd schema````i tornem a crear el ````sudoers.ldif````, posant el següent contingut:

````
dn: cn=curs,cn=asv01,cn=udl,cn=cat
objectClass: olcSchemaConfig
cn: sudo
olcAttributeTypes: {0}( 1.3.6.1.4.1.15953.9.1.1 NAME 'sudoUser' DESC 'User(s) who may  run sudo' EQUALITY caseExactIA5Match SUBSTR caseExactIA5SubstringsMatch SYNTAX 1.3.6.1.4.1.1466.115.121.1.26 )
olcAttributeTypes: {1}( 1.3.6.1.4.1.15953.9.1.2 NAME 'sudoHost' DESC 'Host(s) who may run sudo' EQUALITY caseExactIA5Match SUBSTR caseExactIA5SubstringsMatch SYNTAX 1.3.6.1.4.1.1466.115.121.1.26 )
olcAttributeTypes: {2}( 1.3.6.1.4.1.15953.9.1.3 NAME 'sudoCommand' DESC 'Command(s) to be executed by sudo' EQUALITY caseExactIA5Match SYNTAX 1.3.6.1.4.1.1466.115.121.1.26 )
olcAttributeTypes: {3}( 1.3.6.1.4.1.15953.9.1.4 NAME 'sudoRunAs' DESC 'User(s) impersonated by sudo (deprecated)' EQUALITY caseExactIA5Match SYNTAX 1.3.6.1.4.1.1466.115.121.1.26 )
olcAttributeTypes: {4}( 1.3.6.1.4.1.15953.9.1.5 NAME 'sudoOption' DESC 'Options(s) followed by sudo' EQUALITY caseExactIA5Match SYNTAX 1.3.6.1.4.1.1466.115.121.1.26 )
olcAttributeTypes: {5}( 1.3.6.1.4.1.15953.9.1.6 NAME 'sudoRunAsUser' DESC 'User(s) impersonated by sudo' EQUALITY caseExactIA5Match SYNTAX 1.3.6.1.4.1.1466.115.121.1.26 )
olcAttributeTypes: {6}( 1.3.6.1.4.1.15953.9.1.7 NAME 'sudoRunAsGroup' DESC 'Group(s) impersonated by sudo' EQUALITY caseExactIA5Match SYNTAX 1.3.6.1.4.1.1466.115.121.1.26 )
olcAttributeTypes: {7}( 1.3.6.1.4.1.15953.9.1.8 NAME 'sudoNotBefore' DESC 'Start of time interval for which the entry is valid' EQUALITY generalizedTimeMatch ORDERING generalizedTimeOrderingMatch SYNTAX 1.3.6.1.4.1.1466.115.121.1.24 )
olcAttributeTypes: {8}( 1.3.6.1.4.1.15953.9.1.9 NAME 'sudoNotAfter' DESC 'End of time interval for which the entry is valid' EQUALITY generalizedTimeMatch ORDERING generalizedTimeOrderingMatch SYNTAX 1.3.6.1.4.1.1466.115.121.1.24 )
olcAttributeTypes: {9}( 1.3.6.1.4.1.15953.9.1.10 NAME 'sudoOrder' DESC 'an integer to order the sudoRole entries' EQUALITY integerMatch ORDERING integerOrderingMatch SYNTAX 1.3.6.1.4.1.1466.115.121.1.27 )
olcObjectClasses: {0}( 1.3.6.1.4.1.15953.9.2.1 NAME 'sudoRole' DESC 'Sudoer Entries' SUP top STRUCTURAL MUST cn MAY ( sudoUser $ sudoHost $ sudoCommand $ sudoRunAs $ sudoRunAsUser $ sudoRunAsGroup $ sudoOption $ sudoOrder $ sudoNotBefore $ sudoNotAfter $ description ) )
````

<img width="1017" alt="Captura de Pantalla 2022-11-10 a las 9 49 00" src="https://user-images.githubusercontent.com/38278207/201045434-150370ac-2147-4892-9810-e302b5ed15a1.png">

- A continuació executem:

```` ldapadd -Y EXTERNAL -H ldapi:/// -f sudoers.ldif````

- Afegir LDIF al OpenLDAP: (````ldap-password```` és la contrasenya general de gestió LDAP):

````ldapadd -x -D cn=admin,dc=curs,dc=asv,dc=udl,dc=cat -w ldap-password -f sudoers.ldif````

- Reiniciar el servei LDAP:

````sudo systemctl restart slapd````

- Per llegir les definicions de sudo, el client ha de tenir instal·lat el paquet libsss-sudo:

````sudo apt install libsss-sudo````

- Reiniciar sssd per aplicar els canvis:

````sudo systemctl restart sssd````

- Tancar la sessió i tornar a iniciar i comprobar que el nostre usuari de xarxa té drets sudo.

### CLIENT:

````cd /etc/openldap/````

I afegim al final del fitxer ````ldap.conf````:

````SUDOERS_BASE ou=sudoers,dc=asv,dc=udl,dc=cat````

<img width="1017" alt="Captura de Pantalla 2022-11-10 a las 10 01 43" src="https://user-images.githubusercontent.com/38278207/201046897-5418261d-83ba-4efb-86d1-d7ba29460cde.png">

### PROVA FINAL:

<img width="1017" alt="Captura de Pantalla 2022-11-10 a las 10 13 00" src="https://user-images.githubusercontent.com/38278207/201049247-0347843d-b5bd-4dea-8d95-7b23faea3d97.png">
