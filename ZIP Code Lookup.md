# Codigo 56 - ZIP Code Lookup
## ¿Que hace?
- Genera un documento.db que contiene la mayoria de documentos de tu computador 

```bash
#!/bin/bash
baseURL="http://www.city-data.com/zips"

/bin/echo -n "ZIP code $1 is in "

curl -s -dump "$baseURL/$1.html" | \
   grep -i '<title>' | \
   cut -d\( -f2 | cut -d\) -f1

exit 0
```