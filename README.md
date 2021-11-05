# Allure
Allure is a custom enchants plugin built for 1.17.1.
Allure registers its enchants through NMS unlike other plugins that utilize the items lore, persistent data container or only extending the enchantment class. This requires having to muck around with altering lore, anvils and all the other good stuff. With NMS registration comes native anvil, enchantment table and treasure support.

A caveat of registering custom enchants is that the client has no translation for the enchant. This means that the enchant cannot be natively shown on the item without a resource pack or mods. Instead, Allure uses lore.. Via packets! Thus the actual item on the server isn't affected. 

## Caveats
Creative mode is messy when it comes to using packets for displaying the lore as the client in creative mode can do anything with items and have it update on the server. To fix this, those packets are intercepted and if the item has any enchantment lore on it then the lore will be removed. 

## Dependencies
- ProtocolLib


## Creating Enchants
In order to create enchants you'll need to extend the AllureEnchant class. The AEnchant annotation then can be used to define the enchantments properties.
```java
@AEnchant(name = "boom", displayName = "Boom", maxLevel = 5, rarity = Enchantment.Rarity.RARE, isTreaure = true, target = EnchantmentTarget.TOOL)
public class BoomEnchant extends AllureEnchant {

    @Override
    public void onBlockBreak(@NotNull final Player player, 
                             @NotNull final Block block, 
                             final int level, 
                             @NotNull final BlockBreakEvent event) {
        player.playSound(player.getLocation(), Sound.ENTITY_GENERIC_EXPLODE, 1.0f, 1.0f);
    }
}
```

### Registering
All enchants that have been created need to be registered. This can be done by creating ONE instance of the enchantment, then parsing it to the enchantment registery.
