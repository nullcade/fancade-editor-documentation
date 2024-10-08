# Fancade Editor (EXPERIMENTAL)

[fancade-editor.onrender.com](https://fancade-editor.onrender.com/)

an unofficial editor for fancade games by NULLCADE

this editor is not a replacement to the original built-in editor in fancade, but just a way for creators to intract with the fancade games directly with much less limits

> [!WARNING]
> this project may result in your ban if used in the wrong way (or the right way). please make sure that your game is stable enough before publishing it.

> [!NOTE]
> this project is under a proprietary license and it's closed source, but we hope that we make it open source (under GPLv3), or at least "source available" (if there is any legal conflicts)

# The Editor

the editor has 3 tabs with different purposes which are:

## Info Tab

as it seems like, this tab corresponds to editing the game info, but also actually importing the game.

there are 2 sections inside of this tab:

### Game Info

in the info tab, you will see 3 text inputs controlling the game's **Title**, **Author** and **Description**, just like you can in the original editor. however, fancade editor by NULLCADE removed the limit of which characters can be used inside of each text input.

there is also a switch which let's you type up to 255 characters inside of the description instead of the 137 characters

> [!WARNING]
> using forbidding characters or larger description can result in a ban from Fancade

there is also a hidden section which can be revealed by using the arrow on the right. pressing it will reveal **App Version** and **ID Offset**.

**App Version** is the version of the Fancade Engine for Fancade to convert old games to new version in case of a change in the Engine. (as of now, it's on version 31)

**ID Offset** is the first id which chunks are going to be assigned with. (as of now, it's on 597)  
since the game is use ids to specify the blocks in a level, it have to also store the custom blocks with specific ids. the ids of built-in blocks and custom blocks have no difference and the only way for the game to distinguish them is by using the **ID Offset**. any id bellow that is considered built-in, otherwise, it's custom.

> [!NOTE]
> apperantly the ID Offset is only used for backward compatibility with older versions of fancade, since changing it will do nothing and will be automatically reverted to the right value (which is 597 as of now)

### Game Load/Save

at first there are 2 buttons with a small sub button:

**Import**: Imports the game file or a zip file with all the games inside (for mobile users, since it exports it as a zip file).

**Export**: literally exports the game and downloads it by your browser.

We noticed that our Fancade Editor won't be good enough, since it's hard to implement professional tools inside to edit your data... so we also added **JSON** Export/Import to be used with different tools and be automated with scripts and different programming languages!

**The button next to Export**: exports a JSON file containing all the data stored in a game.

**The button next to Import**: imports a JSON file to start editing it.

> [!NOTE]
> the documentation of the JSON file is not going to be in this page and will be (hopefully) published soon...

there is also a save section where you can use to save and load all your games inside of the browser directly!

> [!WARNING]
> all the games that are saved are identified by their **Title**. any existing saved game with the same Title will be replaced when saving a new one.

the **Save** button will save the game and show it in the list bellow it

Once a game is added, it can be removed by using the trash icon button next to it.

there is also a **New Game** button which will replace the current game with an empty game and will fill up the **Title**, **Author** and **Description**.

## Chunks

Definition:
> each fancade game is split into 2 parts, header (which contains the game info) and chunks  
> each chunk can be either a level, or a block  
> a chunk can contain block data, face (voxel) data and wire data  
> each chunk can have **child** chunks which corresponds to their **parent** chunk  

in the chunks tab, you will see a list containing all chunks and a "New Chunk" button, and a fingerprint button which will copy the chunk UUID

after selecting a chunk, or creating a new one by selecting "New Chunk", you can start editing the chunk.

there are multiple inputs when editing a chunk:

### Type

the first selector is type which you can select from one of:

1. Solid Block
2. Physics Block
3. Script Block
4. Level

### Name

which specifies the name of the chunk, this can be the level name or the block name.

### Lock

Locking or Unlocking a chunk from being edited

### Collider

if the type is a block, you can set a collider which can be one of:

1. Passthrough
2. Box
3. Sphear

### Offset

> every chunk can have 8x8x8 voxels, which is the same size as a 1x1x1 block.  
> to create a block bigger than 1x1x1, you will need attach multiple chunks together.  
> this is where child chunks and Offset (the place of the chunk inside the block) come in play!

Offset can be from 0 to 3 in each axis.  

> [!TIP]
> Fancade allows any block shape in a 4x4x4 max size, which means sometimes you won't be having an x0 y0 z0 chunk, so you aren't forced to use Offset x0 y0 z0 on the parent chunk. don't worry about it...

### Blocks (Not implemented yet)

used to edit the blocks of a chunk

> [!NOTE]
> I couldn't find a good UI design to show the placed blocks in a chunk and place/break them.  
> if you have any ideas on this, please let me know.

### Faces (Voxels)

used to edit the faces of each chunk (block). the way it's used is going to be explained later

### Wires (Not implemented yet)

used to edit the wires of a chunk

> [!NOTE]
> just like the blocks, I couldn't find a good UI design to show the connected wires in a chunk and add or remove them.  
> if you have any ideas on this, please let me know.

### Limit input size

Fancade limits chunks name to 16 characters, but since we're working with raw data, we can remove the limit and add 256 characters long name to a chunk.

just disable this to get longer names

### Child Chunks

as mentioned, each chunk can have child chunks, and here you can add and remove them.

Child chunks have many similarities to parent chunks. some difference are that child chunks can't have children, and they have the same type and collider as the parent, and even tho they could have blocks and wires inside, they aren't going to be visible...

each child chunk can have **Offset** and **Faces**.

> [!NOTE]
> Blocks and Wires doesn't seem to be stored in child chunks, this was found after a recent research. the editor still going to contain these buttons until it's proven to be right

> [!NOTE]
> child chunks can store much more data than what is used by fancade, but these data still aren't available to be edited by the editor yet (name, blocks, wires, etc.)  
> same thing applies to the parent id of each chunk (each chunk can only be identified as a child if it has a parent id other than it's own id). it's not available to be edited as it have conflict with the way the editor works.  
> hopefully we soon will figure out a way to make this available too

## Script

this is the most exciting part of fancade editor to me!

this tab does something that have been requested many times to be added to fancade: Scripting

by using this tab, you can use TypeScript to code your game inside of a single script block!

this tab has 4 elements:

### Save button

Saves the code inside of the browser

### P button

Prettier, to make your code look pretty!

### Build button

turns your code into a script block, usable in Fancade

### Code Editor

a place to write your code, just like you do in vscode.

in this place, all the magic happens!

the code you're going to write is going to be just like how you connect the blocks in fancade. each script block has a function specified to it, and wires can be stored in variables.

when building the code, all the blocks specified in the code will be placed in the shape of a tower inside of a script block.

> [!TIP]
> playSound is buggy in the web version of fancade, using it deep in the code will make it go up in the script block, and those it becomes laggy.  
> please use playSound near the top of the script to make it work for web version

> [!NOTE]
> the scripting feature still doesn't have the ability to make input/output wires on a block, true functions (there are inline functions which just copies that part of code) or multiple script files.

> [!NOTE]
> the documentation of the typescript is going to be released later

> [!TIP]
> you can use the code suggestions until the documentation is released for scripting