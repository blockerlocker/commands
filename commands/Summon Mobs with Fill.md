These commands were originally tested in 26.1. If you have any issues, feel free to join my Discord server: https://discord.blocker.locker

To summon mobs with the `/fill` command, we need to fill an area with self-activating Command Blocks by setting the `auto` tag of the Command Block to `true`, which will look something like this;
```
/fill <x1> <y1> <z1> <x2> <y2> <z2> command_block{auto:true}
```

These types of Command Blocks will instantly activate when pasted into the world. We can then give this self-activating Command Block any command we like, such as a `/summon` command to fill an area with mobs, though this will have the unfortunate side-effect of leaving the Command Blocks behind. If we instead use a `/execute` command like the one below, we can ensure the Command Blocks are instantly replaced with air when the mob is summoned. (Credit to a [comment from @flamingfire0](https://www.youtube.com/watch?v=fIutv--GtIQ&lc=Ugy2-o_1GMApQkhtLFd4AaABAg) who informed me of this method!)
```
/execute summon creeper run setblock ~ ~ ~ air
```

So as an example, we can create a command like the one below, which will summon 81 Zombies around the player;
```
/fill ~-4 ~ ~-4 ~4 ~ ~4 command_block{auto:true,Command:"execute summon zombie run setblock ~ ~ ~ air"}
```
You can of course use any mob, and choose any two sets of coordinates to fill any area with these mob-spawning Command Blocks, which is great for setting up large mob battle simulations.

---

> In [this video](https://www.youtube.com/shorts/fIutv--GtIQ), I used a different method for summoning mobs with the `/fill` command that required the use of a Repeating Command Block. Although the method above is much better, you can see the guide for the original method below.

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
