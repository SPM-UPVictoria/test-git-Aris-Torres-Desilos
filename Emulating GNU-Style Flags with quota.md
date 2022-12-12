# Codigo 30 - Emulating GNU-Style Flags with quota

- El comando quota muestra nuevas flags}

### Codigo
```bash
#!/bin/bash
flags=""
realquota="$(which quota)"
while [ $# -gt 0 ]
do
  case $1
  in
    --help)  echo "Usage: $0 [--group --verbose --quiet -gvq]" >&2
                       exit 1 ;;
    --group )  flags="$flags -g";       shift ;;
    --verbose)  flags="$flags -v";   shift ;;
    --quiet)  flags="$flags -q";       shift ;;
    --)  shift;           break ;;
    *)  break;
  esac
done
exec $realquota $flags "$@"
```
## Ejecucion y salida.

```
Aris@DESKTOP-CH8QNPE MINGW64 ~/Desktop/Codigos (main)
$ nano Emulating_GNU-Style_Flags_with_quota

Aris@DESKTOP-CH8QNPE MINGW64 ~/Desktop/Codigos (main)
$ sh Emulating_GNU-Style_Flags_with_quota
which: no quota in (/c/Users/Aris/bin:/mingw64/bin:/usr/local/bin:/usr/bin:/bin:/mingw64/bin:/usr/bin:/c/Users/Aris/bin:/c/Program Files/Google/Chrome/Application:/c/Windows/system32:/c/Windows:/c/Windows/System32/Wbem:/c/Windows/System32/WindowsPowerShell/v1.0:/c/Windows/System32/OpenSSH:/c/Users/Aris/AppData/Local/Microsoft/WindowsApps:/usr/bin/vendor_perl:/usr/bin/core_perl)

```