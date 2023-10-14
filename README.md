import org.bukkit.Bukkit;
import org.bukkit.Material;
import org.bukkit.entity.Player;
import org.bukkit.event.EventHandler;
import org.bukkit.event.Listener;
import org.bukkit.event.inventory.InventoryClickEvent;
import org.bukkit.inventory.Inventory;
import org.bukkit.inventory.ItemStack;
import org.bukkit.plugin.java.JavaPlugin;

public class ShopPlugin extends JavaPlugin implements Listener {
    private Inventory shopInventory;

    @Override
    public void onEnable() {
        getServer().getPluginManager().registerEvents(this, this);
        createShopInventory();
    }

    private void createShopInventory() {
        shopInventory = Bukkit.createInventory(null, 27, "Shop");

        // Add items to the shop inventory
        shopInventory.addItem(new ItemStack(Material.DIAMOND, 5));
        shopInventory.addItem(new ItemStack(Material.GOLD_INGOT, 10));
        shopInventory.addItem(new ItemStack(Material.IRON_INGOT, 15));
    }

    @EventHandler
    public void onInventoryClick(InventoryClickEvent event) {
        if (event.getView().getTitle().equals("Shop")) {
            Player player = (Player) event.getWhoClicked();
            event.setCancelled(true);

            ItemStack clickedItem = event.getCurrentItem();
            if (clickedItem == null || clickedItem.getType() == Material.AIR) return;

            // Check player's balance or implement a currency system
            // For simplicity, we assume the player has enough currency to make the purchase
            if (player.getInventory().firstEmpty() != -1) {
                player.getInventory().addItem(clickedItem);
                player.sendMessage("You've purchased " + clickedItem.getAmount() + " " + clickedItem.getType());
            } else {
                player.sendMessage("Your inventory is full. You can't make the purchase.");
            }
        }
    }
}
