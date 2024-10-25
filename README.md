# Write Everywhere - Cities Skylines 2 edition

This repository contains information about the usage and a lot of sample layouts for the Write Everywhere mod for Cities Skylines 2. Below here there are a detailed explanation about the mod usage, also there are information for asset creators that want to do assets compatible with Write Everywhere features.

# This repository structure

There are 3 folders here:
 - Default Atlases: contains some utility images used in asset & importable layouts. Copy the subfolders you need in the sprite library folder of the mod - you can find a button at mod's options menu that leads you there.
 - Asset Layouts: contains themed subfolders that add features to vanilla assets, like **vehicle custom plates positions for vanilla assets** and **gas stations' price indicators**. Copy whole folders into prefab layouts folder of the mod (you can find a button leading there at the WE's options menu).
 - Importable Layouts: contains some prefabs layouts that can be imported as City Layout (via WE button at game's UI). Usage examples are the **vehicle custom plates layout definition**. Notice that some of them also might need the WE

# General instructions for using this mod
## Enabling the mod
The mod have two accesses:
- Using the Ctrl+Shift+W to access the WE tool, you will be able to pick any vehicle, building, prop or tree to edit their individual WE layouts
- At the WE Button in the top left button bar (the circled W) , it will detail the settings stored along the city. For now it have two tabs: City Layouts and CIty Fonts

## Adding layout items

When selecting the asset to be edited, you can use the buttons in the below part of Hierarchy Window . The Plus icon will have options to add empty items (at root, or if any node is selected also will display options for adding as child or as sibling - this last if the current selection does have a parent layout item).
Also there are options to save and load templates from XML or from city layouts templates. Also there's an option to export the layout as *prefab default template* (explained ahead).
At the right of this window there's a cut, copy, paste and delete buttons. The paste buttons also displays a menu to select where to paste, like the add button have.

## Editing layout items

There are 4 types of layout items:
- Text: They can use a city installed font - previously uploaded at font tab at WE button screen - and can display a static or dynamic text using formulaes (explained ahead)
- Image: They can display an image that is at mod atlases folder. Each subfolder is considered as being an atlas, grouping the images inside. The images might not be larger than 512x512 for now and don't support special maps (yet - normals and other maps support may be added in the future). It also can use a formulae to determine which image will be shown. For now, the atlases aren't stored at savegames like the fonts are.
- Placeholder: It marks position for a city layout template. An example usage is car plates, you can add the placeholder at assets to setup where they shall appear and when a city layout with that name get added to the city layout template list all placeholders will be filled with that content. The placeholder layout name is always static.
- White Texture: This creates a white plane that can be used for anything you want, an example of use is to create walls to add decals afterwards (read about decals support ahead)

### Coloring and Shading

At this build, it's possible to edit many shader parameters, like color, emissive color, roughness, etc. Go to appearance settings button in the bottom of the WE tool options when a layout node is selected to open the window.
Also there's a window for decals support. By default, it accepts vehicles decals (called in the mod as *Decal filter for dynamic objects*) to avoid the shader to capture unwanted area shaders, but also can be setted up to accept road, building and any other category of decals. This can open possibilities to use the planes as wall or roofs with detailing

### Sizing

The unit used for sizing at mod UI is centimeter (cm) since the layouts are targeted for small stuff. All layout items supports sizing, but each one behaves a little different due their nature:
- Text: You can define the height of the font (line size) and the width distortion. Also you can determine the maximum width - when overflow it squashes the text, other effects may be added later
- Image: All images will have their height as being considered 100cm (1m) as default. By default, changing the height will proportionally changes the width to keep the aspect ratio, but there's an option allowing to edit both directly
- Placeholder: The size here is just for editor purposes, since it's not applied to the generated layout. It can help to check what will be the looking of the generated layout when one get applied.
- White Texture: It sets directly the size of the plane, starting as 100x100cm (1x1m)
 
## The WE settings window (by clicking on circled W button)

There have 3 tabs by now:

### City layouts tab

It lists all layouts that are saved in the city. At the list, there's a button to add items from XML. You can add files from anywhere in your PC, but it will start navigation from the layouts folder in the WE's ModsData place, so I recommend to leave your layouts there.

When selecting an item in the list, some actions will be able to be done, like renaming, duplicating and removing the layout from the city. Also will have a button to export it as XML. *In the future, there will have a preview of the layout too*

For the sake of performance, the layout names must be composed of alphanumeric or underscores only (case insensitive), and their length must be less than 30 characters.

### City fonts tab

It lists all fonts installed in the city, or required by any city layout. Fonts required by city layouts that don't have a corresponding source at city fonts will look like the default font.

There's a button to import the font from a file. The format accepted by the mod is the TTF font. You can add files from anywhere in your PC, but the window will start navigation from the Fonts folder inside the WE's ModsData place, so I recommend to add the TTF you will use there.

When selecting a font, it will display some actions (rename, duplicate and remove) and a preview will be shown displaying the font. You can type a text in the input field above the preview to see how the font behaves.
The WE renderer have a smart resolution of missing glyphs and always will try to display a glyph, even if the original one is missing. As practical example, if the glyph for the letter "Á" (Uppercase A with acute accent) doesn't exists in the font, it will try to decompose the glyph (look for NFKD normalization for more details) and will try to find the decomposed glyphs individually. In this example, it will decompose to "A" + "´". Having the "A" glyph, the renderer will draw it at final mesh - and will ignore the rest of decomposition.
The above behavior **isn't** displayed at preview, and will may show the missing glyph as a empty square.

For the sake of performance, the font names must be composed of alphanumeric or underscores only (case insensitive), and their length must be less than 30 characters.

### City atlases tab

In this tab you can import a whole atlas to inside the current savegame. It will increase the savegame size but will make the city independent from atlases loaded from the sprites library folder. It's useful if you want to share your city with your custom layouts.

The list will show all the atlases currently stored in the savegame followed by all other atlases loaded from the sprites folder. If there's atlases with the same name in both groups, the savegame atlas version will be shown when redering the mod layouts. Also there's a preview showing the atlas content, it may freeze the game for a while when selecting huge atlases.

## Placeholder naming standards

All standard names for placeholder will follow the pattern `_XXXXXXXXX_YYYYYYYYY` being `XXXXXXXXX` representing a group of placeholders and `YYYYYYYYY` representing a specific usage - all them in uppercase. Some patterns already proposed are below.
It's possible to use the same model for many different placeholders by just duplicating them for all names applicable.

### Group `VEHICLEPLATE`

This group holds layouts for vehicle plates. Asset makers can use it to hold position for a player layout in their vehicles.

- `_VEHICLEPLATE_CAR`: Plate used for common citizen cars.
- `_VEHICLEPLATE_MOTORCYCLE`: Plate used for common citizen motorcycles.
- `_VEHICLEPLATE_BICYCLE`: Plate used for common citizen bicycles (when game have support for that).
- `_VEHICLEPLATE_TRUCK`: Plate used for trucks.
- `_VEHICLEPLATE_BUS`: Plate used for buses.
- `_VEHICLEPLATE_TAXI`: Plate used for taxis.
- `_VEHICLEPLATE_SERVICE`: Plate used for general city services vehicles (not emergencial).
- `_VEHICLEPLATE_EMERGENCY`: Plate used for emergencial city services, like police cars, ambulances and firetrucks.

Other groups may be created by standard at any time, so avoid using this pattern for your own layouts.

## Formulae values

Formulae is a feature to allow getting any value from any component of the game. It allows to navigate between entities and components of ECS used in the game, and also can call some functions.
WE have some built-in utility functions that may be overridden by other mods. Search for them at the formulae window by navigating `Static Method -> Mod -> BelzontWE -> BelzontWE` and reading their methods names in each class.

Notice that Formulae can be applied also to styles properties, and a lot more will be added as builtin functions. Other mods can also provide compatible formulaes, as well also can rewrite behavior of existing builtin formulaes. 

An effective example of a bultin function rewrite is that the Addresses mod will override the function that generates the car plates due it being able to manage that information.

### Advanced use - composing a pipeline
For advanced users, is recommended to get some introduction about Unity ECS system and also to use the Scene Explorer mod by krzychu124 to check what are the components available at the current 

#### Basic workflow

When building a formulae, it always start with the Entity of the selected object (by example, a Car). Then you can:
- Select a component from the Entity (it will list all registered at game, use Scene Explorer to have details about which ones are available at this object)
- to run a static method that receives an Entity as single parameter.
After selecting any of them, the pipeline will show the current type of the item. If it still being an Entity, you will be able to do the same again. If it's not, you can:
- Run a static method that receives that type as single parameter
- Load a property of the object
- Load a field of the object
- Run a zero-parameter instance method of the object

The flow repeats "eternally". The result of the pipeline will always be a String. If the last item doeesn't returns a String, it will do an automatic conversion - which is discouraged.

## Working with WE XML files

### Auto loading default templates for prefabs

The layouts that should be automatically loaded for prefabs shall be under the prefabs folder (`<Game AppData Folder>\ModsData\Klyte45Mods\WriteEverywhere\prefabs`) and all them must follow the naming pattern: `<Prefab internal name>.wedefault.xml`. The mod will search all files with these names recursively under that folder and will load all them, merging their layouts. It can be useful for separating the default layouts parts by subfolders (example: one folder for vehicle plates locations, another for extra text of buses, etc )

### Exporting as prefab default layout

To export a node as prefab layout, at hierarchy window click on the **parent layout item** and then go to save button, select the option **Export selected as prefab default layout** and a file will be generated at root of the prefabs folder. **IT WILL OVERRIDING EXISTING FILES**, so avoid letting the default files at root.
Notice that the root layout item **will be ignored** when writing the XML file. So don't use it to add any effective stuff. Keep it position and rotation at 0 too to avoid misplacements.
> **NOTE: A known bug is that saving a new prefab default layout is making the game to crash after creating the file. Looking on it already.**

### Exporting as common layout

Differently of the prefab default layout, the root node will be exported in this case. It will also export to the prefabs folder above but the name can be input by the user. The name pattern is also different: `<user chosen name>.welayout.xml`. If a file with that name already exists, the mod will append a number in the front of the filename until it get to an not used name.

### The XML file content

***SOON***