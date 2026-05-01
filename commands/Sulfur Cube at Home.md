These commands allow you to create a very basic version of the Sulfur Cube, as seen in [this video](https://youtube.com/shorts/IJ6KRYVn38s). They were created for 26.1. If you have any issues, feel free to join my Discord server: https://discord.gg/EBEBtBVKCK

First of all, you'll need to place in a Repeating Command Block and 8 Chain Command Blocks (9 total), with the arrows facing into each other starting from the Repeating Command Block. Make sure all blocks are powered.

Then in each Command Block, starting with the Repeating Command Block, paste these commands in order.
```
execute as @e[tag=sulfur_cube] at @s on passengers run rotate @s ~ 0
```
```
execute as @e[tag=sulfur_cube] at @s if entity @n[type=item,distance=..1.25] positioned ^ ^0.25 ^1.75 run summon item ~ ~ ~ {PickupDelay:20s,Item:{id:stone},Motion:[0,0.2,0]}
```
```
execute as @e[tag=sulfur_cube] at @s if entity @n[type=item,distance=..1.25] positioned ^ ^0.25 ^1.75 on passengers run item replace entity @n[type=item] contents from entity @s[tag=sulfur_cube_item] contents
```
```
execute as @e[tag=sulfur_cube] at @s if entity @n[type=item,distance=..1.25] on passengers run item replace entity @s[tag=sulfur_cube_item] contents from entity @n[type=item,distance=..1.25] contents
```
```
execute as @e[tag=sulfur_cube] at @s run kill @n[type=item,distance=..1.25]
```
```
execute as @n[type=pig,nbt={HurtTime:9s}] store result entity @s Motion[0] double 0.001 run data get entity @s Motion[0] 4000
```
```
execute as @n[type=pig,nbt={HurtTime:9s}] store result entity @s Motion[2] double 0.001 run data get entity @s Motion[2] 4000
```
```
execute as @e[tag=sulfur_cube_item] if items entity @s contents poisonous_potato on vehicle run kill @s
```
```
execute as @e[tag=sulfur_cube_display] unless predicate {condition:entity_properties,entity:this,predicate:{vehicle:{}}} run kill @s
```

Finally, to summon your Sulfur Cube, paste this command into a regular Command Block (orange one, also known as an Impulse Command Block) and activate it!
```
summon pig ~ ~1 ~ {attributes:[{id:movement_speed,base:0}],active_effects:[{id:resistance,amplifier:-1,duration:-1,show_particles:0},{id:invisibility,amplifier:-1,duration:-1,show_particles:0}],Silent:1,Tags:[sulfur_cube],DeathLootTable:empty,Passengers:[{id:item_display,item:{id:player_head,components:{profile:{properties:[{name:textures,value:ewogICJ0aW1lc3RhbXAiIDogMTc3NDkzMzgxOTk5NywKICAicHJvZmlsZUlkIiA6ICIwZThiMmE3ZjdmNmI0MTdiYTQ3OGQxMTZkMWJiMzI1OCIsCiAgInByb2ZpbGVOYW1lIiA6ICJibG9ja2VybG9ja2VyIiwKICAic2lnbmF0dXJlUmVxdWlyZWQiIDogdHJ1ZSwKICAidGV4dHVyZXMiIDogewogICAgIlNLSU4iIDogewogICAgICAidXJsIiA6ICJodHRwOi8vdGV4dHVyZXMubWluZWNyYWZ0Lm5ldC90ZXh0dXJlL2E0NjllMDcyMTJmYTk3MDQ2NjNhZjU3NjVjZjUzZDg0OTUxNWNmZmM1OWYwMmEyMDc2ZjZkZmM3MjQwMjBlZGUiCiAgICB9LAogICAgIkNBUEUiIDogewogICAgICAidXJsIiA6ICJodHRwOi8vdGV4dHVyZXMubWluZWNyYWZ0Lm5ldC90ZXh0dXJlL2Y5YTc2NTM3NjQ3OTg5ZjlhMGI2ZDAwMWUzMjBkYWM1OTFjMzU5ZTllNjFhMzFmNGNlMTFjODhmMjA3ZjBhZDQiCiAgICB9CiAgfQp9}]}}},teleport_duration:1,item_display:fixed,transformation:[2,0,0,0,0,2,0,-0.35,0,0,2,0,0,0,0,1],Tags:[sulfur_cube_texture,sulfur_cube_display]},{id:item_display,teleport_duration:1,item_display:fixed,transformation:[2.05,0,0,0,0,2.05,0,-0.35,0,0,2.05,0,0,0,0,1],Tags:[sulfur_cube_item,sulfur_cube_display]}]}
```

The Sulfur Cube will be invulnerable, and if you drop blocks onto it, it will absorb them. Unfortunately this Sulfur Cube doesn't have special properties for each block, but at least it's super bouncy.

To remove the Sulfur Cube, just drop a Poisonous Potato on it.
