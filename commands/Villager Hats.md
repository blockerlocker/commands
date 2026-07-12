The following commands will give you various Villager Hats, without requiring any outside mods, resource packs, or data packs, as seen in [this video](https://www.youtube.com/shorts/aslpXkKGd8A). These commands depend on features added in 1.21.9, so they should work in every version after that. If you have any issues, feel free to make a help post in my Discord server https://discord.blocker.locker/
```
/give @p player_head[profile={texture:"entity/villager/profession/armorer"},custom_name="Armorer Hat"]
```
```
/give @p player_head[profile={texture:"entity/villager/profession/butcher"},custom_name="Butcher Hat"]
```
```
/give @p player_head[profile={texture:"entity/villager/profession/farmer"},custom_name="Farmer Hat"]
```
```
/give @p player_head[profile={texture:"entity/villager/profession/fisherman"},custom_name="Fisherman Hat"]
```
```
/give @p player_head[profile={texture:"entity/villager/profession/fletcher"},custom_name="Fletcher Hat"]
```
```
/give @p player_head[profile={texture:"entity/villager/profession/shepherd"},custom_name="Shepherd Hat"]
```
```
/give @p player_head[profile={texture:"entity/villager/type/desert"},custom_name="Desert Villager Hat"]
```
```
/give @p player_head[profile={texture:"entity/villager/type/savanna"},custom_name="Savanna Villager Hat"]
```
```
/give @p player_head[profile={texture:"entity/villager/type/snow"},custom_name="Snow Villager Hat"]
```
```
/give @p player_head[profile={texture:"entity/zombie/drowned_outer_layer"},custom_name="Drowned Mask"]
```

Some Villager professions and types that have hats don't perfectly map to a Player Head, but I've included them in case you want to try them as well:
```
/give @p player_head[profile={texture:"entity/villager/profession/cartographer"},custom_name="Cartographer Hat"]
```
```
/give @p player_head[profile={texture:"entity/villager/profession/cleric"},custom_name="Cleric Hat"]
```
```
/give @p player_head[profile={texture:"entity/villager/profession/librarian"},custom_name="Librarian Hat"]
```
```
/give @p player_head[profile={texture:"entity/villager/profession/weaponsmith"},custom_name="Weaponsmith Hat"]
```
```
/give @p player_head[profile={texture:"entity/villager/type/swamp"},custom_name="Swamp Villager Hat"]
```
```
/give @p player_head[profile={texture:"entity/villager/type/taiga"},custom_name="Taiga Villager Hat"]
```

The `custom_name` component is used instead of the more proper `item_name` component since by default, Player Heads lose most components when placed as a block and then broken, with the only components retained being `profile`, `note_block_sound`, and `custom_name`. For the same reason, I have also omitted a proper `equippable` component to make these hats equippable on interact. Below are the original commands I made that had these components as well.
```
/give @p player_head[profile={texture:"entity/villager/profession/armorer"},item_name="Armorer Hat",equippable={slot:head,allowed_entities:player,equip_on_interact:true}]
```
```
/give @p player_head[profile={texture:"entity/villager/profession/butcher"},item_name="Butcher Hat",equippable={slot:head,allowed_entities:player,equip_on_interact:true}]
```
```
/give @p player_head[profile={texture:"entity/villager/profession/farmer"},item_name="Farmer Hat",equippable={slot:head,allowed_entities:player,equip_on_interact:true}]
```
```
/give @p player_head[profile={texture:"entity/villager/profession/fisherman"},item_name="Fisherman Hat",equippable={slot:head,allowed_entities:player,equip_on_interact:true}]
```
```
/give @p player_head[profile={texture:"entity/villager/profession/fletcher"},item_name="Fletcher Hat",equippable={slot:head,allowed_entities:player,equip_on_interact:true}]
```
```
/give @p player_head[profile={texture:"entity/villager/profession/shepherd"},item_name="Shepherd Hat",equippable={slot:head,allowed_entities:player,equip_on_interact:true}]
```
```
/give @p player_head[profile={texture:"entity/villager/type/desert"},item_name="Desert Villager Hat",equippable={slot:head,allowed_entities:player,equip_on_interact:true}]
```
```
/give @p player_head[profile={texture:"entity/villager/type/savanna"},item_name="Savanna Villager Hat",equippable={slot:head,allowed_entities:player,equip_on_interact:true}]
```
```
/give @p player_head[profile={texture:"entity/villager/type/snow"},item_name="Snow Villager Hat",equippable={slot:head,allowed_entities:player,equip_on_interact:true}]
```
```
/give @p player_head[profile={texture:"entity/zombie/drowned_outer_layer"},item_name="Drowned Mask",equippable={slot:head,allowed_entities:player,equip_on_interact:true}]
```
```
/give @p player_head[profile={texture:"entity/villager/profession/cartographer"},item_name="Cartographer Hat",equippable={slot:head,allowed_entities:player,equip_on_interact:true}]
```
```
/give @p player_head[profile={texture:"entity/villager/profession/cleric"},item_name="Cleric Hat",equippable={slot:head,allowed_entities:player,equip_on_interact:true}]
```
```
/give @p player_head[profile={texture:"entity/villager/profession/librarian"},item_name="Librarian Hat",equippable={slot:head,allowed_entities:player,equip_on_interact:true}]
```
```
/give @p player_head[profile={texture:"entity/villager/profession/weaponsmith"},item_name="Weaponsmith Hat",equippable={slot:head,allowed_entities:player,equip_on_interact:true}]
```
```
/give @p player_head[profile={texture:"entity/villager/type/swamp"},item_name="Swamp Villager Hat",equippable={slot:head,allowed_entities:player,equip_on_interact:true}]
```
```
/give @p player_head[profile={texture:"entity/villager/type/taiga"},item_name="Taiga Villager Hat",equippable={slot:head,allowed_entities:player,equip_on_interact:true}]
```

You could then use a modified version of the Player Head loot table in a data pack to ensure they maintain the `item_name` and `equippable` components when broken. Here are the steps:
1. Create a data pack with `/datapack create player_heads_retain_components "Player heads will retain the item_name and equippable components."`
2. Navigate to the newly created data pack in the `datapacks` folder of your world.
3. Open the `player_heads_retain_components` folder and then the `data` folder, and create a `minecraft` folder.
4. Open the `minecraft` folder and create a `loot_table` folder.
5. Open the `loot_table` folder and create a `blocks` folder.
6. In the blocks folder, create a text file and rename it to `player_head.json`. If you do not have file extensions enabled in your file explorer, you may accidentally create a file called `player_head.json.txt`. Google how to enable file extensions if you aren't sure.
7. In `player_head.json`, paste the text below. Then your data pack should be complete, and when you type `/reload` in-game to reload the data pack, you should be able place down the custom Player Heads, and when broken, they will retain their components!
```
{
  "type": "minecraft:block",
  "pools": [
    {
      "entries": [
        {
          "type": "minecraft:item",
          "functions": [
            {
              "function": "minecraft:copy_components",
              "include": [
                "minecraft:profile",
                "minecraft:note_block_sound",
                "minecraft:custom_name",
                "minecraft:item_name",
                "minecraft:equippable"
              ],
              "source": "block_entity"
            }
          ],
          "name": "minecraft:player_head"
        }
      ],
      "rolls": 1
    }
  ],
  "random_sequence": "minecraft:blocks/player_head"
}
```
