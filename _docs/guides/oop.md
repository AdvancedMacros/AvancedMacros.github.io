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

local _new = MyClass.new
function MyClass:new( ... )
  local obj = _new( self )
  
  return obj
end

return Entity
```
(for anyone who remembers `advancedMacros.inherit`, it still exists, but this requires far less setup and offers some additonal features)

### Best Practices
To avoid naming a class the same thing as someone else, include your minecraft username or reversed domain name before the class name.<br>
Consider also including a project name if it's related to something.
Any of these are fine:<br>
 - `com.theincgi.Foo`
 - `theincgi.Foo`
 - `theincgi.PathFinder.Foo`
 - `com.theincgi.PathFinder.Foo`
<br>
Keep class files in `~/macros/libs/username/` and load them using `require` instead of `run`<br>
While developing, it may be easier to load them with run, but keep in mind that type checking will not work correctly if<br>
an instance was created with a different copy of a class.<br>
This is because `isA( class )` doesn't check the class name (string), it checks the class object and it's parents if any for matches.<br>
Loading with require ensures that you should only ever have one class definition for some class. 

### Basic example

### Inheritance

### Super calls

### Type Checking

### MetaEvents

### VS Code Snippets

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
    
	
	