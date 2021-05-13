# Allure
Allure is a custom enchants plugin built for 1.16.5.
Allure registers its enchants through NMS unlike other plugins that utilize NBT, PDC (Persistent Data Container) and/or lore which can be quite limiting on what can be done. With NMS registration comes native anvil, enchantment table and treaure support.

It also utilizes packets to display the enchantments. Packets are intercepted and changed to the client depending on the enchantments.

## Dependencies
- ProtocolLib


## Creating Enchants
The following is an example which will play an explosion sound on block break.
Annotations are used to store the the enchantment data and options.
```java
@AEnchant(name = "boom", displayName = "Boom", maxLevel = 5, rarity = Enchantment.Rarity.RARE, isTreaure = true, target = EnchantmentTarget.TOOL)
public class BlossomEnchant extends AllureEnchant {

    @Override
    public void onBlockBreak(@NotNull final Player player, 
                             @NotNull final Block block, 
                             final int level, 
                             @NotNull final BlockBreakEvent event) {
        player.playSound(player.getLocation(), Sound.ENTITY_GENERIC_EXPLODE, 1.0f, 1.0f);
    }
}
```
