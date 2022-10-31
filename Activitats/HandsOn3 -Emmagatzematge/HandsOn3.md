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







