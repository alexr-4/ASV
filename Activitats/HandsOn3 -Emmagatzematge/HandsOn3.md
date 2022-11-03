# Xifrant discos i particions

## Xifrant un disc amb LUKS

Instal·lem el crytsteup: 

![image](https://user-images.githubusercontent.com/79162978/199056557-dd6364e9-0158-49ad-8bc1-c9764db8b9b7.png)

Fiquem la pass de s@m@nth@94 ja que no ens deixava ficar asv01234 i creem un sistema de fitxer a la nostra partició xifrada: 

![image](https://user-images.githubusercontent.com/79162978/199059532-5e5b842f-e3c0-480e-8b70-23926e6effb9.png)

Crearem un sistema de fitxer a la nostra partició xifrada:

![image](https://user-images.githubusercontent.com/79162978/199059895-4608c387-2c6d-4c19-ac2d-8ca2b7c69abd.png)

Crearem el nou directori utilitzat per al punt de muntatge del sistema de fitxers xifrat i muntarem el disc: 

![image](https://user-images.githubusercontent.com/79162978/199060143-2dbcc551-3511-412f-ab54-95216ac68f2b.png)


## Automount

Creeu un fitxer de claus per al muntatge automàtic. Podeu afegir qualsevol contingut que vulgueu a aquest fitxer, fins i tot passhprase, però una bona manera per omplir-lo es utiltizant dades aleatòries: 

![image](https://user-images.githubusercontent.com/79162978/199060387-9bc347c2-5a25-4805-afed-5e4db143f3d8.png)

Afegiu el fitxer de clau al dispositiu de subministrament de cryptsetup i els arguments de localització de fitxers de claus i introduïu la contrasenya que heu utilitzat al primer pas.
Afegiu una nova entrada a /etc/fstab per muntar el disc a a l’arrencada.
Afegiu una nova entrada a /etc/crypttab: Aquest informació s’utiltizarà per desxifrar amb èxit el vostre disc. Heu de subministra el nom, el dispositiu i la ubicació del fitxer de claus del mapatge de dispositius:

![image](https://user-images.githubusercontent.com/79162978/199060935-b0489420-e921-42de-b257-e4f47f0d079b.png)

## Sistema de fitxers distríbuits

Instal·lem paquets: 

![image](https://user-images.githubusercontent.com/79162978/199061621-7d495456-59dc-46f9-9a00-a0818dd4d27b.png)

Crearem una disc, l’afegirem, formatejarem i muntarem. Assumirem que aquest punt de muntatge és /mnt/data: Farem servir el mateix dics que ja teniem, ja que era de prova i no passa res si el "reutilitzem". 

Instal·lem el firewall amb la comanda de dnf install firewalld -y i el ficarem en enable i l'iniciarem: 

![image](https://user-images.githubusercontent.com/79162978/199062982-d1d72168-e10c-47eb-bec3-91d9b189b39e.png)

Habilitarem dels serveis: 

![image](https://user-images.githubusercontent.com/79162978/199063562-f1454dbf-21dc-4652-9746-0f616a89d3a5.png)

Editarem l'arxiu /etc/exports per configurar els directoris que volem que estiguin disponibles per NFS i definirem permisos/protocols que podem emprar: 

![image](https://user-images.githubusercontent.com/79162978/199066378-f8486194-9663-4629-bd9f-65ed90a7c084.png)

Arguments:
- /mnt/data: Es el directori a compartir
    xxx.xxx.xx.xx / 24: IP de la màquina client amb la mascara de subred
    rw: Son permisos de escritura sincronització.
    sync: Tots els canvis en el sistema d’arxius corresponents fan commit immediatament;
    no_root_squash: De forma predeterminada, qualsevol sol·licitud d’arxiu realitzada per l’usuari root a la màquina client es tracta com per l’usuari nobody al servidor. Si es selecciona no_root_squash, el root a la màquina client tindrà el mateix nivell d’accés als fitxers del sistema com root al servidor.
  
- Guardem les modiciacions i exportem els fitxers i reiniciem els serveis: 

  ![image](https://user-images.githubusercontent.com/79162978/199064826-0297878f-9ac6-4e45-a36e-035133313de5.png)

## Instal·lant un client NFS

Instanciem una nova màquina: 

![image](https://user-images.githubusercontent.com/79162978/199067100-78879b02-1565-436c-a524-71d9db414301.png)

![image](https://user-images.githubusercontent.com/79162978/199067065-16b379a0-ad50-4a34-9498-4c5eadb13cdd.png)

![image](https://user-images.githubusercontent.com/79162978/199067957-b7ea8af2-dae5-4584-9ab6-774bf7eab38d.png)

Ja es connecten entre si les dues màquines:: 

![image](https://user-images.githubusercontent.com/79162978/199068879-f360ffbb-76e2-4311-b701-6e7f016543c4.png)

# Activitat de seguiment

Creem un nou disc dur: 

![image](https://user-images.githubusercontent.com/79162978/199776495-cd5c5ff6-0181-4541-b11e-ada53eb837b8.png)

Formatem el xfs pel nou disc vdb:

![image](https://user-images.githubusercontent.com/79162978/199778266-2d9579f6-1342-4889-8910-5588677522c9.png)

Creem la carpeta: mkdir /mnt/data

Muntem el disc i comprovem que estigui muntat: 

![image](https://user-images.githubusercontent.com/79162978/199778548-b2a45ad2-740a-41b6-bd89-f2422b86cbbe.png)


Veiem amb fdisk -l els diferents disc que tenim a la nostra màquina. L'últim és el nou: 

![image](https://user-images.githubusercontent.com/79162978/199778748-117b7402-f66b-46f8-8147-10c10da2bff5.png)

Per fer les dues particions: 

![image](https://user-images.githubusercontent.com/79162978/199780728-0b9da3c7-8a9c-45f0-ac86-c6c0a3c30ec8.png)


Muntem una primera partició que serà pel home i serà el /dev/vdb1:

- mkfs.ext4 /dev/vdb1
- mount /dev/vdb1 /mnt/data
- df -h

![image](https://user-images.githubusercontent.com/79162978/199782478-6f9715fd-66c8-4b86-9f79-f7cc9d2e4440.png)

![image](https://user-images.githubusercontent.com/79162978/199782597-26ef5f9f-3432-4cf4-a0b3-137ddc0469bc.png)


Muntem una segona partició que serà pels logs i serà el /dev/vdc2: 

![image](https://user-images.githubusercontent.com/79162978/199782546-8da4024d-9dea-4b00-a032-4384d76468a9.png)

![image](https://user-images.githubusercontent.com/79162978/199782641-fe831a54-0c3c-4aef-9769-a4dc9d42b541.png)

Fem df -h i veiem que el sistema el tenim a la partició: /dev/vda1       4.0G  974M  3.1G  24% /

El home el tenim a: /dev/vdb1       245M   15M  231M   6% /home

I els logs a: /dev/vdb2       245M   15M  231M   6% /var/log

![image](https://user-images.githubusercontent.com/79162978/199782703-70013dc0-0a56-40a9-931a-8ba6e468581f.png)

Script per omplir (petar) la partició: 

fallocate -l 50G big_file

Si omplim la carpeta home o logs no passa res perquè l'usuari sempre pot donar més espai a la partició o esborrar fitxers, però, en el moment que omplim la partició del sistema ja no hi ha marxa enrere. El sistema queda inutilitzat i no permet fer cap acció a l'usuari, havent de forçar accions de l'administrador. 


Enllaç interessant per solucionar el problema d'omplició de disc: https://docs.bluehosting.cl/troubleshooting/servidores/guia-para-solucionar-el-problema---la-particion-root-esta-llena.html








