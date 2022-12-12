# Codigo 81 - Producing Summary Listings of iTunes Libraries

## ¿Que hace?
- Imprime las librerias de la carpeta de Itunes que hay en el equipo.

## Descripcion
- Este script se basa en la funcion de compartir Itunes, el cual esta habilitado, asi que antes de ejecutar este script, se debe de asegurarse de que este activado en las preferencias de Itunes.

## Codigo 1
```bash
#!/bin/bash

# ituneslist--Lists your iTunes library in a succinct and attractive
#manner, suitable for sharing with others, or for synchronizing
#(with diff) iTunes libraries on different computers and laptops

itunehome="$HOME/Music/iTunes"
ituneconfig="$itunehome/iTunes Music Library.xml"

musiclib="/$(grep '>Music Folder<' "$ituneconfig" | cut -d/ -f5- | \
cut -d\< -f1 | sed 's/%20/ /g')"

echo "Your library is at $musiclib"

if [ ! -d "$musiclib" ] ; then
    echo "$0: Confused: Music library $musiclib isn't a directory?" >&2
    exit 1
fi

exec find "$musiclib" -type d -mindepth 2 -maxdepth 2 \! -name '.*' -print \
| sed "s|$musiclib/||"
```

## Codigo 2
```bash
#!/bin/bash

itunehome="$HOME/Music/iTunes"
ituneconfig="$itunehome/iTunes Music Library.xml"

musiclib="/$(grep '>Music Folder<' "$ituneconfig" | cut -d/ -f5- | \
   cut -d\< -f1 | sed 's/%20/ /g')"

echo "Your library is at $musiclib"

if [ ! -d "$musiclib" ] ; then
  echo "$0: Confused: Music library $musiclib isn't a directory?" >&2
  exit 1
fi

exec find "$musiclib" -type d -mindepth 2 -maxdepth 2 \! -name '.*' -print |
   sed "s|$musiclib/||"
```