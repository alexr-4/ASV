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


