---
title: Toggleable Script
permalink: "/guides/toggle-script/"
---

## The template
```lua
FLAG = not FLAG --global
if not FLAG then
  return  --was turned off, exit script
end

log"&bMy awesome script: &a&BENABLED" --&b blue &a green &B BOLD
while FLAG do
  --do stuff here
  waitTick() --checking something? once a tick is good
end
log"bMy awesome script: &c&BDISABLED" --&c red
```

## What???

`FLAG` (rename this to something related to your script)<br>
this is a boolean (true/false) used to indicate if your script should keep running<br>
<br>
When the script starts `FLAG` is `nil`
```lua
log( not nil ) -- true
log( not true ) -- false
log( not false ) -- true
```
Each time the script runs, the `FLAG` is changed.<br>
When the script is turned on, it skips the `if` statment and does the stuff in the `while` loop until the next time the script is run<br>
<br>
When the script is running and it's called again, there's now two of them running at the same time. <br>
Without the `if` statment, you'd see both the `ENABLED` and `DISABLED` messages show up from the one that toggled the script off (skipping the while loop)<br>
When the first one finishes in the while loop, that one still logs the `DISABLED` message

## VS Code Snippet
Using VS Code?
`File` → `Preferences` → `Configure User Snippets` → `lua.json`
```json
"Toggle Script": {
	"prefix": ["toggle"],
	"body":[
        "$TM_FILENAME_BASE = not $TM_FILENAME_BASE",
        "if not $TM_FILENAME_BASE then return end",
        "",
        "log\"&b$TM_FILENAME_BASE&f: &a&BENABLED\"",
        "while $TM_FILENAME_BASE do",
        "  $0",
        "  waitTick()",
        "end",
        "",
        "log\"&b$TM_FILENAME_BASE&f: &c&BDISABLED\""
    ]
}
```
