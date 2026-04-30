These commands let you build an Ancient City portal opening animation, as seen in [this video](https://www.youtube.com/shorts/5OwQGjNDLKo). There is also [this companion resource pack](../resourcepacks/ancient_city_portal.zip) that makes Nether Portals look blue. These commands were made in version 26.1.2, but will likely work in other modern versions of the game.

First, a scoreboard objective must be created to keep track of the animation. Run this command in chat once.
```
/scoreboard objectives add portal_animate dummy
```

Next, we must animate the opening sequence. We can do this by first placing an Impulse Command Block in the bottom corner of the portal frame, pasting in the command below, clicking "Always Active", and then clicking "Done". This will spawn an invisible Marker, and give it a `portal_animate` score of 1.
```
execute summon marker run scoreboard players add @e[type=marker,distance=..30] portal_animate 1
```

Now if we hold Control and Middle-Click (Pick Block) on the Command Block, we will get a copy that instantly activates when placed down. This is how we will animate the opening sequence; by placing our Command Blocks in the order we want the portal blocks to appear. Whenever we place a Command Block down, it creates a new Marker, and increases every nearby Marker's `portal_animate` score by 1, so the oldest Marker will have the highest score, and the newest Marker will have the lowest score.

Once you're done filling the entire frame with these instant Command Blocks, we now have to paste these two commands into a powered Repeating Command Block pointing into a Chain Command Block. These will animate our portal.
```
execute if entity @e[type=marker,scores={portal_animate=..3}] run scoreboard players add @e[type=marker,scores={portal_animate=-999..999}] portal_animate 3
```
```
execute as @e[type=marker,scores={portal_animate=1..3}] at @s run setblock ~ ~ ~ nether_portal[axis=z]
```

To play your animation, simply run this command either in chat or in an Impulse Command Block. It will subtract all of the Marker's `portal_animate` scores to make them negative, which allows the animation commands above to activate.
```
execute unless entity @e[type=marker,scores={portal_animate=..0}] run scoreboard players remove @e[type=marker,scores={portal_animate=-999..999}] portal_animate 180
```

If you notice that the portals are facing the wrong direction, you can change `[axis=z]` in the Chain Command Block to `[axis=x]`, and play the animation again.

Now to add the particle effect, we need to find the coordinate of the center of the portal, and paste it into the `target` field in both of the commands below, which will go in two more Chain Command Blocks attached to our existing Chain Command Block and Repeating Command Block.
```
execute as @e[type=marker,scores={portal_animate=-4..-1}] at @s run particle trail{target:[<x>,<y>,<z>],color:64511,duration:15} ~ ~ ~ 0.5 0.5 0.5 0 5
```
```
execute as @e[type=marker,scores={portal_animate=-4..-1}] at @s run particle trail{target:[<x>,<y>,<z>],color:16777215,duration:10} ~ ~ ~ 0.5 0.5 0.5 0 2
```

So for instance, if the center of your portal is at (-1871.5, -31, 208), your `target` will look like this: `target:[-1871.5,-31,208]`

In the video, I activate the portal by placing a Music Disc into a Jukebox, and this can easily be accomplished by pasting the command used to play the animation into a Command Block directly under a Jukebox, which gives out a Redstone Signal when it has a Music Disc inside.
