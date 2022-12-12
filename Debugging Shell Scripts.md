# Practica 13 - Debugging Shell Scripts
## ¿Que hace?
- Este es un juego, el cual debes de adivinar un numero random ya sea mas grande o mas pequeño del que la persona puso.

```bash

#!/bin/bash
biggest=100
guess=0
guesses=0
number=$(( $RANDOM % $biggest + 1 ))
echo "Guess a number between 1 and $biggest"

while [ "$guess" -ne $number ] ; do
  /bin/echo -n "Guess? " ; read guess
  if [ "$guess" -lt $number ] ; then
    echo "... bigger!"
  elif [ "$guess" -gt $number ] ; then
    echo "... smaller!"
  fi
  guesses=$(( $guesses + 1 ))
done

echo "Right!! Guessed $number in $guesses guesses."

exit 0



```
# Ejemplo de ejecución.
```bash
Aris@DESKTOP-CH8QNPE MINGW64 ~/Desktop/Codigos (main)
$ sh Debugging_Shell_Scripts
Guess a number between 1 and 100
Guess? 50
... smaller!
Guess? 20
... smaller!
Guess? 8
... smaller!
Guess? 80
... smaller!
Guess? 90
... smaller!
Guess? 10
... smaller!
Guess? 5
... smaller!
Guess? 100
... smaller!
Guess? 1
... bigger!
Guess? 2
... bigger!
Guess? 6
... smaller!
Guess? 3
... bigger!
Guess? 4
Right!! Guessed 4 in 13 guesses.
```

