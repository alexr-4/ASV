# Preparant el Servidor

- Instanciar una MV amb nom middle-earth amb el SO base Rocky Linux. (1 CPU, 500MB de RAM, 8GB de disc).
- Actualitzeu totes les llibreries dnf update -y.
- Instal·leu un editor de text (vim o nano). dnf install vim -y.
- Instal·leu la shell tcsh. dnf install tcsh -y.
- Actualitzeu el hostname: hostnamectl set-hostname middlearth.asv01.udl.cat on XX és el vostre identificador.

## Primeres comandes 

nano /etc/motd
exit

cp /etc/issue.net /etc/issue.net.default
nano /etc/issue.net
exit

nano /etc/ssh/sshd_config
#Banner /etc/issue.net

![image](https://user-images.githubusercontent.com/79162978/193089032-788b7c58-1e0c-4c54-bd4e-bf79e2c9d75e.png)

systemctl restart sshd

## Creació de grups 

groupadd -g 600 hobbits
groupadd -g 700 elfs
groupadd -g 800 nans
groupadd -g 900 mags

## Afegir usuaris 
useradd frodo -g 600 -u 601 -c "Frodo" -m -d\
 /home/frodo
useradd gollum -g 600 -u 602 -c "Smeagol" -m -d\
 /home/smeagol
useradd samwise -g 600 -u 603 -c "Samwise" -m -d\
 /home/samwise
useradd legolas -g 700 -u 701 -c "Legolas" -m -d\
 /home/legolas
useradd gimli -g 800 -u 801 -c "Gimli" -m -d\
 /home/gimli
useradd gandalf -g 900 -u 901 -c "Gandalf" -m -d\
 /home/gandalf

## Canviar Pass usuaris 

passwd frodo
Tolkien2LOR

*fer per cada user*


## Afegir el root al grup mags
sudo usermod -a -G mags root

## Per veure que el root està al grup
root mags

## Per canviar el home del Gollum
usermod -d /home/smeagol gollum

## Perq el Legolas tingui per defecte la shell tcsh
usermod -s "/bin/tcsh" legolas

## Per eliminar la pass de gimli
passwd -d gimli

- Article d'interés: https://nebul4ck.wordpress.com/comandos-para-modificar-cuentas-de-usuarios-y-grupos/

## Per entrar com a Frodo
su frodo

## Per cambiar el home del frodo
cd home
cd frodo

## Per instalar mail
dnf -y install postfix
dnf -y install mailx

## Configurar fitxer
Editeu el fitxer /etc/postfix/main.cf:

myhostname = mail.middlearth.asv00.udl.cat
mydomain = udl.cat
myorigin = $mydomain
inet_interfaces = all
inet_protocols = ipv4
mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain
mynetworks = 127.0.0.0/8
home_mailbox = Maildir/

- Ficar això al final
#hide the kind or version of SMTP software
smtpd_banner = $myhostname ESMTP

#add follows to the end
#disable SMTP VRFY command
disable_vrfy_command = yes

#require HELO command to sender hosts
smtpd_helo_required = yes

#limit an email size
#example below means 10M bytes limit
message_size_limit = 10240000

#SMTP-Auth settings
smtpd_sasl_type = dovecot
smtpd_sasl_path = private/auth
smtpd_sasl_auth_enable = yes
smtpd_sasl_security_options = noanonymous
smtpd_sasl_local_domain = $myhostname
smtpd_recipient_restrictions = permit_mynetworks, permit_auth_destination,permit_sasl_authenticated, reject

## Configurar dimoni
Arrancar: systemctl enable --now postfix

Preparar bústies: echo 'export MAIL=$HOME/Maildir' >> /etc/profile.d/mail.sh

![image](https://user-images.githubusercontent.com/79162978/192591029-4f045e0a-0270-4f3d-8133-c3807a43d672.png)

## Afegir un nasgul
adduser nasgul

## Canviar contrasenya a Hawkings

![image](https://user-images.githubusercontent.com/79162978/192594844-137922d1-6c31-4178-b9cd-ee207d3fc226.png)

## Demanar que canvii la contrasenya en el proper inici 
sudo passwd --expire frodo

## Actualitzant l'equip

- Actualitzar username de legolas a glorfindel: *usermod -l glorfindel legolas*
- Actualitzar el UID de Gimli a 800: *usermod -u 800 gimli*
- L'usuari gandalf ha de poder invocar a l'usuari root: 
 Primer afegim a gandalf dintre del fitxer sudoers: nano /etc/sudoers
 Després fem su - gandalf. 
 I finalment, per poder invocar permisos de root, farem su root-c "_______"
 - Bloquejar el compte de glorfindel: passwd -l glorfindel
 
  ![image](https://user-images.githubusercontent.com/79162978/193078245-459a7f11-d2e4-4419-b206-af58e0997cbd.png)

## El poder de l'anell

- Crear el directori de l'anell: 

 ![image](https://user-images.githubusercontent.com/79162978/193081230-47fc18cb-0f1e-4c94-bcc0-f635820da901.png)

- Els fitxers d’aquest directori únicament podran ser executats/editats per l’usuari Frodo, la resta d’usuaris no ha de tenir cap permís ni de lectura, a excepció del grup d’usuari del grup portadors que han de poder llegir el directori.

- Agegim permisos de execució, lectura i escriptura: 
chmod u+x /home/anell
chmod u+r /home/anell
chmod u+w /home/anell

- Fem que el frodo sigui l'usuari que tingui aquests permissos. 
chown frodo /home/anell
ls -la /home/anell

 ![image](https://user-images.githubusercontent.com/79162978/193085935-e533c2c8-12aa-4c2f-8c85-bc8243f364e5.png)
 
- Creem el grup de portadors:
nano /etc/group
- Fem que el frodo junt amb els portadors tinguin accés al directori anell i treiem permisos al grup d'escriptura i d'execució: 

 ![image](https://user-images.githubusercontent.com/79162978/193087056-549b4268-45da-4f2c-9e9a-974158666630.png)

## Final del viatge

- Que no li aparegi al Gimli el missatge: 

 ![image](https://user-images.githubusercontent.com/79162978/193093093-1b16f210-0b9d-4eb6-8c2d-640acf333796.png)

- Article interés: https://www.cyberciti.biz/howto/turn-off-the-login-banner-in-linux-unix-with-hushlogin-file/

- Ens logem i no veiem cap missatge: 

 ![image](https://user-images.githubusercontent.com/79162978/193092926-2a96c5ef-b871-46b6-b952-82bbf34fcd59.png)

- Treure permisos del home al gimli: setfacl -x gimli /home/gimli

 ![image](https://user-images.githubusercontent.com/79162978/193094003-4c1342e3-2087-46a8-ad01-682b5dcc083e.png)

- Article interés: https://blog.alcancelibre.org/staticpages/index.php/uso-getfacl-getfacl

- Borrar a Samwise: userdel samwise

 ![image](https://user-images.githubusercontent.com/79162978/193094877-a169f97e-304f-4099-b870-94946e2682e8.png)

