---
title: AM Utils
permalink: "/docs/reference/am-utils/"
redirect_from:
  - /am-utils/
  - /docs/am-utils/
---

All of the functions listed on this page are found in
```lua
advancedMacros.utils
```

### assertType
**assertType( String:type, *:value, String:functionName, String:argName/Num, Number:level)**

asserts that `value` is of type `type` else throws an error at `level` relative to caller with a message 

"`functionName` arg `argName/Num` expected `type`, got `type(value)`"


The implementation of this function should be simplified in the future to retrieve `functionName` from debug info.


### keys
**keys( Table:tbl ) -> Table**

returns a table with numbered indices listing all keys in `tbl`

### values
**values( Table:tbl ) -> Table**

returns a table with numbered indices listing all values in `tbl`

### asSet
**asSet( Table:tbl ) -> Table**

using `ipairs`, itterates the `tbl` to collect unique values and returns as a table.

### inverse
**inverse( Table:tbl ) -> Table**

swaps keys and values in a copy of `tbl` then returns it.

### reduce
**reduce( Table:tbl, Function:func <, *:i> ) -> return type from** `func`

applies a reducing function to all values in the `tbl` and returns the final result


`i` is the inital value, defaults to the first element returned by `next`'s key

```lua
local utils = advancedMacros.utils

local t = {4,5,6,7,8}
local r = utils.reduce( 
    t, 
    function( a, b ) 
        return a + b
    end
)
log( r ) --30

r = utils.reduce( 
    t, 
    function( a, b ) 
        return a + b
    end,
    8971
)
log( r ) --9001
```

### clone
**clone( Table:tbl <, Boolean:deep> ) -> Table**

Creates a shallow or deep clone of a given table.

```lua
local utils = advancedMacros.utils

local t = {
    x = 45,
    z = {1,2,3}
}
local u = utils.clone( t ) --shallow copy
local v = utils.clone( t, true ) --deep

log( t      == u      ) --false
log( t.x    == u.x    ) -- true
log( t.z    == u.z    ) -- true refers to same table
log( t.z    == v.z    ) -- false also a copy
log( t.z[1] == v.z[1] ) --true
```

<div class="note warning">Note: metatables are not copied</div>
<div class="note error">Deep clones will not handle recursion gracefully in the current version</div>

### append
**append( Table:a, Table:b <, Boolean:inPlace> ) -> Table**

Joins two tables using `ipairs`.

If `inPlace` is true, the returned table is `a`, else a new table

`inPlace` defaults to false

```lua
local utils = advancedMacros.utils
local a = {4,5,6}
local b = {7,8,9}
local c = utils.append( a, b )
log( c ) --{4,5,6,7,8,9}
log( a ) --{4,5,6}
utils.append( a, b, true )
log( a ) --{4,5,6,7,8,9}
```

### map
**map( Table:tbl, Function:map <,Boolean:mapKeys> ) -> Table**

Applies a function to all values in a table, the returned result is a new table.

If `mapKeys` is true, then `map` takes `2` args and returns `2` args (`key`,`value`) 

else, `1` arg, `1` return (`value`)

```lua
local utils = advancedMacros.utils
local t = {
    cows = 10,
    sheep = 11,
    wolves = 3 
}

local a = utils.map( 
    t,
    function( v )
        return v * 2
    end
)
log( t ) --same table as above
log( a ) --{ cows=20, sheep=22, wolves=6 }

local b = utils.map( 
    t,
    function( k,v )
        return k:upper(), v * 2
    end,
    true
)
log( b ) --{ COWS=20, SHEEP=22, WOLVES=6 }
```

### pickRandom
**( Table:options <, Boolean:useKeys> ) -> ?**

Returns a random value from the table between index `1` to `#options`

If `useKeys` is true then `advancedMacros.utils.keys` will be used to randomly pick a key


### startsWith
**startsWith( String:a, String:b <,Boolean:caseSensitive> ) -> Boolean**

Returns true if `a` starts with `b`
<div class="note"><code>caseSensitive</code> defaults to <code>false</code></div>


### hasText
**hasText( Table:a, String:b ) -> Table**
**hasText( String:a, String:b ) -> Boolean**

#### When <code>a</code> is a Table
Returns a table of strings from `a` where `a[i]:find(b,1,true)` was true.

Iterates using `ipairs`

#### When <code>a</code> is a String
Returns true if the string `b` was found in `a`. Pattern matching is disabled

### inTable
**inTable( *:value, Table:tbl ) -> Boolean**

Returns true if `value` is one of the values in `tbl`.

Iterates using `pairs`

### fTime
**fTime( Number:seconds <, String:format> ) -> String**

Formats a time in seconds into something easier to read.

Default format: `"%02d:%02d:%02d"`


If hours becomes larger than `24` the result will read like
`1 days 00:00:00`

### split
**split( String:text, String:deliminators ) -> Table**

splits text by doing this:
```lua
local out = {}
for a in text:gmatch("[^"..delims.."]+") do
  table.insert(out,a)
end
return out
```

```lua
local utils = advancedMacros.utils
log( utils.split( "hello world", "eo" )  ) -- {"h","ll w","rld"}
```

### charArray
**charArray( String:str ) -> Table**

```lua
local utils = advancedMacros.utils
log( utils.charArray( "foo" ) ) -- {"f","o","o"}
```

### splitWords
**splitWords( String:text <,Boolean:lower> )**

Splits up `text` with a ` ` (space) deliminator


`lower` default false, if true all strings have `:lower()` applied to them

```lua
local utils = advancedMacros.utils
log( utils.splitWords( "hello world" ) ) -- {"hello","world"}
```

### capitalizeWords
**capitalizeWords( String:text )**

```lua
local utils = advancedMacros.utils
log( utils.capitalizeWords( "hello world" ) ) -- "Hello World"
```

### maskStr
**maskStr( base, mask, start ) -> String**
Lets you impose one string on another

```lua
local utils = advancedMacros.utils
log( utils.maskStr( 
  ".........." -- 10 long
  "BAR",
  3 
)) -- "..BAR....."
```

### matchesOption
**matchesOption( String:name, String:option ) -> Boolean**

Returns true if `option` is valid for auto-completion of `name`

`helm min` would be valid for `Minecraft Helmet` because `helm` and `min` are both the starts of words in `option`


Used by `.autoComplete`

### autoComplete
**autoComplete( String:text, Table:allOptions ) -> Table**

Returns a list of auto-complete options for `text`

```lua
local utils = advancedMacros.utils
local opts = {
    "cow",
    "sheep",
    "crossbow",
    "wooden pickaxe",
    "wooden shovel"
}

log( utils.autoComplete( "c", opts ) ) -- {"cow","crossbow"}
log( utils.autoComplete( "sh", opts ) ) -- {"sheep","wooden shovel"}
log( utils.autoComplete( "r", opts ) ) -- {} --no words start with "r"
log( utils.autoComplete( "w", opts ) ) -- {"wooden pickaxe","wooden shovel"}
log( utils.autoComplete( "w p", opts ) ) -- {"wooden pickaxe"} --has words that start with "w" and "p"
log( utils.autoComplete( "", opts ) ) -- everything, everything contains empty string
```

### writeFile
**writeFile( String:text <, String:file <, Boolean:append>> )**
**writeFile( Table:tbl <, String:file <, Boolean:append>> )**

Dumps text/table into a file.

Uses `advancedMacros.utils.serializeOrdered( tbl )` for tables

`file` defaults to `debugOutput.txt`
`append` defaults to `false`

### multiGet
**multiGet( Table:tbl, Table:keys <,Boolean:unpack>) -> Table/Varargs**

Returns a with only keys `keys` with values from `tbl`

If `unpack` is true, the table is unpacked

### kwargs
**kwargs( Table:argInfo, ... ) -> Table**

<div class="note"> See <a href="/kwargs">THIS</a> page for details </div>

### typeMatches
**typeMatches( *:value, Table:options ) -> Boolean**

Returns true if `type(value)` is present in `options` or


`value` and `option` in `options` are a instance and class, where `value:isA( option )` is true or


`value` is a class and `option` is a string starting with `class:` ending with the class name
**this loads the class using require to allow for child classes to be matched**

```lua
local typeMatches = advancedMacros.utils.typeMatches
local Foo = newClass"theincgi.Foo"
local Foo = newClass"theincgi.Bar"
local foo = Foo:new()

log( typeMatches(   10, {"number","boolean"} ) ) -- true
log( typeMatches( true, {"number","boolean"} ) ) -- true
log( typeMatches( "hi", {"number","boolean"} ) ) -- false
log( typeMatches(  foo, {"number", "boolean"} ) ) -- false
log( typeMatches(  foo, {Foo, "boolean"} ) ) -- true
log( typeMatches(  foo, {"class:theincgi.Foo","boolean"} ) ) -- true
log( typeMatches(  foo, {"class:theincgi.Bar","boolean"} ) ) -- false
```

### serializeOrdered
**serializeOrdered( Table:tbl <,Function sortFunction> ) -> String**

Returns a string representation of `tbl`.

`sortFunction(a, b)` returns true if `a < b`

Default sort function:
```lua
function( a,b )
    if type(a)~=type(b) then
      return type(a)<type(b)
    end
    return a<b
end
```

### tryCatch
**tryCatch{ try=Function <,catch=function> <,finally=function> <,args=Table> } -> ?**

Attempts to call `try` with `args` unpacked as args (if present, no args otherwise)


If successful, run `finally` (if present) with no args

Returned value(s) is the returned value(s) from `try`


If error, `catch` is run with the error from `xpcall` as it's arg ( you are still in the xpcall and can use debug functions to retrieve stacktrace info ).

`finally` is called with no args after `catch` completes

If `catch` returns any values `tryCatch` returns that instead.

<div class="note">//TODO: give <code>catch</code> & <code>finally</code> the same function environment as <code>try</code></div>

```lua
local tryCatch = advancedMacros.utils.tryCatch

local file
local contents = tryCatch{
    try = function( ... )
        file = filesystem.open("foo.txt","r")
        return file.readLine()
    end,
    catch = function( err )
        log("Could not read file! &c"..err)
        return false
    end,
    finally=function()
        if file then
            file.close()
        end
    end
}

log( contents ) --first line of file or false
```

### weightedRandom
**weightedRandom( Table:options ) -> ?**

given a table `options` with each key being a possible return value and the value being a weight, return something randomly

```lua
local wRandom = advancedMacros.utils.weightedRandom

local x = {
    "foo" = 10, -- 10 / 20 chance
    "bar" = 4,  --  4 / 20 chance
    "cow" = 6   --  6 / 20 chance
}
--20 is total of 10 + 4 + 6
local y = wRandom( x )
```

### utils.inRect
**inRect( Number:testX, Number: testY, Number:boxX, Number:boxY, Number:boxWidth, Number:boxHeight) -> Boolean**

Check if a point `testX, testY` exists in a box starting at `boxX, boxY` with size `boxWidth, boxHeight`