These commands can be used to easily visualize the commands inside of Command Blocks with an automatically updating Text Display, as seen in [this video](https://youtube.com/shorts/dALL5zALJdM). These commands are confirmed to work in version 26.1, but will probably work in some previous and future versions, too. If you have any issues, feel free to join my Discord server: https://discord.blocker.locker

First, you need to give yourself a special spawn egg to spawn the Text Display. The Text Display has the `command_vision` tag so we can easily modify it later using our Command Blocks. This command can be run in chat, but if you place it in a Command Block instead to run it, just be sure to change `@s` to `@p`.
```
/give @s cod_spawn_egg[enchantment_glint_override=1,entity_data={Tags:[command_vision],billboard:vertical,id:text_display,line_width:160,shadow:1,transformation:{scale:[.25,.25,.25]}},item_model=pale_oak_hanging_sign,item_name="Command Block Reader"]
```

Next, place these two commands into a powered Repeating Command Block whose arrow is facing into a powered Chain Command Block. The first command will automatically set the text of every Text Display that has the `command_vision` tag to the command in the Command Block directly below it.
```
execute as @e[tag=command_vision] at @s run data modify entity @s text set from block ~ ~-0.5 ~ Command
```
The second command will remove any Text Displays with the `command_vision` tag that do NOT have a Command Block beneath them.
```
execute as @e[tag=command_vision] at @s unless block ~ ~-1 ~ command_block unless block ~ ~-1 ~ repeating_command_block unless block ~ ~-1 ~ chain_command_block run kill @s
```

Now if you use your special "Command Block Reader" spawn egg on top of any command block, the Text Display will appear and be automatically updated! And if you destroy the Command Block, the Text Display will disappear.
