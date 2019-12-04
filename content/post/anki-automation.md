+++
description = ""
keywords = [
]
categories = [
]
date = "2019-10-29T11:37:59+03:30"
title = "Anki automation"

+++

I wrote following script, to automate adding new card to my Anki decks. When I encounter new word or phrase, I select that word and press *Ctrl+i* to enter it into the Anki deck. befor anythin, you should install *Anki Connect* plugin.

```bash
#!/bin/bash
clipboard="$(xclip -out -selection)"
echo "$clipboard"
clipboard="$(jshon -s "$clipboard" | sed  's/\\n/<br>/g')"
echo $clipboard
#echo "$clipboard"
#clipboard=$(jq -aR . <<< $clipboard)

data='{
  "action": "addNote",
  "version": 6,
  "params": {
      "note": {
          "deckName": "default",
          "modelName": "Basic",
          "fields": {
              "Front": '"$clipboard"',
              "Back": ""
          },
          "options": {
              "allowDuplicate": false
          },
          "tags": [
              "api"
          ]
      }
  }
}'

resp=$(curl -X POST \
  http://localhost:8765/ \
  -H 'content-type: application/json' \
  -d "$data")

r=$(jq '.error' <<< "$resp")

if [ "$r" == "null" ]; then
      notify-send "Success" "${clipboard} is added"
      paplay /usr/share/sounds/freedesktop/stereo/complete.oga
else
      notify-send "Failed" "adding ${clipboard} failed"
      paplay /usr/share/sounds/freedesktop/stereo/dialog-error.oga
fi
```

Add shortcut for above script:

![Keyboard Shortcut](/img/keyboard.png)
