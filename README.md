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



