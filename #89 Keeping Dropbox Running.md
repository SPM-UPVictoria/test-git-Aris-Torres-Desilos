# Codigo 89 - Keeping Dropbox Running

## ¿Que hace?
- Abre la pagina de **Dropbox**

## Descripcion
- Dropbox es uno de varios sistemas utiles de almacenamiento en la nube y es particularmente popular entre las personas que usan variedad de dispositivos.

## Codigo 1
```bash
#!/bin/bash
# startdropbox--Makes sure Dropbox is running on OS X

app="Dropbox.app"
verbose=1

running="$(Xps aux | grep -i $app | grep -v grep)"

if [ "$1" = "-s" ] ; then
    verbose=0
fi

# -s is for silent mode.

if [ ! -z "$running" ] ; then
    if [ $verbose -eq 1 ] ; then
    echo "$app is running with PID $(echo $running | cut -d\ -f2)"
    fi
else
    if [ $verbose -eq 1 ] ; then
        echo "Launching $app"
    fi
    open -a $app
fi

exit 0
```

## Codigo 2
```bash
#!/bin/bash

app="Dropbox.com"
verbose=1

running="$(ps aux | grep -i $app | grep -v grep)"

if [ "$1" = "-s" ] ; then
  verbose=0
fi

if [ ! -z "$running" ] ; then
  if [ $verbose -eq 1 ] ; then
    echo "$app is running with PID $(echo $running | cut -d\  -f2)"
  fi
else
  if [ $verbose -eq 1 ] ; then
    echo "Launching $app"
  fi
  xdg-open $app
fi

exit 0
```