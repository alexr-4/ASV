# ASV Summary. Alex Ramon, Paula Uber & Samantha Roldán

<center>

<a href="url"><img src="https://redfibra.mx/wp-content/uploads/que-es-cloud-computing-1.jpg" align="center" height="250" width="250" ></a>

</center>

# Week 00

***Que he aprés?***

El concepte d'un administrador de sistemes, la seva funcio i utilitat dins del mon empresarial; Entenem que es necessari en moltissims entorns reals de treball, per instal·lar, configurar i mantenir òptimament qualsevol infraestructura de xarxes i/o sistemes informàtics, i per donar suport als usuaris, una mica un "tot terreny" que té controlat tot lo relacionat amb la informatica. 

Creiem que també es especialment important coneixer la nomenclatura de l'ambit: switch, hub, conenctors, rack, Adreça IP, RJ, CPD, Servidors, Antenes, Routers, Acces Point.. Ja que en realitat al llarg de la universitat sempre hem treballat tots aquests conceptes de manera teorica (en assignatures com xarxes...) i creiem que amb el que se'ns explica (i s'explicara) podem realacionar per a que serveix cada aparell de xarxa i la seva importantia dins d'una infraestructura de xarxa.

Destacar l'altissima imopotrancia del bon manteniment d'una sala CPD: Posar mútltiples aires acondicionats i demés aparells per refrigerar el clima per tal de que els servidors estiguin en condicions de climatitzacio bones, que afavoreixi el correcte funcionament. Al final, son màquines que treballen constantment i és vital que no es sobrecalentin.

També hem conegut el servei SSH, com atacar a una maquina per SSH, entendre el funcionament de una VPN i saber crear i gestionar un servidor web amb un wordpress.

Coneixer els sitemes CENTOS i Rocky Linux, i valorar quin dels 2 ens interessa més de cara al plantejament de l'assignatura
 
***Que he consultat?***

- https://www.ionos.es/digitalguide/servidores/configuracion/rocky-linux/

- https://geekland.eu/fingerprint-servidor-ssh/

- https://blog.trescomatres.com/2020/01/saber-los-puertos-abiertos-en-servidor/

- https://www.tecmint.com/fix-failed-to-set-locale-defaulting-to-c-utf-8-in-centos/


***Quines preguntes m'han sorgit?***
 
- Com puc atacar a una maquina per SSH? Quina comanda he de fer servir?

- Com podem separar en maquines diferents els serveis (sql, web, ...)?

- Que es un CPD i servidor?

- Que es el que fa realment un administrador?

# Week 02

***Que he aprés?***

Hem acabat de consolidar coneixements més especifics de client-servidor i aprés a configurar un servidor didactic per alumnes, un curs de programació. En aquest servidor gran, hem aprés a configurar especificament, a base d'uns requeriments, un servidor linux. Crear usuaris, definir contrassenyes, especificar permisos, crear grups i rols, servidors, ... tot això englobat dins d'un jupyter hub, un servidor gran que dona servei als alumnes.

Entendre els conceptes de:

- R: Permís de lectura

- W: Escriptura

- X: Execució

Que sovintment fem servir quan executem comandes de ``` chmod 777 ``` (permisos maxims a usuari local, grup local, i els altres)

Relacionar que moltissimes utilitats que podem instal·lar a linux, tenen un fitxer de configuració acabat en ``` .conf ``` i que aquest sempre el podem editar amb el vim o nano, i treure'ns la por de no voler-lo tocar per "trencar algo"



Destacar fitxers profunds de linux que ens han resultat interessants com:

- ```/etc/group/ ``` Conté les definicions dels grups

- ``` /etc/shadow/ ``` Conté contrassenyes dels usuaris, sol pot accedir root

- ``` /etc/group ``` Conté definicions dels grups

- ``` /etc/passwd ``` Conté la base de dades d’usuaris del sistema.

- ```psacct ``` Aquesta eina de gestió tant potent ens permet tenir un control total dels esdeveniments que ocorren dins del nostre SO

Destacar el concepte d'enginyeria social, que es basa en trobar relació social entre les persones de la persona afectada, per arribar a la nostra finalitat

En definitiva, crec que cada cop anem consolidant més els nostres coneixements per a ser un administrador de linux, al final també entenem que es impossible saber-se tots els racons de linux i comandes, pero tenir una base forta i poder relacionar conceptes per aprendre a trobar-los crec que es un camí que podrem anar asssolint

***Que he consultat?***

-  https://blog.desdelinux.net/permisos-y-derechos-en-linux/

-  https://jupyterhub.readthedocs.io/en/stable/

_  https://atareao.es/como/gestion-de-usuarios-y-grupos-en-linux/

-  https://www.linuxtotal.com.mx/index.php?cont=info_admon_013

***Quines preguntes m'han sorgit?***

- Que es un servidor jupyterlab?

# Week 03

***Que he aprés?***

En aquesta setmana hem treballat, en un enfocament plenament pràctic, sobre com plantejar un servidor LAMP:

- Linux

- Apache

- Mysql

- PHP

Entenem un servidor LAMP el host d'una plataforma, on es poden connectar els clients per realitzar X tasca.  Hem apres a fer la tasca de sysadmin dins d'aquest servidor, configurant preferències del propi servidor, dels usuaris que entren dins d'aquest, i demés elements de configuració.

![lamp](https://user-images.githubusercontent.com/38278207/197358218-d190718e-c7d5-4bd2-9817-c219c2537cfe.jpg)

Hem treballant amb aquestes 2 màquines:

<img width="1436" alt="Captura de Pantalla 2022-10-22 a las 21 04 11" src="https://user-images.githubusercontent.com/38278207/197358175-8bd46228-7ded-40a8-8755-76f0b9ce1c14.png">

- La maquina server, es la que te el client, i es la que nosaltres com a admin. Es molt personalitzable

- La maquina client, ens es la que es connecta com a usuari al servidor, la que inicia sesio

Tambe hem treballat el concepte de **Kerberos**, que ara sabem que es un protocol de seguretat que ens dona un plus de seguretat dins de la nostra infrastructura de xarxa, mitjançant el seu funcionament (ho expliquem detalladament a la ACT2). Com a conclusió entre fer servir Kerberos i un servidor LAMP, hem plantejat que el millor es fer-los servir tots 2 alhora si es pot; perque així tenim un sistema d'usuaris + un protocol de seguretat.

***Que he consultat?***

- https://es.wikipedia.org/wiki/LAMP

- https://blog.infranetworking.com/servidor-lamp/

***Quines preguntes m'han sorgit?***

- Per a que serveix un servidor LAMP?

- Com instal·lar-lo?

# Week 06

***Que he aprés?***

In this week, me have seen a lot of deep concepts of a linux operative system. We think it's important to know the file system:

<img width="1436" alt="Captura de Pantalla 2022-11-27 a las 17 50 05" src="https://user-images.githubusercontent.com/38278207/204148875-0c46b736-97de-4f1d-8b13-f8adb0ece917.png">

That is so diferent In comparison of a Windows system. Really, we have been working in most of this directories becasuse the configuration of a lot of services of the VM, needs to have a big kndowedge of this directories.

Also, we have seen how to create a new disk and put it in the VM, and, inside, create partitions; a RAID system. Some interesting commands:

```
$ mkfs.xfs /dev/vdb #Formatar en xfs -> $ fdisk -l 
$ mount /dev/vdb /mnt/data/ #Muntar el disc al punt de muntatge
$ df -h #Observar el nou disc muntant
$ fdisk -l
reboot
$ vi /etc/fstab

```

Another interessting point is how to encrypt the discs; we can do it with the LUKS tool. To access the password decryption of the device, the user must provide a pass phrase or an authentication key

We must follow the next steps:

```
dnf install cryptsetup -y
cryptsetup luksFormat /dev/vdb
cryptsetup luksOpen /dev/vdb privateDisk
mkfs.xfs /dev/mapper/privateDisk
mkdir -p /mnt/private
mount /dev/mapper/privateDisk /mnt/private/
df -h
dd if=/dev/urandom of=keyfile bs=1024 count=4
cryptsetup luksAddKey /dev/vdb keyfile
echo "/dev/mapper/privateDisk /mnt/private xfs defaults 1 2" >> /etc/fstab
echo "privateDisk /dev/vdb keyfile1 luks" >> /etc/crypttab


We study the distributred file system -> we able to share files and directories with a lot of users.

For do it, we need to install an NFS server:
```
yum  install nfs-utils -y
setsebool -P nfs_export_all_ro=1 nfs_export_all_rw=1 
firewall-cmd --permanent --add-service nfs
firewall-cmd --reload

systemctl enable rpcbind
systemctl enable nfs-server
systemctl start rpcbind
systemctl start nfs

vi /etc/exports
/mnt/data xxx.xxx.xx.xx/24(rw,sync,no_root_squash)

exportfs -avr
systemctl restart rpcbind
systemctl restart nfs
```
Also wee must install a NFS client:

```
yum install nfs-utils -y
systemctl enable rpcbind
systemctl start rpcbind


mkdir /mnt/data
mount -t nfs -o rw ip-servidor:/mnt/data/ /mnt/data
echo  ip-servidor:/mnt/data/ /mnt/data nfs rw,sync,hard,intr 0 >> /etc/fstab
```

For follow the command steps more correctly -> watch de theory:

https://cv.udl.cat/portal/site/102378-I-2223/tool/51aae730-7529-4b62-8711-ca50fe7babce?panel=Main


***Que he consultat?***

- https://man7.org/linux/man-pages/man8/mount.8.html
- https://www.dell.com/support/kbdoc/es-es/000131456/los-tipos-y-las-definiciones-de-ubuntu-linux-particiones-y-directorios-explicados

***Quines preguntes m'han sorgit?***
 
- Per que esta tot tan dividit en un sistema linux? per que hi ha tantes particions?
- Per a que serveix un servidor NFS?

