---
title: Functions
permalink: "/docs/reference/functions/"
redirect_from:
  - /functions/
  - /docs/functions/
---

<div class="note">Any arguments with <code><></code> around them are optional.</div>
<div class="note">Hit the <code>HOME</code> key at any point to jump to the top of the page</div>
<div class="note">Hit the <code>END</code> key at any point to jump to the bottom of the page</div>

### attack

**attack( \<Number: millis> )**


Causes the player to rapidly click or hold the `attack` keybinding (`lmb`)
when millis is...

| Value     | Result                                             |
|:----------|:---------------------------------------------------|
|nil        | Instantly press and release the attack kebind.     |
|-1         | Hold the attack keybind continuously.              |
|0          | Cancel's the action                                |
|millis > 0 | Attack keybind is held for that many milliseconds. |

### back

**back( Number: millis )**


Causes the player hold the `back` keybinding (`s`)
when millis is...

| Value     | Result                                             |
|:----------|:---------------------------------------------------|
|-1         | Hold the back keybind continuously.                |
|0          | Cancel's the action                                |
|millis > 0 | Back keybind is held for that many milliseconds.   |

### connect

**connect( String: serverIP )**


Attempts to connect you to a server.

### customizeSkin

**customizeSkin( String: Part, Boolean: value )**


Turns skin layers on or off for the player.

| Parts     | Alias   |
|:----------|:--------|
| hat       | helmet  |
| jacket    | chest   |
| left leg  |         |
| right leg |         |
| left arm  |         |
| right arm |         |
| cape      |         |

### disconnect

**disconnect()**


Leaves the server you are connected too.

### drop

**drop( \<Boolean: Drop All> )**


Throw your currently held item.
(like `q`)
If `true` is given as an arg then it will drop the whole stack.
If no arg is passed

### entityRayTrace
**entityRayTrace{ ... }**

everything is optional

| Arg    | Type    | Alias| Note |
|:-------|:--------|:-|:-----|
| yaw    | Number  |  | If set, `pitch` defaults to player pitch |
| pitch  | Number  |  | If set, `yaw` defaults to player yaw     |
| to     | Table   | `target`,`dest`,`destination` | Alternative to `yaw` & `pitch`, {x,y,z} end point of the vector
| from   | Table   | `src`, `source` | defaults to player eyePos|
| fluids | Boolean | `fluid`, `liquid`, `liquids`, `stopOnLiquid` ||
| reach  | Number  | `dist`,`distance`,`range`| if using `to` vector is scaled to `reach` length |

Defaults
  player eye pos, player look direction, player reach amount, and fluids `true`

Returns 

| Key             | Type     | Note                                           |
|:----------------|:---------|:-----------------------------------------------|
| entityID        | Number   |                                                |
| getEntityInfo   | Function | shortcut for getEntity( .entityID )            |
| subHit          | Number   | idk                                            |
| vec             | Table    | `{x,y,z}` of the hit pos                       |


### forward
Causes the player hold the `forward` keybinding (`w`)
when millis is...

| Value     | Result                                             |
|:----------|:---------------------------------------------------|
|-1         | Hold the forward keybind continuously.             |
|0          | Cancel's the action                                |
|millis > 0 | forward keybind is held for that many milliseconds.|

### getBiome

**getBiome( <Number: BlockX, Number: BlockZ> )**


Returns a table with details about the biome either at the players location or the given location.

Output:

| key        | type    |
|:-----------|:--------|
|canSnow     | Boolean |
|canRain     | Boolean |
|rainfall    | Number  |
|temp        | String  |

|Tempatures  |
|:-----------|
|ocean       |
|cold        |
|medium      |
|warm        |

### getBlock

**getBlock( Number: x, Number: y, Number: z )**


Returns a table with information about a block at the given position.
If the block requested is not loaded or is `void air` then it will return false.

| Key | Type | Description |
|:----|:------|:-------------|
|id    | String | The block id, such as "minecraft:stone" |
|name | String | The block name, such as "Stone" |
|nbt  | Table  | NBT tag data about the block<br>This is limited to tile entites and client side info. |
|harvestTool | String | The best tool to break this block.<br>Not every block has a harvest tool and this may be omited |
|mapColor   | Table | The color this block would be on a map in {r,g,b,a} format |

### getBlockLight

**getBlockLight(<Number: x, Number: y, Number: z>)**


Returns the current block light level at a given position.
If no position is given it will use the players position.

### getBlockList

**getBlockList()**


A bit of a misnomer, this function returns a table of all `blocks` and `items` in the game (including mods).
Each entry will be what it would look like if you had an item stack of `1` in an inventory and `log`ed it.
The table uses the item id (such as `minecraft:birch_stairs`) as the key, and the example item as the value.

<div class="note">You can check what creative tabs a block or item would belong to by scanning the results from this function</div>

### getBoundingBox

**getBoundingBox( Number: blockX, Number: blockY, Number: blockZ )**


#### getBoundingBox( {Number: blockX, Number: blockY, Number: blockZ} )

**getBoundingBox( Number: EntityID )**


Returns a table with functions relating to a bounding box of a block or entity.\
For blocks, a second return value of `true` or `false` will be returned indicating if the block is solid.

| function name | args | return value(s) | description |
|:----------------|:-----|:----------------|:-------------|
|contains           |Number: x,<br>Number: y,<br>Number: z | Boolean | Checks if a point exists inside the bounding box |
|contract           |Number: x,<br>Number: y,<br>Number: z |             | Makes the bounding box smaller in a direction. Negative numbers reduce the side on the negative of that axis |
|expand           | Number: x,<br>Number: y,<br>Number: z |             | Makes the bounding box bigger in a direction. Negative numbers effect the negative sides. |
|getCenter       |              | Number: x,<br>Number: y,<br>Number: z | Returns the center point of this bounding box |
|getPoints		|   | Number: xMin,<br>Number: yMin,<br>Number: zMin<br>Number: xMax,<br>Number: yMax,<br>Number: zMax | Returns the points defining this bounding box |
|grow           | Number: amount |       | Expands a bounding box on all sides. |
|intersects    | BoundingBox      | Boolean | Returns true if the two bounding boxes overlap |
|intersect      | BoundingBox    | BoundingBox | Creates a new bounding box where the two bounding boxes overlap. |
|offset         | Number: x,<br>Number: y,<br>Number: z |  | Moves the bounding box by the given amount |
|shrink         |Number: amount |        | Contracts the bounding box on all sides |
|Union         | BoundingBox | BoundingBox | Creates a new bounding box using the MIN of one and the MAX of another |
|findEntityOnPath| Number: x,<br>Number: y,<br>Number: z<br><b>or</b><br>{x, y, z} |   | Creates a line starting from the bounding box's center to the center + the vector.<br> The first entity that is found to cross this region (including the box's size) is returned. |

### getChunkUpdateCount

**getChunkUpdateCount()**


Returns the number of chunk updates as seen in the `F3` debug menu.

### getEntity

**getEntity( Number:ID )**


Returns a table with information about an entity much like `getPlayer()`.\
`getEntityList()` can be used to locate an entity's ID number.

| Key                | Type                     | Note                                                                                                         |
|:-------------------|:-------------------------|:-------------------------------------------------------------------------------------------------------------|
|name                | String                   |                                                                                                              |
|class               | String                   | Recommended for checking if a mob is the correct type.<br>(Name tags will affect 'name')                     |
|pos                 | Table                    | Entity position as {x,y,z}                                                                                   |
|dimension           | Table                    |                                                                                                              |
|pitch               | Number                   | The Up/Down rotation of the entity's head                                                                    |
|yaw                 | Number                   | The Left/Right rotation of the entity's head                                                                 |
|fallDist            | Number                   | How far the entity has fallen.<br>0 if the entity is not falling.                                            |
|height              | Number                   |                                                                                                              |
|width               | Number                   |                                                                                                              |
|hurtResTime         | Number                   | How long until the entity can take damage again.                                                             |
|isCollidedHoriz     | Boolean                  |                                                                                                              |
|isCollidedVert      | Boolean                  |                                                                                                              |
|isNoClip            | Boolean                  | If the entity can pass through blocks like a spectator                                                       |
|onGround            | Boolean                  |                                                                                                              |
|isInvulnerable      | Boolean                  |                                                                                                              |
|team                | String                   | <code class="highlighter-rouge">none</code> or the teams name                                                |
|velocity            | {Number, Number, Number} | {x, y, z} velocity of the entity                                                                             |
|health              | Number                   |                                                                                                              |
|isOnLadder          | Boolean                  |                                                                                                              |
|potionEffects       | Table                    | Each entry describes another potion effect                                                                   |
|air                 | Number                   | Amount of air remaining until the entity starts drowning                                                     |
|isInWater | Boolean |                          |                                                                                                              |
|isInLava            | Boolean                  |                                                                                                              |
|immuneToFire        | Boolean                  |                                                                                                              |
|isImmuneToExplosion |                          | <span class="tableFlavorText">Someone, give this to a creeper</span>                                         |
|isOnFire            |Boolean                   |                                                                                                              |
|isSprinting         | Boolean                  |                                                                                                              |
|entityRiding        | Table                    | Lists all the stuff in this table, but for the entity that is being ridden.                                  |
|isInvisible         | Boolean                  |                                                                                                              |
|nbt                 | Table*                   | In some cases nbt may show up as <code class="highlighter-rouge">false</code> if an error occured getting it |
|uuid                | String                   |                                                                                                              |
|lookingAt           | {Number, Number, Number} | What block the entity is looking at                                                                          |

### getEntityList

**getEntityList()**


Returns a list of entities loaded in your chunks.

Each entity will have...

| name  | Either the nametag name, player name, or entity type     |
| id    | ID number used to get more information about this entity |
| class | Exact type of entity                                     |

### getEntityNBT

**getEntityNBT( Number: ID )**


Return a table with just the NBT data for an entity.\
ID number is from the `getEntityList()` function.

### getFps

**getFps()**


Returns the current FPS as seen in the `F3` debug menu.

### getHotbar

**getHotbar()**


Returns the currently selected hotbar index.\
(`1`-`9`)

### getInventory

**getInventory( \<String: name> )**


Returns a table listing the players inventory contents.\
If a name is given it will return the visible part of another players inventory (or false if no player is found).

<div class="note">When using on another player, you can expect to only see armor and held items.</div>

### getJarLibLoaders
....Looks like this returns a table where jars can be added so require can find them..?

### getLight

**getLight(<Number: x, Number: y, Number: z>)**


Returns the current block and sky light level at a given position.
If no position is given it will use the players position.

Return values:

	light level, sky, block

### getLoadedPlayers

**getLoadedPlayers()**


Returns a list of any players in your loaded chunks.

### getPlayer

**getPlayer( \<String: name> )**


Returns a hoard of information in a table about your player (no arg), or the target player (name arg).

| Key                | Type                     | Note                                                                                                                                                     |
|:-------------------|:-------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------|
|name                | String                   |                                                                                                                                                          |
|inventory           | Table                    | Lists everything you'd see in <code>getInventory()</code>                                                                                                |
|pos                 | Table                    | Entity position as {x,y,z}                                                                                                                               |
|mainHand            | Table                    | Item held in mainHand or <code>false</code>                                                                                                              |
|offHand             | Table                    | Item held in offHand or <code>false</code>                                                                                                               |
|invSlot             | int                      | equivilant of <code>getHotbar()</code>                                                                                                                   |
|dimension           | Table                    |                                                                                                                                                          |
|pitch               | Number                   | The Up/Down rotation of the entity's head                                                                                                                |
|yaw                 | Number                   | The Left/Right rotation of the entity's head                                                                                                             |
|exp                 | Number                   | Players experience points in this level                                                                                                                  |
|expLevel            | Number                   | Player experience level                                                                                                                                  |
|expTotal            | Number                   | Total experience with prior levels                                                                                                                       |
|eyeHeight           | Number                   | How far from the ground the players eyes are located. Changes when sneaking.                                                                             |
|fallDist            | Number                   | How far the entity has fallen.<br>0 if the entity is not falling.                                                                                        |
|height              | Number                   |                                                                                                                                                          |
|width               | Number                   |                                                                                                                                                          |
|swingProgress       | Number                   | Precentage before swing motion is complete and ready to attack again.                                                                                    |
|maxHurtResTime      | Number                   | How long until the entity can take damage again.                                                                                                         |
|isCollidedHori      | Boolean                  |                                                                                                                                                          |
|isCollidedVert      | Boolean                  |                                                                                                                                                          |
|isNoClip            | Boolean                  | If the entity can pass through blocks like a spectator                                                                                                   |
|onGround            | Boolean                  |                                                                                                                                                          |
|isInvulnerable      | Boolean                  |                                                                                                                                                          |
|bedLocation         | {Number, Number, Number} | May be omitted if unset or unavailable.                                                                                                                  |
|team                | String                   | <code class="highlighter-rouge">none</code> or the teams name                                                                                            |
|luck                | Number                   | Current luck amount                                                                                                                                      |
|velocity            | {Number, Number, Number} | {x, y, z} velocity of the entity                                                                                                                         |
|health              | Number                   |                                                                                                                                                          |
|hunger              | Number                   |                                                                                                                                                          |
|isOnLadder          | Boolean                  |                                                                                                                                                          |
|hasNoGravity        | Boolean                  |                                                                                                                                                          |
|potionEffects       | Table                    | Each entry describes another potion effect                                                                                                               |
|air                 | Number                   | Amount of air remaining until the entity starts drowning                                                                                                 |
|isInWater           | Boolean                  |                                                                                                                                                          |
|isInLava            | Boolean                  |                                                                                                                                                          |
|immuneToFire        | Boolean                  |                                                                                                                                                          |
|isImmuneToExplosion | Boolean                  | <span class="tableFlavorText">Someone, give this to a creeper</span>                                                                                     |
|isOnFire            | Boolean                  |                                                                                                                                                          |
|isSprinting         | Boolean                  |                                                                                                                                                          |
|isSneaking          | Boolean                  |                                                                                                                                                          |
|isEyltraFlying      | Boolean                  |                                                                                                                                                          |
|isSleeping          | Boolean                  |                                                                                                                                                          |
|entityID            | Number                   | Used in entity highlighting                                                                                                                              |
|gamemode            | String                   | <code>spectator</code>, <code>creative</code>, <code>survival</code><br><span class="comment">Seems adventure mode may show up as survival. [BUG]</span> |
|entityRiding        | Table                    | Lists all the stuff in this table, but for the entity that is being ridden.                                                                              |
|isInvisible         | Boolean                  |                                                                                                                                                          |
|uuid                | String                   |                                                                                                                                                          |
|lookingAt           | {Number, Number, Number} | What block the entity is looking at                                                                                                                      |

<span id="playerSecret"></span>

### getPlayerBlockPos

**getPlayerBlockPos( \<String: name> )**


Returns the block position of either yourself or a player by name.\
If a player can not be found the function will return <code>false</code>

The position will always be whole numbers.\
If you want the decimal part, use `getPlayerPos()`

### getPlayerList

**getPlayerList()**


Returns a list of players on the server. This is not limited to loaded chunks like `getLoadedPlayers()`.

### getPlayerNBT

**getPlayerNBT( \<String: PlayerName> )**


Returns the NBT data for a player or yourself.

### getPlayerPos

**getPlayerPos( \<String: Player Name >)**


Returns the exact players position of your player or the given player.
If the player can't be found then it will return `false`
```lua
local x, y, z = getPlayerPos()
```

### getProfile

**getProfile()**


Returns the name of the current profile from the bindings menu.

### getRecipes

**getRecipes( \<String: item> )**


Returns a list of crafting recipes.
If an `item` is specified, any recipes whos output item id contains `item` in the string will be added to the list.\
For example: `stone` will add `minecraft:stone`'s recipe as well as `minecraft:cobblestone_stairs` because it has the word `stone` in it.

For 
```lua
local recipes = getRecipes()
```
The output is formated as follows:
recipes[`recipeType`][`recipeNumber`][`'in'`/`'out'`]\
For `input` items:
 - shaped recipes will list items as [x][y][options]
 - shapless recipes will list items as [x][options]
For `output` items:
 - Will list the output item directly
 
<div class="note">Currently (9.0.2) there is no method to check if additional items are returned such as a bucket from cake.</div>


### getScreen

**getScreen()**


Returns a new `image` with controls with the pixel data being a screenshot of the game.

### getSettings

**getSettings()**

Returns a table containing any mod settings and controls for Minecraft settings.

Some useful stuff:
`getSettings().editor.colors.textFill` controls the background color in the editor. (Transparent colors are allowed)
All of the mod's colors are defined in the settings and can be changed to whatever you like.

`getSettings().chat.maxLines` Controls the number of lines the chat can store before it starts removing messages. By default Minecraft has this as `100`. Changing this can be useful for looking at large tables in chat.
A good number to use would be `1000`.

<div class="note warning">Making the <code>maxLines</code> too large may cause lag after many messages accumulate.</div>

`getSettings().scriptBrowser.columns` Controls how many columns are in the file browser. (Too many may cause them to overlap)
`getSettings().profiles` This is the table where each binding profile is saved. You can edit them from here if you want to do so.
`getSettings().minecraft` Returns a table with functions for changing Minecraft settings

| Function Name            | Args              | Return Value(s) | Description                                                                                  |
|:-------------------------|:------------------|:----------------|:---------------------------------------------------------------------------------------------|
|getFov                    |                   | Number          | Current FOV                                                                                  |
|setFov                    | Number:FOV        |                 | Sets FOV. Can be out of normal range.                                                        |
|getVolume                 | String:Category   | Number          | Gets the volume for a selected sound category.<br>[See table below]                          |
|setVolume                 | String:Category,<br>Number:volume | | Sets the volume for some category.<br>[See table below]                                      |
|setRenderDistance         | Number            |                 | Sets your render distance. Value is clamped to range of 2 to 32                              |
|getRenderDistance         |                   | Number          | Returns the render distance setting.                                                         |
|setFullscreen             | <Boolean>         |                 | Arg defaults true. Sets the game to fullscreen or exits fullscreen with false.               |
|isFullscreen              |                   | Boolean         | Is the game full screen.                                                                     |
|getSkinCustomization      |                   | Table           | Returns a table listing if a skin layer is on or off.                                        |
|getSkinCustomization      | String            | Boolean         | Returns a boolean indicating if a skin layer is on or off.                                   |
|getMaxFps                 |                   | Number          | Returns the FPS limit                                                                        |
|setMaxFps                 | Number            |                 | Sets the max FPS                                                                             |
|setAdvancedItemTooltips   | Boolean           |                 | Enable or disable advanced tooltips. (shows durability and id on items)                      |
|isAdvancedItemTooltips    |                   | Boolean         | Check if advanced tooltips are visible                                                       |
|getSmoothLighting         |                   | String          | Lighting mode of <code>off</code>, <code>min</code>, or <code>max</code>                     |
|setSmoothLighting         | String:Mode       |                 | Sets smooth lighting mode. Modes are <code>off</code>, <code>min</code>, or <code>max</code> |
|setAutoJump               | Boolean:autoJump  |                 | Sets if the player uses auto jump.                                                           |
|isAutoJump                |                   | Boolean         | Returns if the player has auto jump enabled.                                                 |
|getChatOpacity            |                   | Number          | Returns current opacity of the chat                                                          |
|setChatOpacity            | Number            |                 | 
|getChatScale              |                   | Number          |
|setChatScale              | Number            |
|getChatHeightFocused      |                   | Number
|setChatHeightFocused      | Number            |
|getChatHeightUnfocused    |                   | Number
|setChatHeightUnfocused    | Number
|setChatWidth              | Number
|getChatWidth              |                   | Number
|setCloudsMode             | String            |                 | Sets the mode for cloud rendering. Modes are <code>off</code>, <code>fast</code>, or <code>fancy</code>.(not case senstive)
|getCloudsMode             |                   | String          | Returns render mode for clouds. Modes are <code>off</code>, <code>fast</code>, or <code>fancy</code>
|setDifficulty             | String            |                 | Sets the difficulty using the difficulty name. <code>peaceful</code>,<code>easy</code>,<code>normal</code>,<code>hard</code>
|setDifficulty             | Number            |                 | Sets the difficulty using:<br><code>0</code> for <u>peaceful</u><br><code>1</code> for <u>easy</u><br><code>2</code> for <u>normal</u><br><code>3</code> for <u>hard</u>
|getDifficulty             |                   | String          | Returns the current difficulty as a string
|setVsync                  | Boolean           |                 | Sets if the game should use <code>vsync</code>
|isVsync                   |                   | Boolean         | Returns <code>true</code> if render settings has <code>vsync</code> enabled
|setEntityShadows          | Boolean           |                 | Set if the game should render shadows for entities
|isEntityShadows           |                   |                 | Returns <code>true</code> if the game currently renders entity shadows
|setFancyGraphics          | Boolean           |                 | Sets if the game should use fancy graphics
|isFancyGraphics           |                   | Boolean         | Returns <code>true</code> if the game is currently using fancy graphics
|setGuiScale               | String            |                 | Sets the GUI scale to one of the following modes:<br><code>auto</code>, <code>small</code>, <code>normal</code>, <code>large</code>
|getGuiScale               |                   | String          | Returns the current GUI scale as a string.
|setHeldItemTooltips       | Boolean           |                 | **For versions 9.0.2 and earlier, function acts the same as:** <code>setAdvancedItemTooltips</code><br>Sets if held item tooltips are enabled.
|isHeldItemTooltips        |                   | Boolean         | Returns true if held item tooltips are enabled
|setInvertMouse            | Boolean           |                 | Sets if the mouse should be inverted
|isInvertMouse             |                   | Boolean         | Returns <code>true</code> if the mouse is being inverted
|getLanguage               |                   | String          | Returns the language code for the current language.<br>Example: <code>en_us</code>
|getLanguages              |                   | Table           | Returns a table with all valid language codes.
|setLanguage               | String            |                 | Sets the current language used by the game
|getLastServer             |                   | String          | Returns the ip of the last server the player was connected to.
|getMainHandSide           |                   | String          | Returns which hand is used as the **main hand**.<br>Sides are <code>left</code> and <code>right</code>
|setMainHandSide           | String            |                 | Set which hand is used as your main hand
|getMipmapLevels           |                   |                 | Returns the current mipmap level
|setMipmapLevels           | Number            |                 | Sets the number of mimpap levels used.
|getMouseSensitivity       |                   | Number          | Returns the current mouse sensitivity setting
|setMouseSensitivity       | Number            |                 | Sets the mouse sensitivity
|setParticleLevel          | String            |                 | Sets the particle level for rendering. Options are:<br><code>all</code><br><code>decreased</code><br><code>minimal</code>
|getParticleLevel          |                   | String          | Returns the current particle level as a string
|setPauseOnLostFocus       | Boolean           |                 | Sets if the game should pause if you switch out of the game.<br>Equivilant of: <code>F3</code>+<code>P</code>
|isPauseOnLostFocus        |                   |                 | Check if the game will pause if no longer focused.
|setSmoothCamera           | Boolean           |                 | Set if smooth camera is enabled
|isSmoothCamera            |                   |                 | Check if smooth camera is enabled
|setPerspective            | String            |                 | Changes the players camera view like <code>F5</code>. Options are:<br><code>first</code><br><code>front</code><br><code>back</code>
|getPerspective            |                   |                 | Return the players perspective as a string
|setTouchscreenMode        | Boolean           |                 | Set if touchscreen mode should be used
|isTouchscreenMode         |                   | Boolean         | Check if touchscreen mode is enabled
|setViewBobbing            | Boolean           |                 | Set if view bobbing should be used.
|isViewBobbing             |                   |                 | Check if view bobbing is enabled.

|Sound Categories |
|:----------------|
|master           |
|music            |
|record           |
|weather          |
|block            |
|hostile          |
|neutral          |
|player           |
|ambient          |
|voice            |

`getSettings().save()` Saves all changes you made to settings. Be sure to call this after making changes.

### getSkyLight
**getSkyLight( \<Number:x, Number:y, Number:z> )**

Returns the light level provided from the sky at a given position or the players current block pos.
### getSound
**getSound( String:file )**
Returns a table with controls for playing a sound.
When a sound stops because it has finished playing or has been stopped with the <code>stop</code> function the resources are released and are not reuseable.
<div class="note">Unlike <code>playSound</code>, <code>getSound</code> follows the same file access rules the rest of the mod follows <span class="comment">[Link needed]</span>.<br>
 With no prefix on the file this is the same folder as your script runs from</div>

**Controls:**

| Function Name            | Args              | Return Value(s) | Description                              |
|:-------------------------|:------------------|:----------------|:-----------------------------------------|
| isPlaying                |                   | Boolean         | Returns true if this instance of the sound is currently playing.
| stop                     |                   |                 | Stops this instance of a sound also causeing an resources used to be released.
| loop                     | Number            |                 | Sets the number of times to play the sound.<br><code>-1</code> and <code>nil</code> will loop endlessly
| pause                    |                   |                 | Stops the audio without discarding resources. Playing will resume where the sound stopped.
| play                     |                   |                 | Starts or resumes playing of an audio clip.
| setVolume                | Number            |                 | Sets the volume for the sound. Volume should be between <code>0</code> and <code>1</code>.

### getWorld
**getWorld()**

Returns a table containing information about the current world or `false` if you are not currently in a world.

| Key                | Type                     | Note                                                                                              |
|:-------------------|:-------------------------|:--------------------------------------------------------------------------------------------------|
| border             | Table                    | world border                                                                                      |
| cleanWeatherTime   | Number                   | seems to always be <code>0</code>...                                                                           |
| difficulty         | String                   | <code>"peaceful"</code>,<code>"easy"</code>,<code>"normal"</code>,<code>"hard"</code>             |
| gameType           | String                   | <code>"creative"</code>,<code>"spectator"</code>,<code>"survival"</code>,<code>"adventure"</code> |
| isDaytime          | Boolean                  |                                                                                                   |
| isDifficultyLocked | Boolean                  |                                                                                                   |
| isHardcore         | Boolean                  |                                                                                                   |
| isRemote           | Boolean                  | ...true even in single player?                                                                    |
| moonPhase          | Number                   |                                                                                                   |
| name               | String                   |                                                                                                   |
| rainTime           | Number                   | also always <code>0</code>...                                                                     |
| seed               | Number                   | minecraft world seed, <code>0</code> if unavailable                                               |
| spawn              | Table                    | {<code>x</code>,<code>y</code>,<code>z</code>}                                                                                                  |
| weather            | String                   | <code>clear</code>,<code>rain</code>,<code>thunder</code> Never clear directly to thunder or back |
| worldTime          | Number                   | in ticks                                                                                          |

#### border

| Key                | Type                     | Note                         |
|:-------------------|:-------------------------|:-----------------------------|
| centerX            | Number                   |                              |
| centerZ            | Number                   |                              |
| dmgAmount          | Number                   |                              |
| radius             | Number                   |                              |
| size               | Number                   | slightly smaller than radius |
| warningDist        | Number                   |                              |

#### moonPhase

| value |                                    | name            |
|:-----:|:----------------------------------:|:----------------|
| 0     | <img src="/assets/img/moon/0.png"> | Full moon       |
| 1     | <img src="/assets/img/moon/1.png"> | Waning gibbous  |
| 2     | <img src="/assets/img/moon/2.png"> | Last quarter    |
| 3     | <img src="/assets/img/moon/3.png"> | Waning crescent |
| 4     | <img src="/assets/img/moon/4.png"> | New Moon        |
| 5     | <img src="/assets/img/moon/5.png"> | Waxing crescent |
| 6     | <img src="/assets/img/moon/6.png"> | First quarter   |
| 7     | <img src="/assets/img/moon/7.png"> | Waxing Gibbous  |

### highlightEntity
**highlightEntity( Number: entityID, String: action <,Boolean: active> )**

Causes an entity to be rendered as glowing or rendered on top of everything else.

| actions          |                |
|:-----------------|:---------------|
|<code>glow</code> | Glowing effect |
|<code>xray</code> | Render on top  |

### httpRequest
**httpRequest{ args... }

| Arg                                 | Type    | Optional | Default                 | Note                                                                      |
|:------------------------------------|:--------|:---------|:------------------------|:--------------------------------------------------------------------------|
| <code>url</code>                    | string  | No       |                         | <code>http:</code> or <code>https:</code> is required in <code>url</code> |
| <code>requestMethod</code>          | string  | Yes      | <code>GET</code>        |                                                                           |
| <code>requestProperties</code>      | table   | Yes      | <code>nil</code>        |                                                                           |
| <code>timeout</code>                | number  | Yes      | <code>10</code>         | value is in seconds                                                       |
| <code>doOutput</code>               | boolean | Yes      | <code>false</code>      | set to <code>true</code> if you need to send data to the server           |
| <code>followRedirects</code>        | boolean | Yes      | ?                       |                                                                           |

#### Returns
Table

| Value              | Type     | Note                                          |
|:-------------------|:---------|:----------------------------------------------|
| disconnect         | Function | disconnect from the server                    |
| err                | Function | returns error input stream                    |
| getContentEncoding | Function |                                               |
| getContentLength   | Function | returns number of bytes                       |
| getFollowRedirects | Function |                                               |
| getHeaderFields    | Function | returns table with headers                    |
| getResponseCode    | Function | returns number                                |
| getURL             | Function | returns url used for this request             |
| input              | Function | returns input stream used to read from server |

### httpQuick
**httpQuick( String:url )**

#### Returns
Table

| Value                               | Type    | Note                                               |
|:------------------------------------|:--------|:---------------------------------------------------|
| <code>.code</code>                  | Number  | http response code integer                         |
| <code>.headers</code>               | Table   | response headers from server                       |
| <code>.length</code>                | Number  | length of response in bytes                        |
| <code>.response</code>              | String  | string returned by server                          |
| <code>:parse()</code>               | Boolean | turns json response into table, returns success    |
| <code>.json</code>                  | Table   | when parsed, json as table                         |
| <code>:save( String:file )</code>   |         | saves as file in <code>"~/downloads/"..file</code> |
| <code>:status()</code>              |         | fancy print on chat                                |
| <code>.time</code>                  | Number  | milliseconds since request and full receive        |
| <code>.type</code>                  | Table   | <code>.response.headers['Content-Type']</code>     |
| <code>.url</code>                   | String  | Url from function call                             |

#### Since

|    MC    |    AM    |
|:--------:|:--------:|
| `1.12.2` | `7.11.0` |

### isKeyDown
**isKeyDown(String: keyName)**

Returns a boolean if a key is held or mouse button is held.
The key name will match the name used in the bindings menu.
<div class="note">Also works with mouse buttons</div>
<div class="note warning">Please note the key names changed between MC versions</div>

### jump
**jump()**
<span id="jumpSecret" style="display:none"></span>
Makes the player jump

<script>
  if ( window.addEventListener ) {
    var kkeys = [], konami = "38,38,40,40,37,39,37,39,66,65";
    window.addEventListener("keydown", function(e){
        kkeys.push( e.keyCode );
        if ( kkeys.toString().indexOf( konami ) >= 0 ) {
            let jump = document.getElementById("jump");
            let e = document.getElementById("jumpSecret");
             setTimeout(()=>{
              jump.scrollIntoView({behavior:"smooth"});
            },500);
            setTimeout(()=>{
              e.style.display="block";
              let msg=`jump("forced")`;
              for(let i=1;i<=msg.length;i++) {
                setTimeout(()=>{
                  e.innerHTML = `<strong>${msg.substr(0,i)}</strong>`;
                },100*i);
              }
              setTimeout(()=>{
                let ps = document.getElementById("playerSecret");

                ps.scrollIntoView({behavior:"smooth",block:"center"});
                
                let msg2="getPlayer().setVelocity( Number:x, Number:y, Number:z )";
                for(let i=1;i<=msg2.length;i++){
                  setTimeout(()=>{
                    ps.innerHTML = `<code class="language-plaintext highlighter-rouge">${msg2.substr(0,i)}</code>`;
                  }, i*100 + 1000);
                }
              },msg.length*100+1500);
            },2000);
            kkeys = [];
        }
    }, true);
}
</script>

### key
**key( String:keyName <, Number:duration> )**

Holds the key with the matching name down for `duration` seconds.<br>
Default duration is `0`,<br>
<br>
When `duration <= 0` the key is released<br>
<div class="note">Duration is in milliseconds</div>

### left
**left( <Number: duration>)**

Holds the left strafe key (`a`) for the provided duration.<br>
Default duration is `0`,<br>
<br>
When `duration <= 0` the key is released<br>
<div class="note">Duration is in milliseconds</div>

### listTextures
**listTextures()**
returns a list of textures.

#### Try in REPL
```lua
tex = listTextures()
b = hud3D.newBlock()
b.changeTexture("block:"..tex[11])
b.enableDraw()
```

### loader
?

### log
**log( ... )**
Writes text to the chat.
<div class="note">Only you can see text written by <code>log</code></div>

#### Basic usage
```lua
log"Hello world!"
log("Hello"," ","world!")
log("You're using AM v",_MOD_VERSION)
```

#### Coloring & Formatting
You can add `&` codes to color/format your text.<br>
Formatting is applied up until the next color change or arg
```lua
log("&aHello World") --green
log("&aHello &BWorld") --green then green &bold
log("&BHello &aworld") --bold & white, then green and not bold
log("&aHello"," world") --world is written with wite text
```
<div class="note">You can escape your <code>&</code> by writing them as <code>&&</code></div>
```lua
log"This && That"
```

| & Code | Effect |
|:-------|:-------|
| 0      | Reset all formating, Color to <code><span style="color: #000000;">BLACK</span>       </code>|
| 1      | Reset all formating, Color to <code><span style="color: #0000AA;">DARK BLUE</span>   </code>|
| 2      | Reset all formating, Color to <code><span style="color: #00AA00;">DARK GREEN</span>  </code>|
| 3      | Reset all formating, Color to <code><span style="color: #00AAAA;">DARK AQUA</span>   </code>|
| 4      | Reset all formating, Color to <code><span style="color: #AA0000;">DARK RED</span>    </code>|
| 5      | Reset all formating, Color to <code><span style="color: #AA00AA;">DARK PURPLE</span> </code>|
| 6      | Reset all formating, Color to <code><span style="color: #FFAA00;">GOLD</span>        </code>|
| 7      | Reset all formating, Color to <code><span style="color: #AAAAAA;">GRAY</span>        </code>|
| 8      | Reset all formating, Color to <code><span style="color: #555555;">DARK GRAY</span>   </code>|
| 9      | Reset all formating, Color to <code><span style="color: #5555FF;">BLUE</span>        </code>|
| a      | Reset all formating, Color to <code><span style="color: #55FF55;">GREEN</span>       </code>|
| b      | Reset all formating, Color to <code><span style="color: #55FFFF;">AQUA</span>        </code>|
| c      | Reset all formating, Color to <code><span style="color: #FF5555;">RED</span>         </code>|
| d      | Reset all formating, Color to <code><span style="color: #FF55FF;">LIGHT PURPLE</span></code>|
| e      | Reset all formating, Color to <code><span style="color: #FFFF55;">YELLOW</span>      </code>|
| f      | Reset all formating, Color to <code><span style="color: #FFFFFF;">WHITE</span>       </code>|
| B      | Bold       |
| I      | Italics    |
| O      | Obfuscated |
| S      | Strikethru |
| U      | Underlined |

<div class="note">REPL history doesn't start empty, hit up until you find a colorful message</div>

#### Click Events
When a click `&` code is added, the next argument after the string is consumed

```lua
log("&a&NHover here&f &b&U&FClickMe","A &atooltip&f!",function(formatted,unformatted) log"You clicked it!" end, " &d&U&FAnother clickable", {hover="Do it!", click=function(formatted,unformatted) log("&a&BIt worked!") end})
```

| & Code | Effect                                                                          | Consumes                    |
|:-------|:--------------------------------------------------------------------------------|:----------------------------|
| F      | Function - Triggeres a function, receives args (formattedText, unformattedText) | Function
| R      | Run - Causes the player to say something, usually used for commands             | String
| T      | Type - Suggest text, puts text into the chat input without pressing enter       | String                                                  |
| L      | Link - URL                                                                      | String URL or table {click="url", hover="tooltip text"} |
| N      | None - No click action, only tooltip                                            | String tooltip or table {hover="tooltip text"}          |
| *      | Open File - Like the link for a screenshot                                      | String file                                             |


### look
**look( Number:yaw, Number:pitch <, Number:millis> )**

Make the player turn their head to some `yaw` and `pitch`.

If `millis` is not provided, head instantly snaps to the angle

If `millis` is provided, head smoothly turns over that many milliseconds.<br>
(Non blocking)

### lookAt
**lookAt( Number:x, Number:y, Number:z <, Number:millis>)

Make the player turn their head to some `x`,`y`,`z`.

If `millis` is not provided, head instantly snaps to the angle

If `millis` is provided, head smoothly turns over that many milliseconds.<br>
(Non blocking)

<div class="note">If you want to look at the center of a block, add <code>.5</code> to the <code>x</code>,<code>y</code> & <code>z</code></div>

### narrate
**narrate( String text <, Boolean:stopCurrentSpeach> )**

Does text to speach for `text`<br>
if the narrator is already saying somethign and `stopCurrentSpeach` is `true`, the narrator will be interrupted, else queued.<br>
Default: `false`

### newMutex
**newMutex( String:name )**

Creates a reference to a mutex used for thread saftey.<br>
A mutex created with the same name as another both refer to the same lock.

#### Behavior
When a mutex is locked, no other threads will be able to lock until the thread that locked it unlocks it (or is cleaned up).

#### Example

##### Preventing spam

```lua
local function noSpam()
  local mutex = newMutex"theincgi_noSpam" --unique name
  if not mutex.tryLock() then 
    return
  end

  playSound("chimes.wav").play()
  sleep(2000) --cooldown for playing the sound

  mutex.unlock() --important!
end

for i=1,10 do
  noSpam()
  --try it without the mutex if you want to hear the difference
  --playSound("chimes.wav").play()
  waitTick()
end
```

#### Preventing race conditon

<a href="/thread-saftey" target="_blank">View here</a>


### openInventory
**openInventory()**

Returns a table containing controls for interacting with inventories

#### Returned table contains...

| Key | Value | Note
|:----|:------|:---------- 
| LMB | 0     | Constant used for `left mouse button`   |
| MMB | 2     | Constant used for `middle mouse button` |
| RMB | 1     | Constant used for `right mouse button`  |
| click | function | |
| close | function | |
| closeAndDrop | |
| dragClick | |
| drop | |
| getHeld | |
| getMap | |
| getSlot | |
| getTotalSlots | | 
| getType | |
| grabAll | |
| hotSwap | |
| mapping | |
| quick | |
| setRecipe | |
| split | |
| swap | |

#### Click
**.click( Number:slot <,Number:button> )**
As if you clicked on a slot using your mouse

#### Close
**.close()**
Closes the gui without dropping items held by the mouse

#### CloseAndDrop
**.closeAndDrop()**
Normal behavior of closing the inventory screen, items dropped to ground if held by mouse.

#### DragClick
**.dragClick( Table:slots <,Number:button> )**
Distribute items across slots in order

#### Drop
**.drop( Number:slot <,Boolean:stack>)**
Drop the item in the provided inventory slot.<br>
If `stack` is true, the whole stack is dropped instead of 1 item.<br>
Default: `false`

#### GetHeld()
**.getHeld( <Boolean:coerce> )**
returns `false` or the item held by the mouse.

If `coerce` is true, a the ItemStack is returned as `userdata`

#### GetMap()
**.getMap()**
returns the slot mappings for the current container/inventory.

##### Typical Usage
```lua
local inv = openInventory()
local map = inv.getMap()
inv.click( map.hotbar[3] ) --clicks 3rd slot in hotbar
```
##### Possible Sections

| Name       | Type   | Note                                                  |
|:-----------|:-------|:------------------------------------------------------|
| hotbar     | Table  | Players hotbar                                        |
| main       | Table  | The first 3 rows of your inventory                    |
| boots      | Number | Equipment slot                                        |
| leggings   | Number | Equipment slot                                        |
| chestplate | Number | Equipment slot                                        |
| helmet     | Number | Equipment slot                                        |
| offHand    | Number |                                                       |
| craftingIn | Table  | keys are `1` to `4` or `1` to `9` depending on screen | 
| craftingOut| Number |                                                       |
| slot       | Number | The only slot in a beacon                             |
| fuel       | Number | in brewing stand or furnace                           |
| input      | Number | Top slot in brewing stand, anvil, villager or furnace |
| output     | Number | In brewing stand, anvil, villager or furnace          |
| contents   | Table  | When viewing a chest, dispenser, dropper or hopper    |
| item       | Number | Left slot in anvil                                    |
| material   | Number | Second slot in anvil                                  |
| tool       | Number | Enchanting table                                      |
| lapis      | Number | Enchanting table                                      |

#### GetSlot
**.getSlot( Number:slot <,Boolean:coerce> )

If `coerce` is true, a the ItemStack is returned as `userdata`
<div class="note">You can craft in the 2x2 even while you're not looking at your inventory screen</div>
<div class="note">It's possible to stash items in your crafting slots. <div class="note warning">These items will drop when you open and close your inventory next, and will likely drop if you log out</div></div>

#### GetTotalSlots()
**.getTotalSlots()**
returns the total number of slots for the current inventory

#### GetType()
**.getType()**
returns the name of the current inventory

common ones with mappings are:

| <code>inventory</code>           |
| <code>enchantment table</code>   |
| <code>villager</code>            |
| <code>anvil</code>               |
| <code>beacon</code>              |
| <code>brewing stand</code>       |
| <code>chest</code>               |
| <code>double chest</code>        |
| <code>crafting table</code>      |
| <code>dispenser</code>           |
| <code>furnace</code>             |
| <code>hopper</code>              |
| <code>horse inventory</code>     |
| <code>shulker box</code>         |

#### GrabAll
**.grabAll( Number:slot )**

Like when you quickly double click an item to pick up all of the same type

#### HotSwap
**.hotSwap( Number:slot, Number:hotbarSlot )
Like when you hover an item in your inventory and hit a number key to switch items

<div class="note error">hotbar slot is a mapped slot, not <code>1</code>-<code>9</code></div>

#### Mapping
**table**
This is used by `.getMap()` and contains all container mappings listed by inventory type
`.getMap()` basically does this:
```lua
local map = inv.mapping[ inv.getType() ]
```

#### Quick
**.quick( Table:slots, <,Number: limit> ) **
**.quick( Table:slots ) **

For quickly transfering inventory contents into a container
<a href="https://github.com/AdvancedMacros/AdvancedMacros/blob/e2208189fa2a49f5884043864896575ca542682f/src/main/java/com/theincgi/advancedMacros/lua/functions/OpenInventory.java#L118-L150">#CHECK_ME</a>

#### SetRecipe 
**.setRecipe( Number:recipeID <,Boolean:makeAll> )**

Emulates clicking on a recipe from the recipe book.<br>
`recipeID` is from <span style="color:#fc0;text-decorration:underline;cursor:pointer;" onclick="document.getElementById('getrecipes').scrollIntoView({behavior:'smooth'});">getRecipes</span><br>

If `makeAll` is `true` then it acts like shift clicking the recipe pulling in as many ingredients as it can.



### pRun
**pRun( String:file )**
pcall, but for `run`

### pickBlock
**pickBlock()**
Middle click action

Survival: select hotbar slot with item or move item from inventory to current hotbar slot

Creative: select hotbar slot with item orcopy item to hand

### pickItem
**pickItem( String:name <, Number:slot )

Attempts to pick an item from your inventory
If it exists it is picked from hotbar or moved to the prefered slot
Slot number is returned or false if none found

Source can be found [here](https://github.com/AdvancedMacros/AdvancedMacros/blob/2ad8f1bae8c4d2d49dd65f011506aaa6ed3463cf/src/main/resources/assets/advancedmacros/scripts/morefunc.lua#L61)

### playSound
**playSound( String:soundName )**

Counterintuitively this returns controls for playing a sound.

Sounds are located in `~/sounds` (AM Root dir)

If you're planning to share your code, it's instead recommended to use `getSound`.

| Controls                    | Returns  | Note                                                       |
|:----------------------------|:---------|:-----------------------------------------------------------|
| .isPlaying()                | Boolean  |                                                            |
| .stop()                     |          | stopped, next play is from start                           |
| .loop( <Number:times> )     |          | Loop `times` times, forever if `<code>`nil`                |
| .pause()                    |          | pause audio, can resume                                    |
| .play()                     |          | play/resume audio                                          |
| .setVolume( Number:volume ) |          | volume is a `%`, so `0` to `1`                               |
| .getClip()                  | Userdata | LuaJava of audio clip                                      |

### print
**print(...)**

Puts text in the console.
<div class="note warning">This does not show up in the chat, it shows up in the Minecraft console.</div>

### rayTrace
**rayTrace(<vector2d:yawPitch> <,vector3d:from> <,Number:reachDistance <,Boolean stopOnLiquid>>)**

`vector2d` can be either `yaw`,`pitch` or `{yaw,pitch}`

`vector3d` can be either `x`,`y`,`z` or `{x,y,z}`


Returns false or a table containing info about the trace result

<div class="note warning">This does not show results for entity hits, see <code></code></div>

If hit block:

| Key    | Note                                        |
|:-------|:--------------------------------------------|
| block  | Table containing `dmg`, `id` and `name`     |
| pos    | `{x,y,z}` block pos                         |
| side   | `up` `down` `north` `east` `west` `south`   |
| subHit | idk                                         |
| vec    | `{x,y,z}` exact location of ray intersection  |

### right
**right( <Number: duration>)**

Holds the right strafe key (`d`) for the provided duration.<br>
Default duration is `0`,<br>
<br>
When `duration <= 0` the key is released<br>
<div class="note">Duration is in milliseconds</div>

### run
**run( String:file, ... )**

Runs a script like a function returning any results.

Unlike require this does not save the returned results and instead runs it each time.

File access rules apply. File is local to the directory of the caller.

<div class="note">you can use <code>filesystem.resolve("",2)</code> to get the local directory of something earlier in the stack trace, 1 being the current scope and 2 being the previous caller </div>

### runThread
**runThread( String file, ... )**
**runThread( function:task, ... )**

Instantly starts the given file or function in a new thread with provided args.

Returns a table with thread controls for checking status and killing the thread if needed.

If you don't wish to start the thread immediatly you can instead do
```lua
local myThread = thread.new( myFunction )
--or
local myThread = thread.new( function(...) run( "myScript.lua", ...)) end )
--then later
myThread.start()
```

### say
**say( String:msg )**
Causes the player to speak into the chat.
This can be used to run commands as well, just don't forget the `/`!

### setHotbar
**setHotbar( Number:slot )**
Selects the hotbar slot.

Slot numbers are `1` through `9`

### setProfile
**setProfile( String:profileName )**
Changes the active profile in the bindings menu

returns `false` if the profile could not be found.

### sleep
**sleep( Number:milliseconds )**

Causes the script to pause for the given number of milliseconds.

### sneak
**sneak( <Number:millis> )**

Holds the sneak key (`shift`) for the provided duration.<br>
Default duration is `0`,<br>
<br>
When `duration <= 0` the key is released<br>
<div class="note">Duration is in milliseconds</div>

### sprint
**sprint( <Boolean:sprint> )**

Default: true, start sprinting

Causes the player to start or stop sprinting

### stopAllScripts
**stopAllScripts**

Kills all running scripts. Like hitting `CTRL`+`AM Menu Key` and clicking each little `[x]`

<div class="note">There's a shortcut for this: <code>CTRL</code>+<code>ALT</code>+<code>SHIFT</code>+<code>AM Menu Key</code></div>

### swapHand
**swapHand()**

Switches your main hand's item with your off hand's item.

### toast
**toast( <String:title> <, String:detail> )**
Creates a popup notification 

Default text for both is `nil`

### use
**use( <Number: duration> )**
**use()**

Holds the use key (`a`) for the provided duration.<br>
<br>
When `duration <= 0` the key is released<br>


If no number is provided then it does an instantaneous click
<div class="note">Duration is in milliseconds</div>
<div class="note">You can click faster than Minecraft allows mouse input for with this</div>

### waitTick
**waitTick()**

Causes the script to sleep until the next Minecraft tick starts.