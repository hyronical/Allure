# Allure
Allure is a custom enchants plugin built for 1.16.5.
Instead of other methods of creating enchants, Allure registers them straight into NMS. This means native anvil and enchantment table support.

# Creating Enchants
The following is an example which will play an explosion sound on block break.
```java
@AEnchant(name = "boom", displayName = "Boom", maxLevel = 5, rarity = Enchantment.Rarity.RARE, isTreaure = true, target = EnchantmentTarget.TOOL)
public class BlossomEnchant extends AllureEnchant {

    @Override
    public void onBlockBreak(@NotNull final Player player, @NotNull final Block block, final int level, @NotNull final BlockBreakEvent event) {
        player.playSound(player.getLocation(), Sound.ENTITY_GENERIC_EXPLODE, 1.0f, 1.0f);
    }
}
```
