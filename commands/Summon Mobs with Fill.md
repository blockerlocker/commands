To summon mobs with the `/fill` command, you can simply fill an area with a self-activating Command Block that has a summon command pre-written in it. For example, the following command will summon 81 Zombies around the player;
```
/fill ~-4 ~ ~-4 ~4 ~ ~4 command_block{auto:true,Command:"summon zombie"}
```
The `auto` tag is what makes it activate the moment it's placed into the world. You can of course select any two sets of coordinates, and fill any area with these mob-spawning Command Blocks, which is great for setting up large mob battle simulations.

The problem with this approach however is the fact that it leaves behind the Command Block, which isn't usually ideal. I've found the simplest way to get rid of these leftover Command Blocks is by placing down a Repeating Command Block, making sure it's powered by Redstone, and putting the following command inside;
```
execute as @e at @s if block ~ ~ ~ command_block{auto:1b,LastOutput:{extra:[{translate:"commands.summon.success"}]}} run setblock ~ ~ ~ air
```

All this does is look at the location of every mob, and check if it's standing inside of an autuomatic Command Block that has just successfully summoned a mob. If that check passes, it replaces the block with air. This definitely isn't the most bulletproof or lagproof solution, but it's fun for messing around and summoning giant cubes of Creepers, like this;
```
/fill ~-5 ~ ~-5 ~4 ~29 ~4 command_block{auto:true,Command:"summon creeper"}
```
