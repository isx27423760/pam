# Practica samba server
## @edt ASIX M06 Franlin C. 20/12/2018

Creacio de un servidor samba que es conecta a un servidor ldap , i que a mes funciona com a servidor per
que altres host fora del server local , puguin montar un homes tant de usuaris locals de el servidor com de 
els usuaris del ldap. Usa el backend ldapsam 
Es dira samba:18homes

### Reposistoris utilitzats:
* Totes aquestes imatges estan totes juntas en una xarxa propia creat amb dokcer .

       **$docker create network sambanet** 

* **samba:18ldapsamba** : Servidor SAMBA amb usuaris locals i usuaris LDAP unix, es crearan usuaris locals i alguns usuaris de LDAP
amb backend ldapsam.

* **hostpam:18samba** :  Farem servir la base de un que ja tenia, aquest contenidor funcionar com host fora del servei samba i ldap , llavors verificarem que pot fer mount dels usuaris locals del servei samba i dels usuaris ldap. El archiu clau de mudificaio es el **pam_mount.conf.xml** , pero abans tenin que instalar el paquet **cifs-utils**.

### Configuracio del hostpam:18ldapsamba

* Configurem clau del hostpam:  **pam_mount.conf.xml**

```
    <volume user="*" fstype="cifs" server="samba" path="%(USER)"  mountpoint="~/%(USER)" />

```


#### Execució dels tres containers que necesitarem

* **SERVER LDAPSAM: ldapserver:18samba**

```
    $ docker run --rm --name ldap -h ldap --network sambanet -it francs2/ldapserver:18samba

```

* **SERVER SAMBA: samba:18ldapsamba**

```
    $ docker run --rm --privileged --name samba -h samba --network sambanet -it francs2/samba:18ldapsamba

```

* **HOST PAM : hostpam:18samba**

```
    $ docker run --rm --privileged --name host -h host --network sambanet -it francs2/hostpam:18ldapsamba

```

#### Comprovar que funciona desde el hostpam:samba :

	```
[root@host docker]# smbtree -L
MYGROUP
	\\SAMBA          		Samba Server Version 4.7.10
		\\SAMBA\IPC$           	IPC Service (Samba Server Version 4.7.10)
		\\SAMBA\public         	Public Stuff


[root@host docker]# su - local02
[local02@host ~]$ pwd
/home/local02


[local02@host ~]$ su - pere
pam_mount password:
[pere@host ~]$ ll
total 0
drwxr-xr-x 2 pere users 0 Jan 12 19:25 pere
[pere@host ~]$ mount -t cifs
//samba/pere on /tmp/home/pere/pere type cifs (rw,relatime,vers=default,cache=strict,username=pere,domain=,uid=5001,forceuid,gid=100,forcegid,addr=172.19.0.3,file_mode=0755,dir_mode=0755,soft,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,echo_interval=60,actimeo=1)


[root@host docker]# smbclient //SAMBA/public -U pere%pere
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Sat Jan 12 19:25:02 2019
  ..                                  D        0  Sat Jan 12 19:25:47 2019
  INFO.txt                            N       54  Sat Jan 12 19:25:02 2019
  Dockerfile                          N      469  Sat Jan 12 19:25:02 2019
  smbldap_bind.conf                   N      430  Sat Jan 12 19:25:02 2019
  startup.sh                          A      305  Sat Jan 12 19:25:02 2019
  smb.conf                            N      867  Sat Jan 12 19:25:02 2019
  nsswitch.conf                       N     1731  Sat Jan 12 19:25:02 2019
  populate.ldif                       N    19046  Sat Jan 12 19:25:02 2019
  ldap.conf                           N      311  Sat Jan 12 19:25:02 2019
  nslcd.conf                          N     4831  Sat Jan 12 19:25:02 2019
  install.sh                          A     2612  Sat Jan 12 19:25:02 2019
  smbldap.conf                        N     7803  Sat Jan 12 19:25:02 2019
  README.md                           N     9738  Sat Jan 12 19:25:02 2019

		656411128 blocks of size 1024. 591143560 blocks available
smb: \> 	
	```



