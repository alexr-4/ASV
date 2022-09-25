###### @Autors:
Paula Uber,
Alex Ramon,
Samantha Roldán


# 1 Part teòrica

## Pregunta 1

CENTOS 7 es el sistema operativo padre de RockyLinux. RockyLinux nace tras la necesidad que deja CENTOS 7 al dejar de actualizarse. La comunidad crea RockyLinux para poder trabajar de forma gratuita, estable, fiable y fácil de usar.

Actualmente, entre estos dos, recomendariamos RockyLinux porque a pesar de que las actualizaciones se van haciendo de forma lenta, ofrece un sistema actualizado y seguro con el que poder trabajar.

Pero, investigando, hemos podido ver que RockyLinux como hemos comentado, tiene el handicap de la lentitud de las actualizaciones dentro del sistema. Esto hace que paralelamente existan otros sistemas operativos que satisfacen las necesidades de los usuarios, como por ejemplo, Centos Stream. Centos Stream es un sistema operativo que está en constante actualización, pero, tiene el inconveniente de que todos los usuarios lo usasn como sistema de pruebas y esto no lo hace seguro.

https://www.ionos.es/digitalguide/servidores/configuracion/rocky-linux/

## Pregunta 2

El Fingerprint sirve para generar tanto las claves públicas como privadas en el momento de crear un servidor SSH. Esto genera una huella digital que nos permite registrarnos y usar el servidor SSH. A esta huella se le llama fingerprint y su principal función es identificar de forma inequívoca un servidor.

Los problemas que intenta solucionar son principalmente dos: que no nos conectemos a servidor ssh malicioso y evitar ataques "man in the middle".

https://geekland.eu/fingerprint-servidor-ssh/

# 2 Part pràctica

## Pregunta 3

Los puertos que tenemos abiertos son:
- 22/tcp   open  ssh     OpenSSH 8.0 (protocol 2.0)
- 80/tcp   open  http    Apache httpd 2.4.37 ((rocky))
- 3306/tcp open  mysql   MySQL 5.5.5-10.3.35-MariaDB

Los hemos identificado leyendo el siguiente artículo: 
https://blog.trescomatres.com/2020/01/saber-los-puertos-abiertos-en-servidor/

Los pasos que hemos seguido han sido:
1. Instalar: dnf install nmap
2. Detectar el servidor: localhost
3. Ver el mapeado: nmap -A -T4 localhost
4. Fijarse en los servidores abiertos (open).

## Pregunta 4

Para resolver esta pregunta, hemos investigado en Google y hemos encontrado este artículo:
https://www.tecmint.com/fix-failed-to-set-locale-defaulting-to-c-utf-8-in-centos/

El comando que hemos utilizado para solucionar el problema de idioma del usuario/región ha sido:

localectl set-locale LANG=en_US.UTF-8

## Pregunta 5

El cambio se realiza desde la terminal con el comando hostname [nombre nuevo]. 
Seguidamente, para verificar que el cambio se ha realizado correctamente, lanzamos hostname o hostnamectl para ver más detalles. 

![image](https://user-images.githubusercontent.com/79162978/191810208-541e4167-f4ce-4c1a-9a21-a4f56bd4fad1.png)

## Pregunta 6

![image](https://user-images.githubusercontent.com/79162978/191810819-6dbed02d-96b8-4c0b-ad3f-9440ff64a478.png)

## Pregunta 7

Generat la clau publica a la maquina .84 (la que és servidor web), amb la comanda:

``` ssh-keygen -t ed25519 ```

I introduint aquesta clau al fitxer authorized keys (.ssh/authorized_keys) de la maquina .83 (la que te la bbdd)

<img width="1017" alt="Captura de Pantalla 2022-09-25 a las 19 56 51" src="https://user-images.githubusercontent.com/38278207/192158036-8be3e3f4-02bc-4b59-b065-17e32c5f3410.png">


Hem creat al directori /etc/bin a la maquina .84 el següent script amb el nom ``` db-server ```, que es converteix en una comanda que ataca per ssh a la maquina .83 i no ens demana contrassenya.

<img width="1017" alt="Captura de Pantalla 2022-09-25 a las 19 59 22" src="https://user-images.githubusercontent.com/38278207/192158146-4fd8209a-1675-42c9-8c1f-020527346805.png">

Dins de la maquina .83, per donar permisos a la BD amb aquest nou usuari que ve de la .84, iniciem bbdd i executem la següent comanda:

<img width="973" alt="Captura de Pantalla 2022-09-22 a las 23 20 52" src="https://user-images.githubusercontent.com/38278207/192158216-610e402b-7d0b-4bad-8b5b-aaea32264c60.png">
