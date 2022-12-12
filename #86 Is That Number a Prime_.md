# Codigo 86 - Is That Number a Prime?

## ¿Que hace?
- Imprime que si es un numero primo o no lo es.

## Descripcion
- Los numeros primos son numeros que solo son divisibles por si mismo. Lo que hace el script es reconocer los numeros primos y existen diferentes enforques matematicos para determinar si un numero es primo.

## Codigo 1
```bash
#!/bin/bash

# isprime--Given a number, ascertain whether it's a prime. This uses what's
#known as trial division: simply check whether any number from 2 to (n/2)
#divides into the number without a remainder.

counter=2
remainder=1

if [ $# -eq 0 ] ; then
    echo "Usage: isprime NUMBER" >&2
    exit 1
fi

number=$1

# 3 and 2 are primes, 1 is not.

if [ $number -lt 2 ] ; then
    echo "No, $number is not a prime"
    exit 0
fi

# Now let's run some calculations.
while [ $counter -le $(expr $number / 2) -a $remainder -ne 0 ]
do
    remainder=$(expr $number % $counter) # '/' is divide, '%' is remainder
    # echo " for counter $counter, remainder = $remainder"
    counter=$(expr $counter + 1)
done

if [ $remainder -eq 0 ] ; then
    echo "No, $number is not a prime"
else
    echo "Yes, $number is a prime"
fi

exit 0
```

## Codigo 2
```bash
#!/bin/bash

  counter=2
remainder=1

if [ $# -eq 0 ] ; then
  echo "Usage: isprime NUMBER" >&2
  exit 1
fi

number=$1

if [ $number -lt 2 ] ; then
  echo "No, $number is not a prime" ; exit 0
fi

while [ $counter -le $(expr $number / 2) -a $remainder -ne 0 ]
do
  remainder=$(expr $number % $counter)
  counter=$(expr $counter + 1)
done

if [ $remainder -eq 0 ] ; then
  echo "No, $number is not a prime"
else
  echo "Yes, $number is a prime"
fi
exit 0
```