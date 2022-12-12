# Codigo 91 - Creating Slide Shows from Cloud Photo Streams

## ¿Que hace?
- Abrira todas las imagenes que hayan en un directorio.

## Descripcion
- El script abre las imagenes de un directorio especificado que donde se tengan las imagense.

## Codigo 1
```bash
#!/bin/bash
# slideshow--Displays a slide show of photos from the specified directory.
#Uses ImageMagick's "display" utility.

Xdelay=2 # Default delay in seconds
psize="1200x900>" # Preferred image size for display

if [ $# -eq 0 ] ; then
    echo "Usage: $(basename $0) watch-directory" >&2
    exit 1
fi

watch="$1"

if [ ! -d "$watch" ] ; then
    echo "$(basename $0): Specified directory $watch isn't a directory." >&2
    exit 1
fi

cd "$watch"

if [ $? -ne 0 ] ; then
    echo "$(basename $0): Failed trying to cd into $watch" >&2
    exit 1
fi

suffixes="$(Yfile * | grep image | cut -d: -f1 | rev | cut -d. -f1 | \
rev | sort | uniq | sed 's/^/\*./')"

if [ -z "$suffixes" ] ; then
    echo "$(basename $0): No images to display in folder $watch" >&2
    exit 1
fi

/bin/echo -n "Displaying $(ls $suffixes | wc -l) images from $watch "
set -f ; echo "with suffixes $suffixes" ; set +f

display -loop 0 -delay $delay -resize $psize -backdrop $suffixes

exit 0
```

## Codigo 2
```bash
#!/bin/bash

delay=2
psize="1200x900>"	

if [ $# -eq 0 ] ; then
  echo "Usage: $(basename $0) watch-directory" >&2 ; exit 1
fi

watch="$1"

if [ ! -d "$watch" ] ; then
  echo "$(basename $0): specified watch directory $watch isn't a directory" >&2 ; exit 1
fi

cd "$watch"

if [ $? -ne 0 ] ; then
  echo "$(basename $0): failed trying to cd into $watch" >&2 ; exit 1
fi

suffixes="$(file * | grep image | cut -d: -f1 | rev | cut -d. -f1 | \
   rev | sort | uniq | sed 's/^/\*./')"

if [ -z "$suffixes" ] ; then
  echo "$(basename $0): no images to display in folder $watch" >&2 ; exit 1
fi

/bin/echo -n "Displaying $(ls $suffixes | wc -l) images from $watch "
set -f ; echo with suffixes $suffixes ; set +f

display -loop 0 -delay $delay -resize $psize -backdrop $suffixes

exit 0
```