These are various commands that can be used to increase the number of items that fit in a Bundle, as seen in [this video](https://www.youtube.com/shorts/mApxhEG59ns).

**Firstly**, you could just give yourself a stack of 99 items like this to be able to store 99 items in a Bundle:
```
/give @p diamond[max_stack_size=99] 99
```

**Secondly**, you could give Bundles the ability to suck up item entities that are dropped on them by putting the following two commands in a Repeating Command Block and Chain Command Block:
```
execute as @e[type=item] if items entity @s contents #bundles at @s if entity @n[type=item,distance=0.0001..1] run data modify entity @s Item.components."minecraft:bundle_contents" append from entity @n[type=item,distance=0.0001..1] Item
```
```
execute as @e[type=item] if items entity @s contents #bundles at @s if entity @n[type=item,distance=0.0001..1] run kill @n[type=item,distance=0.0001..1]
```
Once you've done this, it can be convenient to add the following commands to three more Chain Command Blocks so Bundles display the number of item stacks stored inside them:
```
execute as @e[type=item] if items entity @s contents #bundles store result entity @s data.stack_count int 1 if data entity @s Item.components."minecraft:bundle_contents"[]
```
```
execute as @e[type=item] if items entity @s contents #bundles run data modify entity @s CustomName set string entity @s data.stack_count
```
```
execute as @e[type=item] if items entity @s contents #bundles unless data entity @s {CustomNameVisible:1b} run data modify entity @s CustomNameVisible set value 1
```
You can also use this command to summon a stream of infinite 99 Diamond stacks to more rapdily fill these Bundles:
```
summon item ~ ~-1 ~ {Item:{id:diamond,count:99,components:{max_stack_size:99}}}

```
**Thirdly**, you can use this command in a regular Impulse Command Block to cause the nearest Bundle item entity to duplicate all of its item stacks, effectively doubling the number of items inside each time:
```
execute as @n[type=item] run data modify entity @s Item.components."minecraft:bundle_contents" append from entity @s Item.components."minecraft:bundle_contents"[]
```
