# PAM
## @edt ASIX M06-ASO Curs 2018-2019

Repositori d'exemples de containers docker que utilitzen PAM  samba i ldap

 * **hostpam:18samba** host pam amb authenticació ldap i tambe per autenticar y montar homes de samba. utilitza l'ordre authconfig per
configurar l'autenticació.


#### Execució

```
docker run --privileged --rm --name host -h host --net sambanet -it hostpam:18samba
```

#### Utilització

```
getnet passwd local01
getent passwd pau
getent passwd

getent group localgrp01
getent group [alumnes, profes]
getent group
```

Ordre per provar si va o no :
	* Amb un usuari ldap
	* su pere
	* mount -t cifs
