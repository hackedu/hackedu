---
name: 'Minecraft Mod'
description: 'Make your first Minecraft mod using Forge and IntelliJ IDEA'
author: '@KaiDevrim'
img: 'https://cloud-m4x2nuz66.vercel.app/image.png'
---  

Learning to mod Minecraft is a very simple process and can help anyone learn programming. Minecraft uses the Java language which albeit old, is still very popular and learning it is still useful. This Minecraft modding workshop will go from setting up IntelliJ IDEA to making an item, creative inventory tab, and a block. The result will look something like this:  

![The end result with an inventory tab and a few items](https://cloud-m4x2nuz66.vercel.app/image.png) 

Here is the [final code](https://github.com/KaiDevrim/PlayerEvolutions/tree/workshop). This workshop should take around an hour to complete but its fun the entire time.

*Note: unlike most workshops, this workshop requires a local development environment. You need to use a computer that you're allowed to install things on. If you're using a school-issued computer or a Chromebook, this workshop may not work for you.*

*For the sake of simplicity, this workshop will assume you're using IntelliJ to code your project.*

## Part 1: Setup

The annoying thing about Minecraft development is that it requires _a lot_ of setup. In the interest of keeping this workshop short and focused on mod building, we're going to skip a lot of the setup and start from a starter project. Don't worry, though—I'll still explain what's happening in the setup process and why every part of it is necessary, so you'll still be able to make your own Minecraft mods on your own after this workshop.

First, make sure you have IntelliJ IDEA installed. If you don't, [download it here](https://www.jetbrains.com/idea/download/) first (the community edition is fine).

Next, download and unzip the starter project from [hack.af/modworkshopstarter](https://hack.af/modworkshopstarter).

You should be greeted with something like this:

![IntelliJ starter project](https://cloud-c322pijsg.vercel.app/0screen_shot_2021-02-04_at_10.05.11_am.png)

### Walking through the starter project

So what's all this stuff?

The most important thing that you can't see is Forge. Forge is the API used to make Minecraft mods. Throughout the process of making this mod, you'll be importing things from "net.minecraft" or "net.minecraftforge"—these are all methods as part of Forge that allow you to access things in Minecraft, such as blocks, items, inventory, textures, events, you name it!

<details>

<summary>How do you install Forge normally (not as part of a starter project)?</summary>

If you're going to make mods in the future, you'll have to be able to install Forge yourself. Here's how you do it:

Download the [Forge MDK for 1.15.2](http://files.minecraftforge.net/maven/net/minecraftforge/forge/index_1.15.2.html). There will be a few download links—make sure you click on the one that says "Mdk".

![Download the MDK](https://cloud-gwdhe1huj.vercel.app/image.png)

When you click on "Mdk", you will be taken to a very sketchy-looking page with a bunch of ads. Your computer will be fine, but DO NOT click on anything on the page! Wait 5 seconds, then a button that says "Skip" will appear at the top right. Click the "Skip" button to download the Forge MDK. Sadly, navigating spam and adware is normal in the Minecraft world. It's not a big deal, but it's something you should be aware of and navigate through carefully if you choose to continue mod or plugin development.

Once the Forge MDK is installed, start up IDEA. Once it's started up, click on `Open or Import`. Find the Forge MDK folder (usually called `forge` or `forge-1`) and select the file inside it called `build.gradle`. When prompted, choose `Open as Project`.

![Open As Project](https://cloud-1ijkxbdqk.vercel.app/image.png)

</details>

Next, if you expand all the folders in under the `main` folder on the left sidebar, you'll notice a _bunch_ of nested folders with some files inside them. This is the common folder structure for a Minecraft mod. If you make your own mod in the future, you'll have to make all of these folders and files yourself.

![folder structure](https://cloud-m0v4ngksl.vercel.app/0screen_shot_2021-02-04_at_10.16.51_am.png)

### The setup steps that we do need to do

We do need to do two small setup things before we can begin coding our mod.

First:

1. Click on the tab called `Gradle` at the top right corner. This will look like a super thin tab, and the `Gradle` label will be 90 degrees sideways. You will see a section pop out of the right of IntelliJ. <br>
![Click on Gradle on the side](https://cloud-beqpbpts3.vercel.app/image.png) <br>
2. Open the folder called `Tasks`
3. Open the folder called `fg_runs`
4. Double-click on `genIntelliJRuns` <br>

![Gradle Project -> Tasks -> fg_runs -> genIntelliJRuns](https://cloud-hfo336o3s.vercel.app/image.png) <br>

`Gradle` is the name of the build system we are using. It is what turns our Java code into something the compiler understands. `Tasks` is a directory of all the build actions we can use, so if we wanted to change the way the compiler saw our program then we change which build action or Task. `fg_runs` is the Forge specfic build action set and contains all the build actions for our program. 

`genIntellijRuns` tells the compiler and the program itself that it needs to go through Forge before going through the compiler. This also sets us up with our development environment with the mod automically loaded in and a test version of Minecraft is loaded when you run the program from your IDE.

Once it has been built, it should say `BUILD SUCCESSFUL` in the Build tab at the bottom.

Next, we need to rename some of the directories in the project. Take a look at your left sidebar. See how these are two directories that say `yourusername` and `modname`?

![directory list highlighting the ones we need to change](https://cloud-jnth07j1l.vercel.app/0screen_shot_2021-02-04_at_10.16.51_am.png)

The one at the top is called a package. Minecraft mods and plugins follow this package structure. Packages follow the format `com.yourusername.modname`. In IntelliJ, they're separated by periods, but these periods are actually their own nested directories.

- Right-click on the package at the top. Hover over `Refactor`, then click `Rename`. Replace `yourusername` with your username, and `modname` with `playerevolutions`. Make sure there are no spaces and everything is lowercase.
- Next, right-click on the `assets.modname` directory. Hover over `Refactor`, then click `Rename`. Replace `modname` with `playerevolutions`.

Now we're ready to start coding! 🚀

### Creating your first class

Right-click on the package near the top. Hover over `New`, then click `Java Class`. We want this class to be called the same as our mod name. Since our mod name is `playerevolutions`, name this class `PlayerEvolutions` (make sure the P and E are capitalized)

A class in Java is a blueprint that allows you to create new objects. For more information about classes [read here](https://www.w3schools.com/java/java_classes.asp)

IntelliJ should automatically open the Java class. If it doesn't, open it by double-clicking it.

Just above the `public class PlayerEvolutions` line, add:

```java
@Mod("PlayerEvolutions")
public class PlayerEvolutions {

}
```

As you type `@Mod`, IntelliJ will prompt you to import something from Forge. Hit enter to import it. In Java, this @ thing is what's known as an [interface](https://www.w3schools.com/java/java_interface.asp). Forge provides an interface for registering our mod. By putting "PlayerEvolutions" inside the parenthesis, we're specifying that that is our mod ID.

Once this happens, here's what your Java file should look like:

```java
package com.yourusername.playerevolutions;

import net.minecraftforge.fml.common.Mod;

@Mod("PlayerEvolutions")
public class PlayerEvolutions {

}
```

Inside the class (in between the curly braces), add:

```java
@Mod("PlayerEvolutions")
public class PlayerEvolutions {
  private static final Logger LOGGER = LogManager.getLogger();
  public static final String MOD_ID = "ModName";
}
```

Move your cursor onto `Logger` and `LogManager`, then type `Alt + Enter` on your keyboard to import the packages. Once you do this, two `import` statements should be added to the top of the file.

Make sure these are the import statements:

```java
import org.apache.logging.log4j.LogManager;
import org.apache.logging.log4j.Logger;
```

If the import statements are these:

```java
import java.util.logging.Logger;
import java.util.logging.LogManager;
```

❌ that is incorrect. Delete those lines and replace them with the two that include `org.apache`.

A Logger is just a method that makes it easy to log things to the console. You don't really need to know the specifics of what it does if you don't already know what it is.

Under that line, add a [constructor](https://www.w3schools.com/java/java_constructors.asp), like so:

```java
public PlayerEvolutions() {

}
```

Inside the constructor, add:

```java
public PlayerEvolutions() {
  FMLJavaModLoadingContext.get().getModEventBus().addListener(this::setup);  
  FMLJavaModLoadingContext.get().getModEventBus().addListener(this::doClientStuff);  
  MinecraftForge.EVENT_BUS.register(this);
}
```

Hit `Alt + Enter` to import `FMLJavaModLoadingContext`, as well as `MinecraftForge`, if it isn't already imported. For now, you'll see errors on `setup` and `doClientStuff`. This is because we're referencing some methods that we haven't written yet. Once we write those methods, those errors will go away.

So let's define those methods! After the constructor, add:

```java
public ModName {
  // ...code we just wrote
}

private void setup (final FMLCommonSetupEvent event) {

}
private void doClientStuff(final FMLClientSetupEvent event) {

}
```

Make sure to import `FMLCommonSetupEvent` and `FMLClientSetupEvent`.

What we just made is a very stripped-down version of the example file mod that Forge gives us. Since all we need to do in this workshop is make an item and a block, that is all the Java we need for the mod to load within Minecraft.

<details>

<summary>Here's what your class should look like so far:</summary>

```java
package com.yourname.playerevolutions;

import net.minecraftforge.common.MinecraftForge;
import net.minecraftforge.fml.common.Mod;
import net.minecraftforge.fml.event.lifecycle.FMLClientSetupEvent;
import net.minecraftforge.fml.event.lifecycle.FMLCommonSetupEvent;
import net.minecraftforge.fml.javafmlmod.FMLJavaModLoadingContext;
import org.apache.logging.log4j.LogManager;
import org.apache.logging.log4j.Logger;

@Mod("PlayerEvolutions")
public class PlayerEvolutions {
    private static final Logger LOGGER = LogManager.getLogger();
    public static final String MOD_ID = "ModName";

    public PlayerEvolutions() {
        FMLJavaModLoadingContext.get().getModEventBus().addListener(this::setup);
        FMLJavaModLoadingContext.get().getModEventBus().addListener(this::doClientStuff);
        MinecraftForge.EVENT_BUS.register(this);
    }

    private void setup (final FMLCommonSetupEvent event) {

    }
    private void doClientStuff(final FMLClientSetupEvent event) {

    }
}
```

</details>

Next, we need to edit some metadata. Go to your `src/main/resources/META-INF/` directory and open the `mods.toml` file. This file contains the metadata for your mod. You won't need to edit most of the file, but you do need to edit one thing.

Find the line that starts with `modID`. Replace `examplemod` with what you put inside the `@Mod` interface in your Java class ("PlayerEvolutions"). This is case-sensitive, so make sure it looks exactly the same!

In order to build and run Minecraft to test the mod, click on the build menu at the top and choose `runClient`. Then press `Shift-F10` or the triangle play button.

![The build menu](https://cloud-1w8zg60d9.vercel.app/0screen_shot_2021-02-03_at_6.35.14_pm.png)

## Part 2: Setting up the Registry!

That was a lot of setup—but the good news is that now we can actually start writing the mod!

Making your first item is annoying to setup but easy once you understand. 

The first step is to make a registry handler.

A Registry Handler is what Forge [describes as](https://mcforge.readthedocs.io/en/latest/concepts/registries/) making objects known to the game. We are telling Minecraft that there are new elements like blocks, items, sounds, resources and we need to load them in. Without this, Minecraft would not know what to load or how to load in the new resources.

To create one, find the package called `util` in `src/main/java/com/name/modname/`. Right-click on it and create a new class called `RegistryHandler`.

![creating the registryhandler class](https://cloud-1eh2dnafi.vercel.app/0image.png)

Inside the `RegistryHandler` class, add:

```java
public class RegistryHandler {
  public static final DeferredRegister<Item> ITEMS = new DeferredRegister<>(ForgeRegistries.ITEMS, PlayerEvolutions.MOD_ID);
}
```

Import any statements that aren't imported. Notice that you're importing the `PlayerEvolutions` class you just wrote near the end!

The `<>` syntax in this code also means that it is a `generic` type in Java and can be as `of Type`. Since we are not changing the type in this Registry Handler class we can keep it as the default type, `<>`.

Next, create a method called `init()` to initialize the creation of our items. Under the line you just added, add:

```java
public class RegistryHandler {
  public static final DeferredRegister<Item> ITEMS = new DeferredRegister<>(ForgeRegistries.ITEMS, PlayerEvolutions.MOD_ID);
  
  public static void init() {
    ITEMS.register(FMLJavaModLoadingContext.get().getModEventBus());
  }
}
```

(Make sure to import `FMLJavaModLoadingContext`)

Essentially, we are just adding our item to the Forge registry.

To finish off registering our items, go back into your main class, `PlayerEvolutions.java` and before the `MinecraftForge.EventBus` line add this to make sure your registry is loaded into the game:

```java
RegistryHandler.init();
```

Make sure to import your `RegistryHandler` class.

<details>

<summary>Not sure where to add this line?</summary>

```java
@Mod("PlayerEvolutions")
public class PlayerEvolutions {
    private static final Logger LOGGER = LogManager.getLogger();
    public static final String MOD_ID = "ModWorkshop";

    public ModWorkshop() {
        FMLJavaModLoadingContext.get().getModEventBus().addListener(this::setup);
        FMLJavaModLoadingContext.get().getModEventBus().addListener(this::doClientStuff);
        RegistryHandler.init(); // here
        MinecraftForge.EVENT_BUS.register(this);
    }
```

</details>

## Part 3: Coding your first item! 

The boring registry stuff is out of the way. Now, we can start the fun part: adding items to the game.

Go into the `RegistryHandler.java` class. Inside the class, but after the `init()` method, add:

```java
public static final RegistryObject<Item> RUBY = ITEMS.register("ruby", ItemBase::new);
```

Use `Alt + Enter` to import `RegistryObject`. You'll get an error on `ItemBase` because that is referencing a class that we haven't created yet.

<details>

<summary> Here's what your RegisteryHandler class should look like so far: </summary>

```java
package com.username.playerevolutions.util;

import com.username.playerevolutions.PlayerEvolutions;
import net.minecraft.block.Block;
import net.minecraft.item.Item;
import net.minecraftforge.fml.RegistryObject;
import net.minecraftforge.fml.javafmlmod.FMLJavaModLoadingContext;
import net.minecraftforge.registries.DeferredRegister;
import net.minecraftforge.registries.ForgeRegistries;

public class RegistryHandler {
    public static final DeferredRegister<Item> ITEMS = new DeferredRegister<>(ForgeRegistries.ITEMS, ModWorkshop.MOD_ID);
    public static void init() {
        ITEMS.register(FMLJavaModLoadingContext.get().getModEventBus());
    }
    public static final RegistryObject<Item> RUBY = ITEMS.register("ruby", ItemBase::new);
}

```

</details>

Now, let's fix that `ItemBase` error by creating our `ItemBase` class.

- Find the directory called `items` in your left sidebar.
- Right-click it and create a new class. Call it `ItemBase`.

Once, you're inside the `ItemBase` class:

- First add `extends Item` at the end of the class name.
  ```java
  public class ItemBase extends Item {
  
  }
  ```
- Import `Item` from `net.minecraft.item.Item`.
- Once you do this, you will see an error. Click on the red light bulb (you may have to hover near the left of the line to see it). Then click "Create constructor matching super". <br>
  ![create constructor matching super](https://cloud-5kx4ewe3h.vercel.app/0screen_shot_2021-02-03_at_7.05.57_pm.png)
- IntelliJ should automatically add a few new lines of code:
  ```java
  public class ItemBase extends Item {
      public ItemBase(Properties properties) {
          super(properties);
      }
  }
  ```
- Inside the parentheses of the `ItemBase` constructor, remove `Properties properties`.
- Within the `super()` method, remove `properties` and add this line:
  ```java
  super(new Item.Properties().group(PlayerEvolutions.TAB)
  ```
- You will see an error because we haven't made a TAB for our item yet.

Once you've done this, here's what the whole `ItemBase` class should look like:

```java
package com.yourusername.playerevolutions.items;

import net.minecraft.item.Item;
import net.minecraft.item.ItemGroup;
import com.yourusername.playerevolutions.PlayerEvolutions;

public class ItemBase extends Item {

    public ItemBase() {
        super(new Item.Properties().group(PlayerEvolutions.TAB));
    }
}
```

Now, go back to the `RegistryHandler` class and hit `Alt + Enter` to import `ItemBase`.

A tab in Minecraft is where you will find the item in creative mode. To fix the error, go back into your main class, `PlayerEvolutions.java`, and add this at the bottom of the class:

```java 
public static final ItemGroup TAB = new ItemGroup("playerEvolutions") { 
    @Override 
    public ItemStack createIcon() { 
        return new ItemStack(RegistryHandler.RUBY.get()); 
    }
};
```

![screenshot showing where to put this function](https://cloud-2scubjums.vercel.app/0image.png)

Import anything you need to import.

## Part 4: Making Item Textures

Find the file called `en_US.json` in `src/main/resources/lang`. Open the file. Inside, add:

```json
{
  "item.playerevolutions.ruby": "Ruby",
  "block.playerevolutions.ruby_block": "Block of Ruby",
  "itemGroup.playerevolutions": "Player Evolutions"
}
```

Next, find the file called `item.json` in the `models/item` directory. Rename it to `ruby.json`.

Inside the file, add:

```json
{ 
  "parent": "ruby/generated", 
  "textures": { 
    "layer0": "playerevolutions:items/ruby" 
  } 
} 
```

All this is doing is telling Forge that the item only has one layer.

Now run Minecraft using Shift-F10 or the triangle play button and see your item in Minecraft!

## Part 5: Making your first block! 

Making your first block is actually very simple now that we have most of the files and registries made.  

Open the `RegistryHandler.java` file. Inside of that we are going to use the same methods from before but change them up a little.

First, copy the line that has `DeferredRegister` in it and paste it right under. Replace `<Item>` with `<Block>`, and both instances of `ITEMS` with `BLOCKS`.

```java
public static final DeferredRegister<Item> ITEMS = new DeferredRegister<>(ForgeRegistries.ITEMS, PlayerEvolutions.MOD_ID);
public static final DeferredRegister<Block> BLOCKS = new DeferredRegister<>(ForgeRegistries.BLOCKS, PlayerEvolutions.MOD_ID);
```

When you import `Block`, make sure you're importing the one from Minecraft, not from anywhere else.

Next, find the line that contains `RegistryObject<Item>` and add this right under:

```java
public static final RegistryObject<Block> RUBY_BLOCK = BLOCKS.register("ruby_block", RubyBlock::new);
```

Finally, under that, create another `RegistryObject<Item>`, like so:

```java
public static final RegistryObject<Item> RUBY_BLOCK_ITEM = ITEMS.register("ruby_block", () -> new BlockItemBase(RUBY_BLOCK.get()));
```

<details>

<summary> Here's what your RegistryHandler class should look like now: </summary>

```java
public class RegistryHandler {
    public static final DeferredRegister<Item> ITEMS = new DeferredRegister<>(ForgeRegistries.ITEMS, PlayerEvolutions.MOD_ID);
    public static final DeferredRegister<Block> BLOCKS = new DeferredRegister<>(ForgeRegistries.BLOCKS, PlayerEvolutions.MOD_ID);

    public static void init() {
        ITEMS.register(FMLJavaModLoadingContext.get().getModEventBus());
        BLOCKS.register(FMLJavaModLoadingContext.get().getModEventBus());
    }

    public static final RegistryObject<Item> RUBY = ITEMS.register("ruby", ItemBase::new);
    public static final RegistryObject<Block> RUBY_BLOCK = BLOCKS.register("ruby_block", RubyBlock::new);
    public static final RegistryObject<Item> RUBY_BLOCK_ITEM = ITEMS.register("ruby_block", () -> new BlockItemBase(RUBY_BLOCK.get()));
}
```

</details>

Next, right-click on your package under the `java` directory and crate a new package called `com.yourusername.playerevolutions.blocks`.

Once you've created that, right-click on it and create two classes:

- `BlockItemBase`
- `RubyBlock`

Open the `BlockItemBase` class and add this:

```java 
public class BlockItemBase extends BlockItem { 
  public BlockItemBase(Block block) { 
    super(block, new Item.Properties().group(PlayerEvolutions.TAB)); 
  } 
} 
```

Next, open the `RubyBlock` class. Add this:

```java
public class RubyBlock extends Block {
  public RubyBlock() {
    super(Block.Properties.create(Material.IRON)
      .harvestTool(ToolType.PICKAXE)
    );
  }
}
```

The `super()` line sets the "type" of block that your new block is. `.harvestTool()` sets the type of tool that it can be mined with. You can set these to any material in the game (if you type `Material.` or `ToolType.`, IntelliJ will suggest every available item in the game). 

Now, go back to the `RegistryHandler` class and use `Alt + Enter` to import these two new classes and fix the errors.

## Part 6: Block Textures

We're almost done! The final step is to add our block texture to the game.

Find the file called `my_block.json` in the folder called `blockstates`. Inside, add:

```json
{ 
  "variants": { 
    "": { "model": "playerevolutions:block/ruby_block" } 
  } 
}
```

Next, find the file called `my_block.json` in the folder called `models/block`. Inside, add:

```json
{ 
  "variants": { 
    "": { "model": "playerevolutions:block/ruby_block" } 
  },
  "parent": "block/cube_all", 
  "textures": { 
    "all": "playerevolutions:blocks/ruby_block" 
  } 
}
```

Finally, find the file called `my_block.json` in `models/item`. Inside, add:

```json
{ 
  "parent": "playerevolutions:block/ruby_block" 
} 
```

That's it! If you start the test Minecraft client, you should see your mod in action 😎

## Hacking

The fun doesn't stop here. Here are a few examples & demos of other things you can do:

- [Ultron Block](https://github.com/devrimtech/PlayerEvolutions/tree/hackable-demo-1)
  ![](https://cloud-kl251xoy7.vercel.app/0image.png)

- [Rickroll Item](https://github.com/devrimtech/PlayerEvolutions/tree/hackable-demo-2)
  ![](https://cloud-cf16uvc03.vercel.app/0image.png)

- [Deathnote](https://github.com/devrimtech/PlayerEvolutions/tree/hackable-demo-3)
  ![](https://cloud-rhvv52dfm.vercel.app/0image.png)

Happy hacking!