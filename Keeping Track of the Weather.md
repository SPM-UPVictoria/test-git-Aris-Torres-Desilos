# Codigo 58 - Keeping Track of the Weather
## ¿Que hace?
- Da un seguimiento del clima para saber como esta el dia.
- no manda lo que deberia de mandar.

```bash

#!/bin/bash
if [ $# -ne 1 ]; then
  echo "Usage: $0 <zipcode>"
  exit 1
fi

apikey="b0304b43b2e7cd23" 

weather=`curl -s \
    "https://api.wunderground.com/api/$apikey/conditions/q/$1.xml"`
state=`xmllint --xpath \
     //response/current_observation/display_location/full/text\(\) \
     <(echo $weather)`
zip=`xmllint --xpath \
     //response/current_observation/display_location/zip/text\(\) \
     <(echo $weather)`
current=`xmllint --xpath \
     //response/current_observation/temp_f/text\(\) \
     <(echo $weather)`
condition=`xmllint --xpath \
     //response/current_observation/weather/text\(\) \
     <(echo $weather)`

echo $state" ("$zip") : Current temp "$current"F and "$condition" outside." 
```
```
Aris@DESKTOP-CH8QNPE MINGW64 ~/Desktop/Codigos (main)
$ sh Keeping\ Track\ of\ the\ Weather 10010
warning: failed to load external entity "/proc/2934/fd/63"
warning: failed to load external entity "/proc/2936/fd/63"
warning: failed to load external entity "/proc/2938/fd/63"
warning: failed to load external entity "/proc/2940/fd/63"
```