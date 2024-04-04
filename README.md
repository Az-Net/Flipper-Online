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

## The Bit-Value Array

Each hexadecimal bit value 0-F is only used once.  
The process of cell combat modifies the hexadecimal strings during interaction, eventually writing the 0 bit to Shape to denote that a cell is dead.  
Reviving a cell simply involves editing its file to remove the 0 bit from its hexadecimal string and then setting a new shape bit value within the string.  

|Bit-Value|Use|Category|
|---|---|---|
| 0 | Null |
| 1 |   |Shape|
| 2 |   |   |
| 3 |   |   |
| 4 |   |Protrusion|
| 5 |   |   |
| 6 |   |   |
| 7 |Small|Size|
| 8 |Medium|   |
| 9 |Large|   |
| A |   |Mood|
| B |   |   |
| C |   |   |
| D |Min|Health|
| E |Mid|   |
| F |Max|   |













## The Combat Matrix

When cells are interacting, their values are copied to a matrix array for pre-processing, and for simultaneously processing multiple interactions per clock cycle.  

