---
title: Named Args
permalink: "/guides/kwargs/"
redirect_from:
  - /guides/named-args/
  - /kwargs/
---
## The Template
```lua
local kwargs = advancedMacros.utils.kwargs

local function pathFind(...)
  local args = kwargs({
    { from="table", {getPlayerBlockPos()}, "start" },
    { to="table",nil,"finish"}
  },...)

  local from = args.from
  local to = args.to
  --...
end
```

Longer example
```lua
local function needsEntity(...)
  local args = kwargs({
    { entity="table",nil,{"entityID","number"}},
    { thing={"table",Class,"number"},0}
  },...)
  
  --you can see if an alias was used by calling args with the key name, returns the name used
  if args.entityID then
    args.entity = getEntity( args.entityID ) --can also do getEntity( args.entity ) here
  end

  --also valid
  
  if args"entity"=="entityID" then
    --alias used
  end

  --stuff with args.entity & args.thing
end
```
Usage
```lua
local result = pathFind{ to={1,2,3} }
local result = pathFind{ start={1,2,3} }
local result = pathFind{ from={4,5,6}, to={1,2,3} }
local result = pathFind{ to={1,2,3}, from={4,5,6} }
--uses order of defined params
local result = pathFind{ {4,5,6}, {1,2,3} }

needsEntity{entity=blah}
needsEntity{entityID=1234}
```
## About
Does your function take a lot of args?<br>
Forgeting which order stuff goes in?<br>
Need type checks?<br>
<br>
`advancedMacros.utils.kwargs({},...)` is here to help.

## Format
The only **required** part of an arg definition is the `name` and `type`<br>

### Arg formats
{ `name` = `type`, `default`, `aliases...` }<br>
{ `name` = {`type1`,`type2`...}, `default`, `aliases...` }

### Alias formats
`string:name`<br>
{`string:name`, `type1`,`type2`,...}

## Behavior
If the defined type(s) do not allow for nil:
 - and arg is nil, default applied
 - and arg is not nil, error thrown

If using an alias for arg:
 - and alias does not include type(s), main type is used for constraint
 - and alias lists type(s), those types are used for checks

### Return'd table
When indexing the primary `name` of an arg, always returns the value used for it or any of it's aliases

When indexing on an `alias`, returns a value if the alias was used, `nil` otherwise

When calling with string of a `name` returns the actual name used to set that value
<div class="note">This is helpful when copying parts of the args to hand off to another function</div>
```lua
local subArgs = { [args"entity"] = args.entity }
```

## VS Code Snippet
Using VS Code?
`File` → `Preferences` → `Configure User Snippets` → `lua.json`
```json
"kwargs": {
  "prefix": ["kwargs"],
  "body": [
  "local args = utils.kwargs({$0",
  "},...)"
  ]
}
```

## Since

|    MC    |    AM    |
|:--------:|:--------:|
| `1.12.2` | `7.11.0` |