# PAM
## @edt ASIX M06-ASO Curs 2018-2019

Repositori d'exemples de containers docker que utilitzen PAM

 * **hostpam:18base** exemple bàsic de host que usa pam, autentica contra el container (en construcio).

#### Execució

```
docker run --rm --name host -h host --net ldapnet -it francs2/hostpam:18base
```

#### Utilització

```
getnet passwd local01
getent passwd pau
getent passwd

getent group localgrp01
getent group profes 
getent group
```


