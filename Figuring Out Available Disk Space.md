# Codigo 38- Figuring Out Available Disk Space

## ¿Que hace?
- Muestra el espacio total de equipo que se esta utilizando por el momento.

## Codigo.
```bash
#!/bin/bash
tempfile="/tmp/available.$$"

trap "rm -f $tempfile" EXIT

cat << 'EOF' > $tempfile
    { sum += $4 }
END { mb = sum / 1024
      gb = mb / 1024
      printf "%.0f MB (%.2fGB) of available disk space\n", mb, gb
    }
EOF

df -k | awk -f $tempfile
exit 0

```
## Salida.
```
Aris@DESKTOP-CH8QNPE MINGW64 ~/Desktop/Codigos (main)
$ sh Figuring_Out_Available_Disk_Space
54533 MB (53.26GB) of available disk space
```
