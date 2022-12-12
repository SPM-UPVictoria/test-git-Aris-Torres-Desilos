# Codigo 31 -Making sftp Look More Like ftp

- hace que el comando sftp sea mas facil.

## Codigo
```bash
#!/bin/bash

/bin/echo -n "User account: "
read account

if [ -z $account ] ; then
  exit 0;
fi

if [ -z "$1" ] ; then
  /bin/echo -n "Remote host: "
  read host
  if [ -z $host ] ; then
    exit 0
  fi
else
  host=$1
fi
exec sftp -C $account@$host

```

## Resultado
- se puede ver que en la primera vez que se ejecto no paso nada ya que son los datos verdaderos
- y en la segunda demostracion se colocaron datos erroneos.
```bash
Aris@DESKTOP-CH8QNPE MINGW64 ~/Desktop/Codigos (main)
$ sh Making_sftp_Look_More_Like_ftp
User account: Aris
Remote host:

Aris@DESKTOP-CH8QNPE MINGW64 ~/Desktop/Codigos (main)
$ sh Making_sftp_Look_More_Like_ftp
User account: Uriel
Remote host: 45879
ssh: connect to host 0.0.179.55 port 22: Network is unreachable
Connection closed
```