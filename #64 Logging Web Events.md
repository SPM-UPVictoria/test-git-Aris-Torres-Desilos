# Codigo 64 - Logging Web Events

## ¿Que hace?
- Se genera un buscador que al ingresar una busqueda nos crea un archivo con el resultado.

## Descripcion
- Lo mas notable del script tiene que ver con como los servidores web y los clientes web donde se comunican.

## Codigo 1
```bash
#!/bin/bash
# log-duckduckgo-search--Given a search request, logs the pattern and then

#feeds the entire sequence to the real DuckDuckGo search system
# Make sure the directory path and file listed as logfile are writable by
#the user that the web server is running as.
logfile="/var/www/wicked/scripts/searchlog.txt"

if [ ! -f $logfile ] ; then
    touch $logfile
    chmod a+rw $logfile
fi

if [ -w $logfile ] ; then
    echo "$(date): X$QUERY_STRING" | sed 's/q=//g;s/+/ /g' >> $logfile
fi

echo "Location: https://duckduckgo.com/html/?$QUERY_STRING"
echo ""

exit 0
```

## Codigo 2
```bash
#!/bin/bash

logfile="/var/www/wicked/scripts/searchlog.txt"

if [ ! -f $logfile ] ; then
  touch $logfile
  chmod a+rw $logfile
fi

if [ -w $logfile ] ; then
  echo "$(date): $QUERY_STRING" | sed 's/q=//g;s/+/ /g' >> $logfile
fi

echo "Location: https://duckduckgo.com/html/?$QUERY_STRING"
echo ""

exit 0

```