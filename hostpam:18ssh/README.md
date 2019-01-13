# PAM
## @edt ASIX M06-ASO Curs 2018-2019

Repositori d'exemples de containers docker que utilitzen sshclient

 * **hostpam:18ssh** host pam amb authenticació ldap. utilitzat per provar ssh com a client.

#### Execució

```
docker run --privileged --rm --name host -h host --net ldapnet -it francs2/hostpam:18ssh
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
ssh 

```
[root@host docker]# ssh pere@172.18.0.3 -p 1022

[root@host docker]# ssh marta@172.18.0.3 -p 1022

[root@host docker]# ssh pau@172.18.0.3 -p 1022
pau@172.18.0.3's password: 
Last login: Fri Jan 11 08:33:24 2019 from 172.18.0.1
[pau@sshd ~]$ pwd
/tmp/home/pau
```

