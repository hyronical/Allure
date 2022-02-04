# Allure
Allure is a custom enchants plugin built for 1.18.1.
Allure registers its enchants through NMS unlike other plugins that directly utilize the items lore, PDC or only extending the enchantment class. All of the following require handling anvil merging, enchantment tables, etc. on your own. 

A caveat of registering custom enchants is that the client has no translation for the enchant. This means that the enchant cannot be natively shown on the item without clientside mods. Instead, Allure uses lore.. via packets! Thus the actual item on the server isn't affected. 

This allows for native anvil, enchantment table, treasure (natural spawning chests) and more!

## Caveats
Enchants will not show in creative mode. This is due to creative allowing players to essentially create or modify an item based on what their client sees.

## Dependencies
- ProtocolLib


## Creating Enchants
Allure does not come with a lot of premade enchants, that's up to you to implement.
In order to create enchants you'll need to extend the AllureEnchant class. The AEnchant annotation then can be used to define the enchantments properties.
There's a variety of event handlers to use for your enchants such as onBlockBreak, onPlayerAttack, onTridentThrow, etc.
```java
@AEnchant(id = "boom", display = "Boom", maxLevel = 5, rarity = Rarity.RARE)
public class BoomEnchant extends AllureEnchant {
    // Play an explosion sound when a block is broken
    @Override
    public void onBlockBreak(@NotNull final Player player, 
                             @NotNull final Block block, 
                             final int level, 
                             @NotNull final BlockBreakEvent event) {
        player.playSound(player.getLocation(), Sound.ENTITY_GENERIC_EXPLODE, 1.0f, 1.0f); // Play explosion sound
        if (level == 5) 
            player.sendMessage("Level 5! That's epic."); // Send message if level is 5
    }
}
```

### Registering
All enchants that have been created need to be registered. This can be done by running register() on the instance of your enchant. Do note that you can only have ONE instance of an enchantment.
