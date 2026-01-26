These commands can be used to build an animated gate in your creative builds, as seen in [this video](https://youtube.com/shorts/oQVNJjuYoq8). These commands were written in version 1.21.11, but the concept behind this tutorial will work in any versions that have Block Displays, the command syntax might just be a little different.

### Step One
First, place three fences, and shoot an arrow into the middle fence. Then run this command to get the block state in NBT format:
```
/data get entity @n[type=arrow] inBlockState
```
There are other ways of getting the block's properties, such as using the `looking_at_block_state` Debug Screen Text in the F3 menu, but the arrow trick helps you figure out how you're supposed to format it when writing commands.

### Step Two
Next, paste the following command into a regular Command Block, and add the fence's block state to the `block_state` section of the command:
```
summon block_display ~-0.5 ~-0.5 ~-0.5 {block_state:{},teleport_duration:20,Tags:[big_gate]}
```
For example, if you are using an Oak Fence, the command might end up looking like this:
```
summon block_display ~-0.5 ~-0.5 ~-0.5 {block_state:{Properties:{east:"true",waterlogged:"false",south:"false",north:"false",west:"true"},Name:"minecraft:oak_fence"},teleport_duration:20,Tags:[big_gate]}
```
You do not need to include all of the block's data, only the properties that aren't considered "default". For example, in the command above, you can remove `waterlogged`, `south`, and `north`.

### Step Three
Now set the Command Block to 'Always Active', and hit 'Done'. This will summon the first Block Display in your gate. You can then hold Control and press Middle Click (or whatever your Pick Block key is) to get the Command Block as an item, with its command and settings still inside.

If you place this block down, it will instantly spawn another new Block Display, allowing you easily build out the rest of your gate. If you misplace a Block Display, just break the Command Block, stand in the misplaced Block Display, and run this command:
```
/kill @n[type=block_display]
```
Break all of these Command Blocks, and the Block Displays will be in the shape of your gate.

### Step Four
You can now use the following commands to either teleport your gate up by 3 blocks, or teleport it down, allowing you to animate it.
```
execute as @e[tag=big_gate] at @s run tp @s ~ ~3 ~
```
```
execute as @e[tag=big_gate] at @s run tp @s ~ ~-3 ~
```
You can obviously change the coordinates in those commands if you want to change how many blocks up the gate animates, but if you want to change the speed at which the gate opens and closes, you can use this command to set the Block Displays' `teleport_duration` in ticks (1/20th of a second)
```
/execute as @e[tag=big_gate] run data modify entity @s teleport_duration set value 30
```
