# Preparant el Servidor

Instanciar una MV amb nom middle-earth amb el SO base Rocky Linux. (1 CPU, 500MB de RAM, 8GB de disc).
Actualitzeu totes les llibreries dnf update -y.
Instal·leu un editor de text (vim o nano). dnf install vim -y.
Instal·leu la shell tcsh. dnf install tcsh -y.
Actualitzeu el hostname: hostnamectl set-hostname middlearth.asv01.udl.cat on XX és el vostre identificador.

## Primeres comandes 

nano /etc/motd
exit

cp /etc/issue.net /etc/issue.net.default
nano /etc/issue.net
exit

nano /etc/ssh/sshd_config
#Banner /etc/issue.net
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

## Canviar Pass usuaris: 

passwd frodo
Tolkien2LOR

*fer per cada user*


## Afegir el root al grup mags:
sudo usermod -a -G mags root

## Per veure que el root està al grup:
root mags

## Per canviar el home del Gollum:
usermod -d /home/smeagol gollum

## Perq el Legolas tingui per defecte la shell tcsh:
usermod -s "/bin/tcsh" legolas

## Per eliminar la pass de gimli:
passwd -d gimli

- Article d'interés: https://nebul4ck.wordpress.com/comandos-para-modificar-cuentas-de-usuarios-y-grupos/

## Per entrar com a Frodo:
su frodo

## Per cambiar el home del frodo:
cd home
cd frodo

## Per instalar mail:
dnf -y install postfix
dnf -y install mailx

## Configurar fitxer:
Editeu el fitxer /etc/postfix/main.cf:

myhostname = mail.middlearth.asv00.udl.cat
mydomain = udl.cat
myorigin = $mydomain
inet_interfaces = all
inet_protocols = ipv4
mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain
mynetworks = 127.0.0.0/8
home_mailbox = Maildir/

Ficar això al final:
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

## Configurar dimoni:
Arrancar: systemctl enable --now postfix
Preparar bústies: echo 'export MAIL=$HOME/Maildir' >> /etc/profile.d/mail.sh

![image](https://user-images.githubusercontent.com/79162978/192591029-4f045e0a-0270-4f3d-8133-c3807a43d672.png)

