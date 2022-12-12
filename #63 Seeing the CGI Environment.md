# Codigo 63 - Seeing the CGI Environment

## ¿Que hace?
- Imprime un codigo de html

## Descripcion
- Para ejecutar el codigo se necesita tener el ejecutable del script ubicado en tu directorio.

## Codigo 1
```bash
#!/bin/bash
# showCGIenv--Displays the CGI runtime environment, as given to any
#
 CGI script on this system
echo "Content-type: text/html"
echo ""
# Now the real information...
echo "<html><body bgcolor=\"white\"><h2>CGI Runtime Environment</h2>"
echo "<pre>"
X env || printenv
echo "</pre>"
echo "<h3>Input stream is:</h3>"
echo "<pre>"
cat -
echo "(end of input stream)</pre></body></html>"
exit 0
```

## Codigo 2

```bash
#!/bin/bash

echo "Content-type: text/html"
echo ""

echo "<html><body bgcolor=\"white\"><h2>CGI Runtime Environment</h2>"
echo "<pre>"
env || printenv
echo "</pre>"
echo "<h3>Input stream is:</h3>"
echo "<pre>"
cat -
echo "(end of input stream)</pre></body></html>"

exit 0

```