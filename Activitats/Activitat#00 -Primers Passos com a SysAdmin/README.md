@Autors:
Paula Uber
Alex Ramon
Samantha Roldán


1 Part teòrica

Pregunta 1

CENTOS 7 es el sistema operativo padre de RockyLinux. RockyLinux nace tras la necesidad que deja CENTOS 7 al dejar de actualizarse. La comunidad crea RockyLinux para poder trabajar de forma gratuita, estable, fiable y fácil de usar.

Actualmente, entre estos dos, recomendariamos RockyLinux porque a pesar de que las actualizaciones se van haciendo de forma lenta, ofrece un sistema actualizado y seguro con el que poder trabajar.

Pero, investigando, hemos podido ver que RockyLinux como hemos comentado, tiene el handicap de la lentitud de las actualizaciones dentro del sistema. Esto hace que paralelamente existan otros sistemas operativos que satisfacen las necesidades de los usuarios, como por ejemplo, Centos Stream. Centos Stream es un sistema operativo que está en constante actualización, pero, tiene el inconveniente de que todos los usuarios lo usasn como sistema de pruebas y esto no lo hace seguro.

https://www.ionos.es/digitalguide/servidores/configuracion/rocky-linux/

Pregunta 2

El Fingerprint sirve para generar tanto las claves públicas como privadas en el momento de crear un servidor SSH. Esto genera una huella digital que nos permite registrarnos y usar el servidor SSH. A esta huella se le llama fingerprint y su principal función es identificar de forma inequívoca un servidor.

Los problemas que intenta solucionar son principalmente dos: que no nos conectemos a servidor ssh malicioso y evitar ataques "man in the middle".

https://geekland.eu/fingerprint-servidor-ssh/

2 Part pràctica

Pregunta 3

Los puertos que tenemos abiertos son:
- 22/tcp   open  ssh     OpenSSH 8.0 (protocol 2.0)
- 80/tcp   open  http    Apache httpd 2.4.37 ((rocky))
- 3306/tcp open  mysql   MySQL 5.5.5-10.3.35-MariaDB

Los hemos identificado leyendo el siguiente artículo: https://blog.trescomatres.com/2020/01/saber-los-puertos-abiertos-en-servidor/

Los pasos que hemos seguido han sido:
1- Instalar: dnf install nmap
2- Detectar el servidor: localhost
3- Ver el mapeado: nmap -A -T4 localhost
4- Fijarse en los servidores abiertos (open).

Pregunta 4

Para resolver esta pregunta, hemos investigado en Google y hemos encontrado este artículo:
https://www.tecmint.com/fix-failed-to-set-locale-defaulting-to-c-utf-8-in-centos/

El comando que hemos utilizado para solucionar el problema de idioma del usuario/región ha sido:

localectl set-locale LANG=en_US.UTF-8

Pregunta 5

El cambio se ha realizado desde la propia máquina virtual:
![image](https://user-images.githubusercontent.com/79162978/191787096-ed70729a-e047-4c8b-9a4c-0e4e0b922649.png)

