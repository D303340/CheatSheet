# Making Text

> [! WARNING]
> This is for PaperMC, I don't know if it will work for Spigot!


## Packages

to make text, you need a couple packages:

``` java
import net.kyori.adventure.text.serializer.legacy.LegacyComponentSerializer;
import net.kyori.adventure.text.Component;
import net.kyori.adventure.text.format.NamedTextColor;
import net.kyori.adventure.text.format.TextDecoration;
```

## Code

After that, the only thing you need is to make a `serializer` 

``` java
// serializer for & codes
var serializer = LegacyComponentSerializer.legacyAmpersand();
```

now for the text itself. to make some text, you need to use `serializer.deserialize()` method

here is an example to add `lore` to an item:

``` java
// makes a new Golden Apple
ItemStack itemStack = new ItemStack(Material.GOLDEN_APPLE);
ItemMeta meta = itemStack.getItemMeta();

// serializer for & codes
var serializer = LegacyComponentSerializer.legacyAmpersand();

// add lore to item
ItemMeta meta = itemStack.getItemMeta();
meta.lore(Arrays.asList(
    serializer.deserialize("&7A shitty ass apple..."))
));
```

the `&r` is a color code, you can use `&0-9` to change the color of the text. 
there are also codes to format the text:

| Code | Format         | Description |
| ---- | ------         | ----------- |
| `&k` | Obfuscated     | adds a glitch effect to the text |
| `&l` | Bold           | makes the text bold |
| `&m` | Strikethrough  | makes the text strikethrough |
| `&n` | Underlined     | makes the text underlined |
| `&o` | Italic         | makes the text italic |
| `&r` | Reset          | resets the text to default |

*_[Here](https://minecraft.wiki/w/Formatting_codes)_* are alle the codes listed 


there is also another way to add styling to the text.

``` java
// makes a new Golden Apple
ItemStack itemStack = new ItemStack(Material.GOLDEN_APPLE);
ItemMeta meta = itemStack.getItemMeta();

// serializer for & codes
var serializer = LegacyComponentSerializer.legacyAmpersand();

// add lore to item
ItemMeta meta = itemStack.getItemMeta();

meta.lore(Arrays.asList(
    serializer.deserialize("&7A shitty ass apple...").decoration(TextDecoration.ITALIC, false)
));
```

| Method                                                | What it does                                                                                         |
| ----------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| `color(TextColor color)`                              | Set the component's text color (use `NamedTextColor` or an RGB `TextColor`).                         |
| `colorIfAbsent(TextColor color)`                      | Set the color only if no color is already defined (acts as a default).                               |
| `decoration(TextDecoration decoration, boolean flag)` | Enable (`true`) or disable (`false`) a specific decoration (eg. `ITALIC`, `BOLD`).                   |
| `decorate(TextDecoration... decorations)`             | Shortcut to enable one or more decorations (sets them to `true`).                                    |
| `style(Style style)`                                  | Replace the component's full `Style` (font, color, decorations, events).                             |
| `mergeStyle(Style style)`                             | Merge the provided `Style` into the component (keeps existing values when the new style lacks them). |
| `font(Key fontKey)`                                   | Set a custom font for the component using a resource `Key`.                                          |
