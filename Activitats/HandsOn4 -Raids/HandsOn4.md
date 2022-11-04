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


**Els raids s’han de muntar al path /mnt/raid1 i /mnt/raid5 i s’hauran de muntar de forma automàtica a l’inici del sistema. S’ha de crear l’usuari Chuck i aconseguir que únicament pugui fer servir 50MB, creant un màxim de 5 fitxers.**



