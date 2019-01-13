# pam

## @edt ASIX M06 2018-2019


Podeu trobar les imatges docker al Dockehub de ...

ASIX M06-ASO Escola del treball de barcelona

### Imatges:

* **hostpam:18base** host pam que autentica els usuaris contra ldap. Usar el container *ldapserver:18group*.

* **hostpam:18auth** host pam amb authenticació ldap. utilitza l'ordre authconfig per configurar l'autenticació.

* **hostpam:18samba** host pam amb authenticació ldap. utilitza per montar els homes del usuaris ldap amb samba.

* **hostpam:18ssh** host pam amb authenticació ldap. utilitza per montar els homes i conectarse als usuaris ldap amb ssh .

* **hostpam:18ldapsamba** host pam amb authenticació ldap. utilitza per montar els homes del usuaris ldap amb samba amb els backend **ldapsam**.

#### Execució

```
$docker run --rm --name host -h host --net ldapnet -it francs2/hostpam:18base 
```

```
$ docker run --rm --privileged --name host -h host --network sambanet -it francs2/hostpam:18samba
```

```
$ docker run --rm --privileged --name host -h host --network ldapnet -it francs2/hostpam:18ssh
```

```
$ docker run --rm --privileged --name host -h host --network sambanet -it francs2/hostpam:18ldapsamba
```


