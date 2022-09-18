---
title: Troubleshooting
permalink: /docs/troubleshooting/
---
## Installation issues
### Crash on startup
If there's an issue with the installation and you've coppied your mods+config from somewhere else:<br>
Check that the config still points to a valid path.
<br>

### Other
Ask on discord<br>
I'll add more here as questions are asked.

## Scripts
General debugging flow chart
1. Find some relevant code
2. Make a prediction about what something should be
3. inspect it, if wrong why? back track to see where something went wrong. [repeat]
4. success or ask for #help on discord

### Common mistakes

#### Event scripts
When testing a script that is triggered by an event. Don't click `run` from the ingame editor.<br>
Clicking run will generated the args `"event","manual"` instead of the event your script is bound to.

#### Typo in variable names
Something nil? Check that your variables are all spelt the same way. They're case sensitive!

### Lua Errors

#### Attempt to OP TYPE1 with TYPE2
If you see an error like `attempt to add nil with number` then somewhere you're code may look like<br>
```lua
local bar = foo + 3
```
in this case `foo` was `nil`, the new question is why.