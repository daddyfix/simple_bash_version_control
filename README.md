# simple_bash_version_control
Increment a version number by date in Bash


```
#!/bin/bash

VER=some_version.txt

CURRENT_VERSION=$(< $VER)

# Set the current version as date format yy.mm.dd
TODAY="$(date "+%y.%m.%d")"

if [[ "$CURRENT_VERSION" == *"$TODAY"* ]]; then
    # get the number of chars in string
    if [[ ${#CURRENT_VERSION} -gt ${#TODAY} ]]; then 
        # get the date plus a letter
        curr=${CURRENT_VERSION:0:9}
        # trim last string
        letter=${curr:(-1)}
    else
        letter='a'
    fi
    # increment the alpha var by one    ie. m to n
    letter=$(echo "$letter" | tr "0-9a-z" "1-9a-z_")
    TODAY="${TODAY}${letter}"
fi

cat <<EOD
***********************************************************
Updating $VER file
from     $CURRENT_VERSION
to       $TODAY
***********************************************************
EOD
echo "$TODAY" > "${VER}"
```
