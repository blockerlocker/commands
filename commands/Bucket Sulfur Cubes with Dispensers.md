These commands let you use Dispensers to bucket Sulfur Cubes automatically, as seen in [this video](https://youtube.com/shorts/-LXZwWP-prI). These commands were made in Java 26.2-snapshot-2. If you have any issues, feel free to join my Discord server: https://discord.blocker.locker

You'll need to place a Repeating Command Block and 11 Chain Command Blocks (12 total), with the arrows facing into each other starting from the Repeating Command Block. Make sure all blocks are powered. Then in each Command Block, starting with the Repeating Command Block, paste these commands in order.

```
execute as @e[type=item,nbt={Age:0s,PickupDelay:0s}] at @s align xyz if predicate {condition:all_of,terms:[{condition:entity_properties,entity:this,predicate:{slots:{contents:{items:bucket}}}},{condition:any_of,terms:[{condition:location_check,offsetZ:-1,predicate:{block:{blocks:dispenser,state:{facing:"south",triggered:"true"}}}},{condition:location_check,offsetZ:1,predicate:{block:{blocks:dispenser,state:{facing:"north",triggered:"true"}}}},{condition:location_check,offsetX:-1,predicate:{block:{blocks:dispenser,state:{facing:"east",triggered:"true"}}}},{condition:location_check,offsetX:1,predicate:{block:{blocks:dispenser,state:{facing:"west",triggered:"true"}}}},{condition:location_check,offsetY:1,predicate:{block:{blocks:dispenser,state:{facing:"down",triggered:"true"}}}},{condition:location_check,offsetY:-1,predicate:{block:{blocks:dispenser,state:{facing:"up",triggered:"true"}}}}]}]} if entity @e[type=sulfur_cube,dx=1,nbt=!{Size:0}] run tag @s add bucketing_sulfur_cube
```
```
execute as @e[type=item,tag=bucketing_sulfur_cube] run item replace entity @s contents with sulfur_cube_bucket
```
```
execute as @e[type=item,tag=bucketing_sulfur_cube] at @s align xyz run data modify entity @s Item.components."minecraft:sulfur_cube_content".id set from entity @n[type=sulfur_cube,dx=1,nbt=!{Size:0}] equipment.body.id
```
```
execute as @e[type=item,tag=bucketing_sulfur_cube] at @s align xyz run data merge entity @n[type=sulfur_cube,dx=1,nbt=!{Size:0}] {Health:0,DeathTime:30,Size:0}
```
```
execute as @e[type=item,tag=bucketing_sulfur_cube] store success entity @s data.delete int 1 at @s positioned ~-0.5 ~ ~ if predicate {condition:location_check,predicate:{block:{blocks:dispenser,state:{facing:east},predicates:{container:{items:{size:{max:8}}}}}}} run loot insert ~ ~ ~ loot {pools:[{rolls:1,entries:[{type:slots,slot_source:{type:slot_range,source:this,slots:contents}}]}]}
```
```
execute as @e[type=item,tag=bucketing_sulfur_cube,nbt=!{data:{delete:1}}] store success entity @s data.delete int 1 at @s positioned ~0.5 ~ ~ if predicate {condition:location_check,predicate:{block:{blocks:dispenser,state:{facing:west},predicates:{container:{items:{size:{max:8}}}}}}} run loot insert ~ ~ ~ loot {pools:[{rolls:1,entries:[{type:slots,slot_source:{type:slot_range,source:this,slots:contents}}]}]}
```
```
execute as @e[type=item,tag=bucketing_sulfur_cube,nbt=!{data:{delete:1}}] store success entity @s data.delete int 1 at @s positioned ~ ~ ~-0.5 if predicate {condition:location_check,predicate:{block:{blocks:dispenser,state:{facing:south},predicates:{container:{items:{size:{max:8}}}}}}} run loot insert ~ ~ ~ loot {pools:[{rolls:1,entries:[{type:slots,slot_source:{type:slot_range,source:this,slots:contents}}]}]}
```
```
execute as @e[type=item,tag=bucketing_sulfur_cube,nbt=!{data:{delete:1}}] store success entity @s data.delete int 1 at @s positioned ~ ~ ~0.5 if predicate {condition:location_check,predicate:{block:{blocks:dispenser,state:{facing:north},predicates:{container:{items:{size:{max:8}}}}}}} run loot insert ~ ~ ~ loot {pools:[{rolls:1,entries:[{type:slots,slot_source:{type:slot_range,source:this,slots:contents}}]}]}
```
```
execute as @e[type=item,tag=bucketing_sulfur_cube,nbt=!{data:{delete:1}}] store success entity @s data.delete int 1 at @s positioned ~ ~-0.5 ~ if predicate {condition:location_check,predicate:{block:{blocks:dispenser,state:{facing:up},predicates:{container:{items:{size:{max:8}}}}}}} run loot insert ~ ~ ~ loot {pools:[{rolls:1,entries:[{type:slots,slot_source:{type:slot_range,source:this,slots:contents}}]}]}
```
```
execute as @e[type=item,tag=bucketing_sulfur_cube,nbt=!{data:{delete:1}}] store success entity @s data.delete int 1 at @s positioned ~ ~0.5 ~ if predicate {condition:location_check,predicate:{block:{blocks:dispenser,state:{facing:down},predicates:{container:{items:{size:{max:8}}}}}}} run loot insert ~ ~ ~ loot {pools:[{rolls:1,entries:[{type:slots,slot_source:{type:slot_range,source:this,slots:contents}}]}]}
```
```
kill @e[type=item,tag=bucketing_sulfur_cube,nbt={data:{delete:1}}]
```
```
tag @e[type=item,tag=bucketing_sulfur_cube] remove bucketing_sulfur_cube
```

Don't forget to stand on each Command Block and run "/forceload add ~ ~" to make sure they stay loaded, otherwise it stops working when you get too far away! And run "/gamerule command_block_output false" so it doesn't spam the chat.
