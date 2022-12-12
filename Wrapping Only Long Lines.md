# Código 22 - Wrapping Only Long Lines

## ¿Que hace?
- Utiliza un documento de texto en el cual se utilizan las primeras 72 lineas de archivo para que puedan ser interpretadas.

```bash
#!/bin/bash

width=72

if [ ! -r "$1" ] ; then
  echo "Cannot read file $1" >&2
  echo "Usage: $0 filename" >&2; exit 1
fi

while read input
do
   if [ ${#input} -gt $width ] ; then
     echo "$input" | fmt
   else
     echo "$input"
   fi
done < $1

exit 0

```
### Resultado del codigo con el documento de texto.
- - 
```bash
Aris@DESKTOP-CH8QNPE MINGW64 ~/Desktop/Codigos (main)
$ sh Working_with_the_Removed_File_Archive
/usr/bin/rm: missing operand
Try '/usr/bin/rm --help' for more information.

Aris@DESKTOP-CH8QNPE MINGW64 ~/Desktop/Codigos (main)
$ sh Wrapping_Only_Long_Lines example_code28.txt

Aris@DESKTOP-CH8QNPE MINGW64 ~/Desktop/Codigos (main)
$ sh Wrapping_Only_Long_Lines example_code28.txt
Hola
hola
ola
la
a
Hola
Bien
buenas
nosches
tardes
asjansdajsd
sjaksdas
sdjasda
asdjaksda
```



