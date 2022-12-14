# Codigo 90 - Syncing Dropbox

## ¿Que hace?
- Se sincroniza **Dropbox**, mueve un archivo y abre **Dropbox**

## Descripcion
- Este script ofrece una manera facil de copiar un directorio lleno de archivo o un conjunto especifico de archivos en el universo de **Dropbox**.

## Codigo 1
```bash
#!/bin/bash
# syncdropbox--Synchronize a set of files or a specified folder with Dropbox.
# This is accomplished by copying the folder into ~/Dropbox or the set of
# files into the sync folder in Dropbox and then launching Dropbox.app
# as needed.

name="syncdropbox"
dropbox="$HOME/Dropbox"
sourcedir=""
targetdir="sync" # Target folder on Dropbox for individual files

# Check starting arguments.
if [ $# -eq 0 ] ; then
    echo "Usage: $0 [-d source-folder] {file, file, file}" >&2
    exit 1
fi

if [ "$1" = "-d" ] ; then
    sourcedir="$2"
    shift; shift
fi

# Validity checks
if [ ! -z "$sourcedir" -a $# -ne 0 ] ; then
    echo "$name: You can't specify both a directory and specific files." >&2
    exit 1
    fi
if [ ! -z "$sourcedir" ] ; then
    if [ ! -d "$sourcedir" ] ; then
        echo "$name: Please specify a source directory with -d." >&2
        exit 1
    fi  
fi

#######################
#### MAIN BLOCK #######
#######################

if [ ! -z "$sourcedir" ] ; then
    if [ -f "$dropbox/$sourcedir" -o -d "$dropbox/$sourcedir" ] ; then
        echo "$name: Specified source directory $sourcedir already exists." >&2
        exit 1
    fi
    echo "Copying contents of $sourcedir to $dropbox..."
    # -a does a recursive copy, preserving owner info, etc.
    cp -a "$sourcedir" $dropbox
else
    # No source directory, so we've been given individual files.
    if [ ! -d "$dropbox/$targetdir" ] ; then
        mkdir "$dropbox/$targetdir"
        if [ $? -ne 0 ] ; then
            echo "$name: Error encountered during mkdir $dropbox/$targetdir." >&2
            exit 1
        fi
    fi

# Ready! Let's copy the specified files.

    cp -p -v "$@" "$dropbox/$targetdir"
fi

# Now let's launch the Dropbox app to let it do the actual sync, if needed.

exec startdropbox -s
```

## Codigo 2
```bash
#!/bin/bash

name="syncdropbox"
dropbox="$HOME/Dropbox"
sourcedir=""
targetdir="sync"

if [ $# -eq 0 ] ; then
  echo "Usage: $0 [-d source-folder] {file, file, file}" >&2 ; exit 1
fi 

if [ "$1" = "-d" ] ; then
  sourcedir="$2"
  shift; shift
fi

if [ ! -z "$sourcedir" -a $# -ne 0 ] ; then
  echo "$name: you can't specify both a directory and specific files." >&2 ; exit 1
fi

if [ ! -z "$sourcedir" ] ; then
  if [ ! -d "$sourcedir" ] ; then
    echo "$name: please specify a source directory with -d" >&2 ; exit 1
  fi
fi

if [ ! -z "$sourcedir" ] ; then
 if [ -f "$dropbox/$sourcedir" -o -d "$dropbox/$sourcedir" ] ; then
    echo "$name: specified source directory $sourcedir already exists in $dropbox" >&2 ; exit 1
  fi

  echo "Copying contents of $sourcedir to $dropbox..."
  cp -a "$sourcedir" $dropbox	
else
  if [ ! -d "$dropbox/$targetdir" ] ; then
    mkdir "$dropbox/$targetdir"
    if [ $? -ne 0 ] ; then
      echo "$name: Error encountered during mkdir $dropbox/$targetdir" >&2 ; exit 1
    fi
  fi

 cp -p -v $@ "$dropbox/$targetdir"
fi

exec ./startDropbox89.sh "Dropbox.com"
```