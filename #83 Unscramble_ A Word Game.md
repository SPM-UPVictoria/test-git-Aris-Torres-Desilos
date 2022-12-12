# Codigo 83 - Unscramble: A Word Game

## ¿Que hace?
- Es un juego de adivinanza que toma de un lista de palabra de un archivo de texto al azar, toma solo una y la desordena, y nuestro trabajo es adivinar que palabra es.

## Descripcion
- Este es un juego basico de anagramas. Su tarea es averiguar cual es la palabra original en el minimo numero de intentos.

## Codigo 1
```bash
#!/bin/bash
# unscramble--Picks a word, scrambles it, and asks the user to guess
#what the original word (or phrase) was
wordlib="$HOME/long-words.txt"

scrambleword()
{
    # Pick a word randomly from the wordlib and scramble it.
    #Original word is $match, and scrambled word is $scrambled.
    
    match="$(randomquote $wordlib)"
    
    echo "Picked out a word!"
    
    len=${#match}
    scrambled="";lastval=1
    
    for (( val=1; $val < $len ; ))
    do
        if [ $(($RANDOM % 2)) -eq 1 ] ; then
            scrambled=$scrambled$(echo $match | cut -c$val)
        else
            scrambled=$(echo $match | cut -c$val)$scrambled
        fi
        val=$(( $val + 1 ))
    done
}

if [ ! -r $wordlib ] ; then
    echo "$0: Missing word library $wordlib" >&2
    echo "(online: http://www.intuitive.com/wicked/examples/long-words.txt" >&2
    echo "save the file as $wordlib and you're ready to play!)" >&2
    exit 1
fi

newgame=""; guesses=0; correct=0; total=0

until [ "$guess" = "quit" ] ; do
    scrambleword
    echo ""
    echo "You need to unscramble: $scrambled"
    guess="??" ; guesses=0
    total=$(( $total + 1 ))
    [while [ "$guess" != "$match" -a "$guess" != "quit" -a "$guess" != "next" ]
    do
        echo ""
        /bin/echo -n "Your guess (quit|next) : "
        read guess
        if [ "$guess" = "$match" ] ; then
            guesses=$(( $guesses + 1 ))
            echo ""
            echo "*** You got it with tries = ${guesses}! Well done!! ***"
            echo ""
            correct=$(( $correct + 1 ))
        elif [ "$guess" = "next" -o "$guess" = "quit" ] ; then
            echo "The unscrambled word was \"$match\". Your tries: $guesses"
        else
            echo "Nope. That's not the unscrambled word. Try again."
            guesses=$(( $guesses + 1 ))
        fi
    done
done

echo "Done. You correctly figured out $correct out of $total scrambled words."

exit 0
```

## Codigo 2
```bash
#!/bin/bash

wordlib="$HOME/usa.txt"

scrambleword()
{
  match="$(randomquote $wordlib)"

  echo "Picked out a word!"

  len=$(echo $match | wc -c | sed 's/[^[:digit:]]//g')
  scrambled=""; lastval=1

  for (( val=1; $val < $len ; )) 
  do
    if [ $(($RANDOM % 2)) -eq 1 ] ; then
      scrambled=$scrambled$(echo $match | cut -c$val)
    else
      scrambled=$(echo $match | cut -c$val)$scrambled
    fi
    val=$(( $val + 1 ))
  done
}

if [ ! -r $wordlib ] ; then
  echo "$0: Missing word library $wordlib" >&2
  echo "(online: http://www.intuitive.com/wicked/examples/long-words.txt" >&2
  echo "save the file as $wordlib and you're ready to play!)" >&2
  exit 1
fi

newgame=""; guesses=0; correct=0; total=0 

until [ "$guess" = "quit" ] ; do

  scrambleword

  echo ""
  echo "You need to unscramble: $scrambled"

  guess="??" ; guesses=0
  total=$(( $total + 1 ))

  while [ "$guess" != "$match" -a "$guess" != "quit" -a "$guess" != "next" ] 
  do
    echo ""
    /bin/echo -n "Your guess (quit|next) : "
    read guess
 
    if [ "$guess" = "$match" ] ; then
      guesses=$(( $guesses + 1 ))
      echo ""
      echo "*** You got it with tries = ${guesses}!  Well done!! ***"  
      echo ""
      correct=$(( $correct + 1 ))
    elif [ "$guess" = "next" -o "$guess" = "quit" ] ; then
      echo "The unscrambled word was \"$match\". Your tries: $guesses"
    else
      echo "Nope. That's not the unscrambled word. Try again."
      guesses=$(( $guesses + 1 ))
    fi
  done
done

echo "Done. You correctly figured out $correct out of $total scrambled words."

exit 0
```