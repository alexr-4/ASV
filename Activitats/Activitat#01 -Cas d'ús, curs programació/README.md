# ACTIVITAT 01 - CURS DE PROGRAMACIÓ

## Pregunta 1: Configurar servidor

Hem creat una maquina nova anomenada: curs-coding-asv01-server:

<img width="1436" alt="Captura de Pantalla 2022-09-29 a las 20 44 32" src="https://user-images.githubusercontent.com/38278207/193116431-20bca797-a7f1-4696-866a-4b3df97f26a3.png">

Creació usuari admin. password: adminadmin.

<img width="1017" alt="Captura de Pantalla 2022-09-29 a las 20 49 47" src="https://user-images.githubusercontent.com/38278207/193117424-40391aaf-e53e-4b99-9fbf-22ff2472cdb6.png">

Li donem permissos de superusuari dins del ``` sudo visudo ```:

<img width="1017" alt="Captura de Pantalla 2022-09-29 a las 20 50 43" src="https://user-images.githubusercontent.com/38278207/193117725-fa9bcf3f-8966-4077-b069-0236fea589e8.png">

Creem grups alumne i professorat:

<img width="527" alt="Captura de Pantalla 2022-09-29 a las 20 54 58" src="https://user-images.githubusercontent.com/38278207/193118418-94762ea7-b545-4ffc-b4c1-a762d2e55d09.png">


Donar permisos máxims al directori /home/alumne/

Hem fet que el propietari del directori alumne sigui el grup professorat, de manera que aquest grup ja tindra permissos: 

<img width="1017" alt="Captura de Pantalla 2022-09-29 a las 21 01 53" src="https://user-images.githubusercontent.com/38278207/193119741-e894209e-b0fb-43fa-bd92-d8c591b98591.png">

comanda interessant per veure permissos:

```ls -la ``

Alternativa per posar permisos:

https://www.google.com/url?sa=i&url=https%3A%2F%2Fayudalinux.com%2Fcomando-chmod-que-es-como-usarlo%2F&psig=AOvVaw1CQ35sXc2niHGzGTxN-Mhb&ust=1664564643269000&source=images&cd=vfe&ved=0CAwQjRxqFwoTCOjOqNTYuvoCFQAAAAAdAAAAABAD![image](https://user-images.githubusercontent.com/38278207/193120164-86008861-9be6-4b8b-9d75-3f5a0ba91d6c.png)


``` chmod 777 ``` 


## Pregunta 2: Investigar eina psactt
