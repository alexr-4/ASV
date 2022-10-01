# ACTIVITAT 01 - CURS DE PROGRAMACIÓ

## Pregunta 1: Configurar servidor

Hem creat una maquina rocky linux nova anomenada: curs-coding-asv01-server. Amb la IP .109:

<img width="1436" alt="Captura de Pantalla 2022-10-01 a las 16 38 10" src="https://user-images.githubusercontent.com/38278207/193414642-8c76eb30-1c34-4689-857c-de1b1df9bd54.png">

Creació usuari admin. password: adminadmin.

<img width="1017" alt="Captura de Pantalla 2022-09-29 a las 20 49 47" src="https://user-images.githubusercontent.com/38278207/193117424-40391aaf-e53e-4b99-9fbf-22ff2472cdb6.png">

Li donem permissos de superusuari dins del ``` sudo visudo ```:

<img width="1017" alt="Captura de Pantalla 2022-09-29 a las 20 50 43" src="https://user-images.githubusercontent.com/38278207/193117725-fa9bcf3f-8966-4077-b069-0236fea589e8.png">

Creem grups alumne i professorat:

<img width="527" alt="Captura de Pantalla 2022-09-29 a las 20 54 58" src="https://user-images.githubusercontent.com/38278207/193118418-94762ea7-b545-4ffc-b4c1-a762d2e55d09.png">


Per onar permisos máxims al directori /home/alumne/, directament em fet que el propietari del directori alumne sigui el grup professorat, de manera que aquest grup ja tindra permissos: 

<img width="1017" alt="Captura de Pantalla 2022-09-29 a las 21 01 53" src="https://user-images.githubusercontent.com/38278207/193119741-e894209e-b0fb-43fa-bd92-d8c591b98591.png">

comanda interessant per veure permissos:

```ls -la ```

Alternativa per posar permisos:

![image](https://user-images.githubusercontent.com/38278207/193120164-86008861-9be6-4b8b-9d75-3f5a0ba91d6c.png)


``` chmod 777 ``` 

Creació usuari Jaimito:

``` sudo useradd jaimito ```

``` passwd jaimito ```

## Pregunta 2: Investigar eina psacct

``` psacct ``` es una eina de codi obert que serveix per monitoritzar les activitats que tenen els usuaris sobre un sistema, entrades i surtides, activitat... ens permet obtenir info com:

- Monitoritzar les activitats de l'usuari.

- Desplega les ordres que es fan servir. 

- Desplega un informe sobre els recursos que s'utilitzen al sistema.

- Ens permet observar quant temps porten connectat els usuaris al sistema

- Acct i psacct no consumeix recursos de la màquina, llavors millorent el rendiment gracies al que ens donen

De manera que com a sysadmin o profes del grup, ens pot servir per saber "qui esta a classe" i quanta estona, des de quan esta connectat l'alumne, que ha fet, etc. En general, tenir un control absolut sobre la asistencia de l'alumnat

Links de interés utilitzats:

- https://www.solvetic.com/tutoriales/article/2940-monitorear-actividad-de-usuario-con-acct-o-psacct/

