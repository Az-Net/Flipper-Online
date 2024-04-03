# Flipper-Online
Flipper Ønline (FØ /Eff:Null/)   
## A Flipper Zero Multiplayer Game Inspired by Digimon &amp; Megaman V-Pets

F0 is a complex cellular automata. Each Flipper Zero device acts as a self-contained digital entity with unique characteristics determined by hexadecimal code. This code influences the Flipper's appearance, mood, and base stats. The game leverages these pre-programmed behaviors to create a world where Flippers interact with their environment and each other based on a set of rules. This rule-based system, combined with the Flipper's ability to access frequency interactions, hopes to achieve a level of autonomy that pushes the boundaries of traditional gaming experiences.

# Design 

The F0 entity is primarily designed using three layered components:
* a Bit-Value array stores modifiable firmware interactions
* plaintext bin files with no extension containing hexadecimal strings act as the core cells 
* a matrix array acts as both the combat grid and as the next evolution in our project, combining and processing individual cells to create a more capable and unique, emergent entity  

The application reads and writes data to- and from- bin files and interprets the firmware logic for processing components.