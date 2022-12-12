# Practica 19 - Locating Files by Filename.

## ¿Que hace?
- Esta practica esta conformada por dos codigos el primero es el que contiene los documentos de tu ordenador, y la segunda parte es la que permirte buscar los documentos con ciertos caracteres.

### Codigo 1
```bash
#!/bin/bash

locatedb="/var/tmp/locate_19.db"

if [ "$(whoami)" != "haydo" ] ; then
  echo "Must be root to run this command." >&2
  exit 1
fi

find / -print > $locatedb

exit 0
```

### Codigo 2
```bash
#!/bin/sh

locatedb="/tmp/locate.db"

exec grep -i "$@" $locatedb

```