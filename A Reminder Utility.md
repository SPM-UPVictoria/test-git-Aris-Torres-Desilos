# Codigo 22 - A Reminder Utility

- Esta practica contiene dos codigos necesarios, el primero geera recordatorios en forma de lista y el segundo codigo permite mostrar la lista.

### Codigo 1
```bash
#!/bin/bash
rememberfile="$USER/.remember"

if [ $# -eq 0 ] ; then
  echo "Enter note, end with ^D: "
  cat - >> $rememberfile
else
  echo "$@" >> $rememberfile
fi

exit 0

```
### Codigo 2
```bash
#!/bin/bash

rememberfile="$USER/.remember"

if [ ! -f $rememberfile ] ; then
  echo "$0: You don't seem to have a .remember file." >&2
  echo "To remedy this, please use 'remember' to add reminders" >&2
  exit 1
fi

if [ $# -eq 0 ] ; then
  more $rememberfile
else
  grep -i -- "$@" $rememberfile | ${PAGER:-more}
fi

exit 0

```