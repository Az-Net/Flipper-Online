# Flipper-Online
Flipper Ønline (FØ /Eff:Null/)   

![](https://github.com/Az-Net/Flipper-Online/blob/main/assets/F0.gif)

## A Flipper Zero Multiplayer Game Inspired by Digimon &amp; Megaman V-Pets

### *This Project is Still in Development*

F0 is a complex cellular automata. Each Flipper Zero device acts as a self-contained digital entity with unique characteristics determined by hexadecimal code. This code influences the Flipper's appearance, mood, and stats. The game leverages these pre-programmed behaviors to create a world where Flippers interact with their environment and each other based on a set of rules. This rule-based system, combined with the Flipper's ability to access frequency interactions, hopes to achieve a level of autonomy that pushes the boundaries of traditional gaming experiences.


# Design 

The F0 entity is primarily designed using three layered components:
* a Bit-Value array stores modifiable firmware interactions
* plaintext bin files with no extension containing hexadecimal strings act as the core cells 
* a matrix array acts as both the combat grid and as the next evolution in our project, combining and processing individual cell interactions to create a more capable and unique, emergent entity.  

The application reads and writes data to- and from- bin files and interprets the firmware logic for processing components from your Flipper's SD card.

## Cells

Each cell exists as a 5-bit hexadecimal string within a plaintext file, with no extension. This means that you can use the existing text viewer and hexadecimal editor apps on the Flipper Zero for modifying cells.  
Each cell consists of a Shape, a Protrusion of a shape, a Health value, a Size, and a Mood value, creating a layered, fractal-like entity.  
There are three options for each attribute, and each attribute influences the others during cell interaction, for a total of 5^3+1 possible cell states at inception.  

### Example Cell Strings
__0x157AF__  
__0x349BE__  
__0x208A0__  

(Remember: each Bit-Value category can only be used once. Refer to the [Bit-Value Array](#bit-value-array)
 below for updated firmware rules.)

## Bit-Value Array

Each hexadecimal bit value 0-F is only used once, and each category of value can only be used one time per cell.  
The process of cell combat modifies the hexadecimal strings during interaction, eventually writing the 0 bit to Shape to denote that a cell is dead.  
Reviving a cell simply involves editing its file to remove the 0 bit from its hexadecimal string and then setting a new shape bit value within the string.  
You can also choose to reset or edit the mood, size, protrusion and health values to anything you want.  

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
(WiP)

When cells are interacting, their values are copied to a matrix array for pre-processing, and for simultaneously processing multiple interactions across numerous cells per clock cycle.  

Cells on the matrix seek to copy themselves across each of the matrices, interacting with- and consuming enemy cells as they go.  

The matrix starts with one user cell and one enemy cell at either ends. Each cell is processed simultaneously, and they may copy themselves to any of the open slots in the matrix adjacent to the cells current slot.  
If two competing cells seek to occupy the same matrix slot, they are processed against one another until one cell dies.  
The matrix continues processing until either the user cell shape or the enemy cell shape is the only one left occupying the matrix.  
Users can set one cell of each shape for pre-selection during automatic battles.  
See [Core Gameplay Loop](#core-gameplay-loop) for more.  

### Advanced Processing 
Matrices can be processed two different ways:
* by copying values from bin files directly to the matrix, editing the strings, then copying the values back
* by referencing a cell file by name to edit it directly
  
A matrix cell that references itself can loop or recurse.  
Matrix cells that reference another matrix or themselves can be made to terminate when a cell Doesn't reference another matrix during the current or next parse.  

Matrices have a unique format;
* each vertical line is closed with [Square Brackets]
* a pipe | separates each horizontal entry
* spaces and line breaks are ignored

Matrix files have no extension and share a folder with cells.

[Example Matrices](https://github.com/Az-Net/Flipper-Online/blob/main/examples/example_matrix.md)

# Cell Processing 

At the most basic level, cells follow a simple roshambo model of interaction.  
○ -> △ -> □  
This remains true of both the Shape and Protrusion of each cell interaction.  
Smaller cells out-speed larger cells.  
Mood, Size, Protrusion and Health are all modifiable values: they change during cell interaction.  
If a Bit-Value for a Shape does not exist in the cell, it is considered dead (the same as a 0 Bit-Value being written).  
Both the Shape and the Protrusion of a cell can be set to 0. Any other Bit-Value in a cell that gets set to 0 will be reverted to its minimum value (ie. Small for Size).  

## Cell Matrix Logic
(WiP)  
Matrix Logic is liable to constant optimization and iteration.  

First:  
* Compare Speed > Smaller Moves Sooner  
* Process Protrusion > Loser Changes Form  

Then:  
* Roshambo on Main Shape > Losing Shape -1 HP

Mood:  
* If Happy then hits enemy > set Protrusion as Enemy Shape
* If Happy then Hit > Neutral
* If Neutral then Hit > Sad
* If Sad then Hit > Set Protrusion 0  
  
Health:  
* If HP Min & Hit = Set Shape 0 (dead)
* If HP Max & Hits enemy > get bigger

# Core Gameplay Loop  
(WiP)

The only current user interactions involve editing the cells between grid combat, scanning them as they're cloning on the matrix, and healing the currently scanned cell during combat.  

Cells compete on the matrix by randomly being scanned into existence (yada yada this part for now. subghz or gyro step scanning.)  
When an enemy loses on the grid, their cell is copied to your data repository to be used in future battles, and a copy of the matrix at the time of completion is also saved.
These matrices will be useful later (see [Online Multiplayer](#online-multiplayer))

### Cell Grid Actions
* Flee  
Cell tries to move away after interaction
* Move  
Cell tries to move anywhere before interactions
* Split (Copy Self)  
Cell tries to copy itself to an adjacent slot before or after interaction

### User Actions
* Heal  
You may heal each cell once per grid combat. 
* Scan  
When you scan a cell on the matrix, information displays detailing the current health, mood, size, shape and protrusion on that cell. Only one cell may be displayed at a time, and you may only heal a currently-scanned cell.

See [Combat Matrix](#the-combat-matrix) for more.

## Display 
(WiP)

The game does not need to be run with a GUI.  
Cell interactions can be processed at the system level without drawing their interactions to the display.

# Hardware Add-ons
* Shop

### Video Game Module
* Gyro Step-Counting
* Raspi 2040 Firmware Integration

### Malveke
* Gameboy Cartridge Reading & Writing
* Serial Data Transfer via Link Cable

### Pi 0
* LLM Integration

# Local Multiplayer

### Contacts

# Online Multiplayer
### Gameplay
### Economy
### Future Development
* Expand single-bit values 0-F to 2-bit values 0-FF
* Expand 3x3 Matrix to layered 9x9 variant
* Layered Matrix Processing Logic
* Server Integration

# Contributing

Currently contributors must visit our GitHub [organization page](https://github.com/Az-Net) and join our discord server, after reading our rules.

## License 

F0 Licensing  
2024

Licensed under the Apache License, Version 2.0 (the "License") modified with Commons Clause
Restriction; you may not use this file except in compliance with the License. You may obtain a
copy of the License at  

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the
License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
KIND, either express or implied. See the License for the specific language governing permissions
and limitations under the License.  

Commons Clause Restriction  

The Software is provided to you by the Licensor under the License, as defined below, subject to
the following condition.  

Without limiting other conditions in the License, the grant of rights under the License will not
include, and the License does not grant to you, the right to Sell the Software.  

For purposes of the foregoing, “Sell” means practicing any or all of the rights granted to you
under the License to provide to third parties, for a fee or other consideration (including without
limitation fees for hosting or consulting/ support services related to the Software), a product or
service whose value derives, entirely or substantially, from the functionality of the Software.  
Any license notice or attribution required by the License must also include this Commons Clause
License Condition notice.  

Tl:Dr; Do whatever you want as long as you do it for free.