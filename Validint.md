# Practica 5 -Validint

## ¿ Que hace?
- Valida todos los numeros o valores ingresados, es necesaria para la practica 6.

## Codigo
```bash
#!/bin/bash
# validint--Validates integer input, allowing negative integers too

validint()
{
# Validate first field and test that value against min value $2 and/or
# max value $3 if they are supplied. If the value isn't within range
# or it's not composed of just digits, fail.
 number="$1";      min="$2";      max="$3"

  if [ -z $number ] ; then
    echo "You didn't enter anything. Please enter a number." >&2 ; return 1
  fi

  if [ "${number%${number#?}}" = "-" ] ; then
    testvalue="${number#?}"
  else
    testvalue="$number"
  fi

  nodigits="$(echo $testvalue | sed 's/[[:digit:]]//g')"

  if [ ! -z $nodigits ] ; then
    echo "Invalid number format! Only digits, no commas, spaces, etc" >&2
    return 1
  fi

  if [ ! -z $min ] ; then
    if [ "$number" -lt "$min" ] ; then
      echo "$number is too small: smallest acceptable value is $min" >&2
      return 1
    fi
  fi
  if [ ! -z $max ] ; then
    if [ "$number" -gt "$max" ] ; then
      echo "Your value is too big: largest acceptable value is $max" >&2
      return 1
    fi
  fi
  return 0
}

if validint "$1" "$2" "$3" ; then
  echo "That input is a valid integer value within your constraints"
fi

```


