# PAM
## @edt ASIX M06-ASO Curs 2018-2019

Repositori d'exemples de containers docker que utilitzen PAM

 * **hostpam:18auth** host pam amb authenticació ldap. utilitza l'ordre authconfig per
configurar l'autenticació.

#### Execució

```
docker run --rm --name host -h host --net ldapnet -it francs2/hostpam:18auth
```

#### Utilització

```
getnet passwd local01
getent passwd pau
getent passwd

getent group localgrp01
getent group alumnes
getent group
```
