# Examen Novembre

### Alex Ramon, Samantha Roldan, Paula Uber
### IP SERVIDOR: 192.168.101.134
### IP CLIENT: 192.168.101.135

## Enunciat

https://cv.udl.cat/portal/site/102378-I-2223/tool/30bc091b-19f7-49bd-b41a-064a532d7de4?panel=Main

**Aconseguir configurar una màquina, client, que utilitzi el servidor d'autenticació centralitzada LDAP, on els usuaris que vosaltres configureu puguin esdevenir root.**

**Aquesta configuració s'ha de fer a la base de dades LDAP, de manera que aquests usuaris puguin esdevenir root en qualsevol màquina de l'organització.**

#### Creem dues màquines noves

![image](https://user-images.githubusercontent.com/79162978/200113344-14cbdfad-ac43-4c21-9743-b68d87163000.png)

#### Executem scrips per a configuració del ldap server i client

- SERVER

  ![image](https://user-images.githubusercontent.com/79162978/200113360-77474ea5-4cfa-49a4-a855-cf98f8760c1f.png)

- CLIENT
  
  ![image](https://user-images.githubusercontent.com/79162978/200113749-656bb579-f411-4cde-bf32-fcc0e53f468a.png)


#### Afegir la clau pública Jordi

- SERVER

<img width="1017" alt="Captura de Pantalla 2022-11-05 a las 10 52 26" src="https://user-images.githubusercontent.com/38278207/200113943-304d5036-f61a-4432-81f0-a2d7c02e89b3.png">

- CLIENT

<img width="1017" alt="Captura de Pantalla 2022-11-05 a las 10 50 15" src="https://user-images.githubusercontent.com/38278207/200113846-649dd7ee-2c6b-40a3-a3e0-c842aa2bf49d.png">


#### Canviar password dels usuaris

- Al servidor canviarem la password de jordi: 
- New password: jordi

<img width="1017" alt="Captura de Pantalla 2022-11-05 a las 11 06 44" src="https://user-images.githubusercontent.com/38278207/200114559-78a4f257-5d94-4408-b7bd-0bdf6dc00465.png">

- Canviarem també la del manel: 
- New password: manel
  
<img width="1017" alt="Captura de Pantalla 2022-11-05 a las 11 07 24" src="https://user-images.githubusercontent.com/38278207/200114582-7b3d9d66-1cca-4d72-ae5f-3207cc4decad.png">

- Donem permisos de superususari a manel i jordi fent ````sudo visudo````:

<img width="1017" alt="Captura de Pantalla 2022-11-05 a las 11 09 15" src="https://user-images.githubusercontent.com/38278207/200114640-cb20834a-ea80-4ba9-9d11-51dfc5d14645.png">

- Hem editat el fitxer hosts al client, afegint el servidor. ````vim /etc/hosts````:

<img width="1017" alt="Captura de Pantalla 2022-11-05 a las 11 16 00" src="https://user-images.githubusercontent.com/38278207/200114889-3399e7ae-cb21-4609-9a18-a4410a684908.png">

- Editem el fitxer de configuració ```vim slapd.conf```` al servidor:

<img width="1017" alt="Captura de Pantalla 2022-11-05 a las 11 19 35" src="https://user-images.githubusercontent.com/38278207/200115034-b0dff15b-210c-4bf1-85dd-5c7e746caf38.png">

- Executem la següent comanda:

````
mkdir /pki
[root@localhost openldap]# openssl req -days 500 -newkey rsa:4096 \
>     -keyout /pki/ldapkey.pem -nodes \
>     -sha256 -x509 -out /pki/ldapcert.pem
````

I completem els camps requerits:

<img width="1017" alt="Captura de Pantalla 2022-11-05 a las 11 24 51" src="https://user-images.githubusercontent.com/38278207/200115231-bb3ee973-6c82-4f95-8318-7abc9cd0488b.png">

Seguim executant comandes de configuració (comunicacions de connexions segures SSL TLS):

<img width="1017" alt="Captura de Pantalla 2022-11-05 a las 11 26 07" src="https://user-images.githubusercontent.com/38278207/200115280-1253f7ff-672e-4c2c-8002-41b41229fbb6.png">

<img width="1017" alt="Captura de Pantalla 2022-11-05 a las 11 26 29" src="https://user-images.githubusercontent.com/38278207/200115290-8ceac612-effe-4df4-b5a1-38e13f7109e5.png">

<img width="1017" alt="Captura de Pantalla 2022-11-05 a las 11 27 22" src="https://user-images.githubusercontent.com/38278207/200115320-a9f33bfd-f4f0-4d04-80fc-25d985e077bf.png">

- Editem ```` vim ldap.conf ````:

<img width="1017" alt="Captura de Pantalla 2022-11-05 a las 11 28 03" src="https://user-images.githubusercontent.com/38278207/200115351-53cad8fc-f318-406b-a032-d5c4516826c0.png">
