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

- Al servidor canviarem la password de Jordi: 
- New password: asv01jordi

  ![image](https://user-images.githubusercontent.com/79162978/200110890-5834fd23-abb9-4ce1-a036-7a7a54d24b17.png)

- Canviarem també la del Manel: 
- New password: asv01manel
  
  ![image](https://user-images.githubusercontent.com/79162978/200110952-0dc46456-1017-48bb-9b76-ffb15d3eca52.png)



