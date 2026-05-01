These commands add Barrelporters to the game, as seen in [this video](https://youtube.com/shorts/t8jcq8QVPzU). This guide first explains how they work, and then how you can add them to your own world. The commands were made in 26.2-snapshot-5. If you have any issues, feel free to join my Discord server: [https://discord.gg/EBEBtBVKCK](https://discord.gg/EBEBtBVKCK)

By dropping an Eye of Ender on a Barrel, you create a "Sender Barrelporter", and by dropping an Ender Pearl on a Barrel, you create a "Receiver Barrelporter". Any item placed in a Sender Barrelporter will get teleported to a random Receiver Barrelporter, if there are multiple Receivers.

Items can only be teleported between Barrels which have the same name, allowing you to link Barrelporters to each other by just renaming the Barrel in an Anvil. So if there is only one Sender named "Storage Room" and only one Receiver named "Storage Room", you can easily send items from one place to another without affecting any other Barrelporters with different names.

To add Barrelporters to your world, first, run this command in chat to create a scoreboard objective that will control the teleportation cooldown of the Barrels.
```
/scoreboard objectives add barrelporter_cooldown dummy
```

Next, paste these commands into a Repeating Command Block pointing into 29 Chain Command Blocks (29 total) all with their arrows pointing to the next Command Block. They must all be either powered by Redstone or set to "Always Active" instead of "Needs Redstone".
```
execute as @e[type=item] if data entity @s Thrower if items entity @s contents ender_eye at @s positioned ~ ~-0.1 ~ if block ~ ~ ~ barrel align xyz positioned ~0.5 ~0.5 ~0.5 store result entity @s data.kill byte 1 unless entity @e[type=item_display,tag=barrelporter_root,distance=..0.1] run summon item_display ~ ~ ~ {item:{id:ender_eye},brightness:{sky:15,block:15},transformation:[1,0,0,0,0,1,0,0,0,0,16.01,0,0,0,0,1],Tags:[barrelporter,barrelporter_root,barrelporter_sender,new],Passengers:[{id:item_display,item:{id:ender_eye},brightness:{sky:15,block:15},transformation:[1,0,0,0,0,1,0,0,0,0,16.01,0,0,0,0,1],Tags:[barrelporter],Rotation:[90,0]},{id:item_display,item:{id:ender_eye},brightness:{sky:15,block:15},transformation:[1,0,0,0,0,1,0,0,0,0,16.01,0,0,0,0,1],Tags:[barrelporter],Rotation:[0,90]}]}
```
```
execute as @e[type=item] if data entity @s Thrower if items entity @s contents ender_pearl at @s positioned ~ ~-0.1 ~ if block ~ ~ ~ barrel align xyz positioned ~0.5 ~0.5 ~0.5 store result entity @s data.kill byte 1 unless entity @e[type=item_display,tag=barrelporter_root,distance=..0.1] run summon item_display ~ ~ ~ {item:{id:ender_pearl},brightness:{sky:15,block:15},transformation:[1,0,0,0,0,1,0,0,0,0,16.01,0,0,0,0,1],Tags:[barrelporter,barrelporter_root,barrelporter_receiver,new],Passengers:[{id:item_display,item:{id:ender_pearl},brightness:{sky:15,block:15},transformation:[1,0,0,0,0,1,0,0,0,0,16.01,0,0,0,0,1],Tags:[barrelporter],Rotation:[90,0]},{id:item_display,item:{id:ender_pearl},brightness:{sky:15,block:15},transformation:[1,0,0,0,0,1,0,0,0,0,16.01,0,0,0,0,1],Tags:[barrelporter],Rotation:[0,90]}]}
```
```
execute as @e[type=item_display,tag=barrelporter_root,tag=new] at @s run playsound block.vault.activate block @a ~ ~ ~
```
```
execute as @e[type=item_display,tag=barrelporter_root,tag=new] at @s run particle portal ~ ~ ~ 0 0 0 0.5 50
```
```
execute as @e[type=item_display,tag=barrelporter_root,tag=new] at @s if data block ~ ~ ~ CustomName run data modify entity @s data.barrelporter.name set from block ~ ~ ~ CustomName
```
```
execute as @e[type=item_display,tag=barrelporter_root,tag=new] at @s unless data block ~ ~ ~ CustomName run data modify entity @s data.barrelporter.name set value "Barrel"
```
```
tag @e[type=item_display,tag=barrelporter_root,tag=new] remove new
```
```
execute unless data storage barrelporter:temp all.sending as @e[type=item_display,tag=barrelporter_sender,scores={barrelporter_cooldown=-1}] at @s if data block ~ ~ ~ Items[0] store success storage barrelporter:temp all.sending byte 1 run tag @s add barrelporter_potential_sending
```
```
tag @e[type=item_display,tag=barrelporter_potential_sending,limit=1,sort=random] add barrelporter_sending
```
```
execute as @e[type=item_display,tag=barrelporter_sending] at @s run data modify entity @s item.components."minecraft:bundle_contents" append from block ~ ~ ~ Items[0]
```
```
execute if entity @e[type=item_display,tag=barrelporter_sending] as @e[type=item_display,tag=barrelporter_receiver,scores={barrelporter_cooldown=-1}] run data modify entity @s data.barrelporter.check.name set from entity @n[type=item_display,tag=barrelporter_sending] data.barrelporter.name
```
```
execute if entity @e[type=item_display,tag=barrelporter_sending] as @e[type=item_display,tag=barrelporter_receiver,scores={barrelporter_cooldown=-1}] store success entity @s data.barrelporter.check.not_target byte 1 run data modify entity @s data.barrelporter.check.name set from entity @s data.barrelporter.name
```
```
execute if entity @e[type=item_display,tag=barrelporter_sending] run tag @e[type=item_display,tag=barrelporter_receiver,nbt={data:{barrelporter:{check:{not_target:0b}}}}] add barrelporter_potential_target
```
```
execute as @e[type=item_display,tag=barrelporter_potential_target] at @s if data block ~ ~ ~ Items[26] run tag @s remove barrelporter_potential_target
```
```
tag @e[type=item_display,tag=barrelporter_potential_target,limit=1,sort=random] add barrelporter_target
```
```
execute as @e[type=item_display,tag=barrelporter_sending] at @e[type=item_display,tag=barrelporter_target] run loot insert ~ ~ ~ loot {pools:[{rolls:1,entries:[{type:"minecraft:slots",slot_source:{type:"minecraft:contents",slot_source:{type:"minecraft:slot_range",source:"this",slots:"contents"},component:"minecraft:bundle_contents"}}]}]}
```
```
execute if entity @e[type=item_display,tag=barrelporter_target] at @e[type=item_display,tag=barrelporter_sending] run data remove block ~ ~ ~ Items[0]
```
```
scoreboard players set @e[type=item_display,tag=barrelporter_sending] barrelporter_cooldown 10
```
```
tag @e[type=item_display,tag=barrelporter_sending] remove barrelporter_sending
```
```
tag @e[type=item_display,tag=barrelporter_target] remove barrelporter_target
```
```
tag @e[type=item_display,tag=barrelporter_potential_sending] remove barrelporter_potential_sending
```
```
tag @e[type=item_display,tag=barrelporter_potential_target] remove barrelporter_potential_target
```
```
execute as @e[type=item_display,tag=barrelporter_sender] run data remove entity @s item.components."minecraft:bundle_contents"
```
```
execute as @e[type=item_display,tag=barrelporter_receiver] run data remove entity @s data.barrelporter.check
```
```
data remove storage barrelporter:temp all
```
```
execute as @e[type=item_display,tag=barrelporter_root] unless score @s barrelporter_cooldown matches ..-1 run scoreboard players remove @s barrelporter_cooldown 1
```
```
execute as @e[type=item_display,tag=barrelporter] at @s store result entity @s data.kill byte 1 unless block ~ ~ ~ barrel
```
```
execute as @e[type=item_display,tag=barrelporter_sender,nbt={data:{kill:true}}] at @s run loot spawn ~ ~ ~ loot {pools:[{rolls:1,entries:[{type:item,name:ender_eye}]}]}
```
```
execute as @e[type=item_display,tag=barrelporter_receiver,nbt={data:{kill:true}}] at @s run loot spawn ~ ~ ~ loot {pools:[{rolls:1,entries:[{type:item,name:ender_pearl}]}]}
```
```
kill @e[nbt={data:{kill:true}}]
```

