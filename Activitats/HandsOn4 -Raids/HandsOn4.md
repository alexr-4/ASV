# Raids

Creem una nova màquina:

![image](https://user-images.githubusercontent.com/79162978/199792627-0afbf65d-3892-4f3d-8768-1a8bf176c5ca.png)

Creem dos discs: 

![image](https://user-images.githubusercontent.com/79162978/199793006-087c4393-aa2c-4cb0-8aaa-56bfb1e6bbbc.png)

Asignem els discos a la màquina nova: 

![image](https://user-images.githubusercontent.com/79162978/199793097-790762b0-04f8-444b-a8b7-b11df4e3d8e0.png)

Configurem els dos discos a la màquina: 

![image](https://user-images.githubusercontent.com/79162978/199793260-a8a95c47-094c-4dc5-83b8-d34eea569d9e.png)

![image](https://user-images.githubusercontent.com/79162978/199793441-618de80b-09aa-4588-9d62-9462206f6bbb.png)

Primer fem umount dels dos discos abans de fer particions:

![image](https://user-images.githubusercontent.com/79162978/199795843-89c562d4-0954-4481-b26f-7a4381e26efe.png)

**Crear un RAID1. Utilitzeu dues particions de 100MB. (md1). En aquest raid no es poden executar cap mena de binaris.**

![image](https://user-images.githubusercontent.com/79162978/199794046-8d10e051-24df-4fe8-92c4-ce3a52071959.png)

Creem les particions: 

![image](https://user-images.githubusercontent.com/79162978/199796082-3a363c3c-55a6-430c-ac87-9a8d6e676241.png)

No cal muntar res pq es fa després de les RAIDS. 

**Crear un RAID5. Feu servir 3 particions de 100MB. (md5). Aquest RAID no té limitacions**

Executem la comanda:

 ````[root@localhost ~]# fdisk /dev/vdc````

I ho configurem de la següent manera:

<img width="1440" alt="Captura de Pantalla 2022-11-04 a las 8 21 05" src="https://user-images.githubusercontent.com/38278207/199915676-dbe6fbaf-35c4-4985-829e-d17b3c3da077.png">

A continuació executem: ````[root@localhost ~]# mkfs.xfs /dev/vdc```` tants cops com particions vulguem definir

<img width="1440" alt="Captura de Pantalla 2022-11-04 a las 8 25 31" src="https://user-images.githubusercontent.com/38278207/199916461-d9edfca0-1554-4edc-abbb-e1cc0f761aab.png">


**Els raids s’han de muntar al path /mnt/raid1 i /mnt/raid5 i s’hauran de muntar de forma automàtica a l’inici del sistema. S’ha de crear l’usuari Chuck i aconseguir que únicament pugui fer servir 50MB, creant un màxim de 5 fitxers.**

- Primerament muntarem el raid1 i el raid5, però per fer-ho, necessitem instalar ```` yum install -y mdadm ```` :

  ![image](https://user-images.githubusercontent.com/79162978/202512578-33da577d-77a1-4ed2-ad77-a29517ae92aa.png)
 
### MD1
- Amb la comanda  ````  mdadm --create --verbose /dev/md1 --level=1 --raid-devices=2 /dev/vdb1 /dev/vdb2 ```` passarem el nom de la raid, el nivell de la raid i els discs que té assignats que seran 2 devices amb els noms de /dev/vdb1 i /dev/vdb2:

  ![image](https://user-images.githubusercontent.com/79162978/202515785-adecf70c-49e3-42f5-9a54-497972dfb943.png)
  
  ![image](https://user-images.githubusercontent.com/79162978/202516203-53464a0f-490b-4f9a-981f-a9dff42690e7.png)

### MD5
- Fem la mateixa comanda per el MD5: 

  ![image](https://user-images.githubusercontent.com/79162978/202516411-9d7eb8c8-2e88-4725-8c92-55cf9f640ecf.png)

- Per afeguir als directoris les raid i muntarles allà: 

![image](https://user-images.githubusercontent.com/79162978/202517868-5a704781-0a64-47ff-a7bd-e51602e213b4.png)
