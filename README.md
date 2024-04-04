# Flipper-Online
Flipper Ønline (FØ /Eff:Null/)   

![](https://github.com/Az-Net/Flipper-Online/blob/main/assets/F0.gif)

## A Flipper Zero Multiplayer Game Inspired by Digimon &amp; Megaman V-Pets

F0 is a complex cellular automata. Each Flipper Zero device acts as a self-contained digital entity with unique characteristics determined by hexadecimal code. This code influences the Flipper's appearance, mood, and stats. The game leverages these pre-programmed behaviors to create a world where Flippers interact with their environment and each other based on a set of rules. This rule-based system, combined with the Flipper's ability to access frequency interactions, hopes to achieve a level of autonomy that pushes the boundaries of traditional gaming experiences.

# Design 

The F0 entity is primarily designed using three layered components:
* a Bit-Value array stores modifiable firmware interactions
* plaintext bin files with no extension containing hexadecimal strings act as the core cells 
* a matrix array acts as both the combat grid and as the next evolution in our project, combining and processing individual cell interactions to create a more capable and unique, emergent entity.  

The application reads and writes data to- and from- bin files and interprets the firmware logic for processing components from your Flipper's SD card.

## Cells

Each cell exists as a hexadecimal string within a plaintext file, with no extension. This means that you can use the existing text viewer and hexadecimal editor apps on the Flipper Zero for modifying cells.  
Each cell consists of a Shape, a Protrusion of a shape, a Health value, a Size, and a Mood value, creating a layered, fractal-like entity.  
There are three options for each attribute, and each attribute influences the others during cell interaction.  

### Example Cell Strings
__0x157AF__  
__0x349BE__  
__0x208A0__  

(Remember: each Bit-Value category can only be used once. Refer to the [Bit-Value Array](#bit-value-array)
 below for updated firmware rules.)

## Bit-Value Array

Each hexadecimal bit value 0-F is only used once.  
The process of cell combat modifies the hexadecimal strings during interaction, eventually writing the 0 bit to Shape to denote that a cell is dead.  
Reviving a cell simply involves editing its file to remove the 0 bit from its hexadecimal string and then setting a new shape bit value within the string.  

|Bit-Value|Use|Category|
|---|---|---|
| 0 |Null|Null|
| 1 |○|Shape|
| 2 |△|Shape|
| 3 |□|Shape|
| 4 |Bump (○)|Protrusion|
| 5 |Spike (△)|Protrusion|
| 6 |Block (□)|Protrusion|
| 7 |Small|Size|
| 8 |Medium|Size|
| 9 |Large|Size|
| A |•⌣•|Mood|
| B |•_•|Mood|
| C |•︵•|Mood|
| D |Min|Health|
| E |Mid|Health|
| F |Max|Health|

For more information, refer to [Cell Processing](#cell-processing)


## The Combat Matrix

When cells are interacting, their values are copied to a matrix array for pre-processing, and for simultaneously processing multiple interactions across numerous cells per clock cycle.  

# Cell Processing 

At the most basic level, cells follow a simple roshambo model of interaction.  
○ > △ > □  
This remains true of both the Shape and Protrusion of each cell interaction.  
The smallest cells out-speed the largest cells. The medium-sized cells can out-speed the smallest cells or largest cells.  
Mood, Size, Protrusion and Health are all modifiable values: they change during cell interaction.  
If a Bit-Value for a Shape does not exist in the cell, it is considered dead (the same as a 0 Bit-Value being written).  
The Shape and Protrusion of a cell can be set to 0. Any other Bit-Value in a cell that gets set to 0 will be reverted to its minimum value.  

# NOTE: FINISH THIS SECTION, ME
First:  
* Compare Speed > Smaller Moves Sooner  
* Process Protrusion > Loser Changes Form  

Mood:  
* If Happy then hits enemy > set Protrusion as Enemy Shape
* If Happy then Hit > Neutral
* If Neutral then Hit > Sad
* If Sad then Hit > Set Protrusion 0 

Then:
* Roshambo on Main Shape > Losing Shape -1 HP

* If HP Min & Hit = Set Shape 0 (dead)
* If HP Max & Hits enemy > get bigger

# Core Gameplay Loop

The only current user interactions involve editing the cells between grid combat, scanning them as they're cloning, and healing the currently scanned cell during combat.

# Hardware Add-ons

### Malveke

### Pi 0

# Contributing

## License 