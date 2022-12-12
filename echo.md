# Practica 8- Sidestepping Poor echo Implementations

## ¿Que hace?
- Remplaza al echo y imprime lo que se ingrese autimaticamente.

```bash
#!/bin/bash
echo "$*" | awk '{ printf "%s", $0 }'
```