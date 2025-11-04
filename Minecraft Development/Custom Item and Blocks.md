# Making a custom items/blocks

## Setting up custom Texture Pack

Before making a custom item/block, you need a texture pack for it.

1. inside `resourcepacks` folder, create a folder with the name of your texture pack.

2. inside the folder, create a file named `pack.mcmeta` and put the following code inside it:

```json
{
  "pack": {
    "pack_format": 64,
    "description": "Custom Texture Pack"
  }
}
```

> [!NOTE ] 
> The `pack_format` is the version of the texture pack format. the latest version is 64, check [here](https://minecraft.fandom.com/wiki/Pack_format) for the version you need.

3. inside the folder, create a folder named `assets`.

4. inside `assets` folder, create another folder, and name it to something that identifies you.

5. inside that folder, create 3 folders: `items`, `models` and `textures`.

6. inside `models` **AND** `textures` folder, create 2 folders named: <br>
`item` and `block`.

    your file structure should look like this:

    ```
    MyTexturePack
    ├── pack.mcmeta
    └── assets
        └── <namespace>
            ├── items
            │   └── item
            │   └── block
            ├── models
            │    ├── item
            │    └── block
            └── textures
    ```

Now you can start making your custom item/block.


## Making a custom item

### Texture Pack

1. first add your texture inside your resource pack inside `assets/<namespace>/textures/item` folder.

2. then inside `assets/<namespace>/models/item` make a new json file with the name of your item and put in the following code:

    ```json
    {
      "parent": "item/generated",
      "textures": {
        "layer0": "<namespace>:item/my_item"
      }
    }
    ```

3.  inside `assets/<namespace>/items` make a new json file with the name of your item and put in the following code:

    ```json
    {
      "model": {
        "type": "minecraft:model",
        "model": "theman:item/god_apple"
      }
    }
    ```
    `"model"` will reference the json file you made in step 2.

    > [!NOTE ] 
    > if you want to test your item in game, you can use this command:
    > ``` java
    > /give @p stick[item_model="<namespace>:<your_item>"]
    > ```
    > this will give you a stick that has your texture on it.




### Code

1. make an `ItemStack` property that will be used to create your item.

    example:
    ```java
    ItemStack item = new ItemStack(Material.APPLE, 1);
    ```
    > [!NOTE ] 
    > `Material` is an enormous enum that contains all the itemsin the game.

2. give your item a custom Item Model:

    ```java
    item.setData(DataComponentTypes.ITEM_MODEL, Key.key("<namespace>", "<item_name>"));
    ```