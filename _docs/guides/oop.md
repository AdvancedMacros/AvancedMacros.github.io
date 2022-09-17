---
title: Object Oriented Programming
permalink: "/guides/object-oriented-programming/"
redirect_from:
  - /guides/oop/
---
## Making Classes with AM

### The template
```lua
local MyClass = newClass"com.theincgi.MyClass"

--Constructor
local _new = MyClass.new   --get default instructor
function MyClass:new( ... )
  local obj = _new( self ) --constructs object, also calls super constructors as needed
  
	--initalize object
	obj.foo = "Hello World!"

  return obj
end

--instance function
function MyClass:foo()
  log( self.foo )  --uses self instead of obj
end

return MyClass
```
(for anyone who remembers `advancedMacros.inherit`, it still exists, but this requires far less setup and offers some additonal features (ps, it's not indented like that in the page source... thanks markup))

<div class="note warning">In the constructor <code>self</code> refers to the class definition of <code>MyClass</code> instead of the instance
</div>

### Best Practices

To avoid naming a class the same thing as someone else, include your minecraft username or reversed domain name before the class name.<br>
Consider also including a project name if it's related to something.
Any of these are fine:<br>
 - `com.theincgi.Foo`
 - `theincgi.Foo`
 - `theincgi.PathFinder.Foo`
 - `com.theincgi.PathFinder.Foo`


Keep class files in `~/macros/libs/username/` and load them using `require` instead of `run`<br>
If relevant to a project you plan to share then instead add your project root to the require path and keep classes there.
<br><br>
While developing, it may be easier to load them with run, but keep in mind that type checking will not work correctly if<br>
an instance was created with a different copy of a class.<br>
This is because `isA( class )` doesn't check the class name (string), it checks the class object and it's parents if any for matches.<br>
Loading with `require` ensures that you should only ever have one class definition for some class. <br>
<br>
If you have functions that do not rely on an instance of your class, put it in `.static`<br>
ex: `MyClass.static = {}`<br>
This makes it easier to know if you should use `.` or `:` on your function calls.<br>
<br>
Have your directory in libs match the formating of your class name<br>
<br>
You can set default values by setting them in your class, when an instance trys to write to it, it will write to it's own table instead, I personally prefer to keep the setup limited to the constructor in most cases however.

#### Recommendations
Less important stuff, consistance can help avoid some issues
 - When overriding a function, leave a comment above it such as
`--override`<br>
This makes it easier to tell which functions are from not from the parent class
 - don't use spaces in your class name
 - classes start with an upper case letter, instances with a lowercase
 - `.` for package names when defining a new class
 - camelCase
 - constructor(s) towards the top of your class
 - local functions above constructor
 - comment usage of functions / constructors if it's not obvious


### Basic example
`~macros/libs/com/theincgi/Counter.lua`
```lua
local Counter = newClass"com.theincgi.Counter"

local _new = Counter.new
function Counter:new( ... )
  local obj = _new( self )
  
	obj.count = 0

  return obj
end

function Counter:inc()
  self.count = self.count + 1
end

return Counter
```
Somewhere else
```lua
local Counter = require"com/theincgi/Counter"
local counter = Counter:new()
counter:inc()
log( "Counter is &b"..counter.count ) --1
```

### Inheritance
`~/macros/libs/com/theincgi/AdvCounter`
```lua
local Counter = require"com/theincgi/Counter"
local AdvCounter = newClass"com.theincgi.AdvCounter"

--you can skip the constructor if it's the same

--override
function Counter:inc()
  self.count = self.count + 5
end

return Counter
```
Somewhere else
```lua
local AdvCounter = require"com/theincgi/AdvCounter"
local advCounter = AdvCounter:new()
advCounter:inc()
log( "Counter is &b"..counter.count ) --5
```

### Super calls
`~/macros/libs/com/theincgi/AdvCounter`
```lua
--...
--override
function Counter:inc()
  self:super().inc( self ) -- +1
  self.count = self.count + 5
end
--...
```
Somewhere else
```lua
local AdvCounter = require"com/theincgi/AdvCounter"
local advCounter = AdvCounter:new()
advCounter:inc()
log( "Counter is &b"..counter.count ) --6
```

### Type Checking
Sometimes you want to make sure your argument isn't just a table, but is a certain class, heres how

#### isClass( x )
```lua
log( isClass( advCounter ) ) --true
log( isClass( 45 )) --false
log( isClass( {} )) --false
```

#### isA( class )
```lua
log( advCounter:isA( AdvCounter ) ) --true
log( advCounter:isA( Counter ) )    --true
log( counter:isA( AdvCounter ) ) --false
log( counter:isA( Counter ) )    --true
```

#### typeMatches
lets you check for multiple types at the same time
```lua
local typeMatches = advancedMacros.utils.typeMatches

log( typeMatches( advCounter, {AdvCounter} ) ) --true
log( typeMatches( counter, {AdvCounter} ) ) --false
log( typeMatches( advCounter, {Counter} ) ) --true
log( typeMatches( 15, {AdvCounter,"string","boolean"} ) ) --false
log( typeMatches( advCounter, {"class:com/theincgi/AdvCounter"} ) ) --true
```
<div class="note">Notice: You can also specifify a class by providing a string starting with <code>class:</code> and ending with the path used by <code>require</code></div>
### MetaEvents
Making meta events work on objects can get confusing, luckly you don't have to worry about that.<br>
<br>
Just call `obj:__enableMetaEvents()` in your `constructor`
any functions that have the event name should be triggered with `self` included<br>

| Supported Events |
|------------------|
| __index          |
| __newindex       |
| __mode           |
| __call           |
| __metatable      |
| __tostring       |
| __len            |
| __pairs          |
| __ipairs         |
| __gc             |
| __name           |
| __unm            |
| __add            |
| __sub            |
| __mul            |
| __div            |
| __mod            |
| __pow            |
| __concat         |
| __eq             |
| __lt             |
| __le             |

<div class="note warning"><code>__gc</code> is listed but may not be triggered</div>

### VS Code Snippets
Using VS Code?
`File` → `Preferences` → `Configure User Snippets` → `lua.json`

#### Class setup

```json
"Lua Class Template": {
	"prefix":["class"],
	"body": [
		"local $TM_FILENAME_BASE = newClass\"${1:PACKAGE_NAME}.$TM_FILENAME_BASE\"",
		"",
		"local _new = $TM_FILENAME_BASE.new",
		"function $TM_FILENAME_BASE:new( ... )",
		"  local obj = _new( self )",
		"  ",
		"  return obj",
		"end",
		"",
		"",
		"",
		"return $TM_FILENAME_BASE",
	]
}
```

#### Constructor only
```json
"Lua constructor": {
	"prefix":["new","constructor"],
	"body": [
		"local _new = $TM_FILENAME_BASE.new",
		"function $TM_FILENAME_BASE:new( ... )",
		"  local obj = _new( self )",
		"  ",
		"  return obj",
		"end"
	 ]
}
```

#### Function

```json
"Class Function": {
	"prefix":["cfunc"],
	"body": [
		"function $TM_FILENAME_BASE:$1($2)",
		"  $3",
		"end"
	]
}
```

#### Super Call
```json
"Call Super": {
    "prefix": ["super"],
    "body": ["self:super().$1( self$2 )"]
}
```
    
## Since

|    MC    |    AM    |
|:--------:|:--------:|
| `1.12.2` | `7.11.0` |