# Codigo 66 - Turning Web Pages into Email Messages

## ¿Que hace?
- Envia un correo electronico hacia una pagina web

## Descripcion
- Lo que hace realmente es extraer informacion de una pagina web para usarla como base de una sub-invocacion posterior. Por lo tanto, el correo resultante incluye todo en la pagina.

## Codigo 1
```bash
#!/bin/bash

# getdope--Grabs the latest column of "The Straight Dope."
# Set it up in cron to be run every day, if so inclined.

now="$(date +%y%m%d)"
start="http://www.straightdope.com/ "
to="testing@yourdomain.com" # Change this as appropriate.

# First, get the URL of the current column.

URL="$(curl -s "$start" | \
grep -A1 'teaser' | sed -n '2p' | \
cut -d\" -f2 | cut -d\" -f1)"

# Now, armed with that data, produce the email.

( cat << EOF
Subject: The Straight Dope for $(date "+%A, %d %B, %Y")
From: Cecil Adams <dont@reply.com>
Content-type: text/html
To: $to

EOF

curl "$URL"
) | /usr/sbin/sendmail -t

exit 0
```

## Codigo 2
```bash 
#!/bin/bash
now="$(date +%y%m%d)"
start="http://www.straightdope.com/ "
to="correo_ejemplo@gmail.com"   

URL="$(curl -s "$start" | \ grep -A1 'teaser' | sed -n '2p' | \ cut -d\" -f2 | cut -d\" -f1)"

( cat << EOF
Subject: The Straight Dope for $(date "+%A, %d %B, %Y")
From: Cecil Adams <dont@reply.com>
Content-type: text/html
To: $to

EOF

curl "$URL"
) | /usr/sbin/sendmail -t

exit 0

```