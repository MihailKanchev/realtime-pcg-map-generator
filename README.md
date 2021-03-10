After reverse engineering the level generation in The Binding of Isaac my curiosity for PCG spiked.


Being a long-term fan of the Diablo series I was always captivated by their level design and enemies, and how unique, yet consistent, they were with every new playthrough. This led me to try and implement a simillar system.


Unlike my previous attempt with PCG that was using arrays, I decided to delve deeper in the Data Structures I have at hand. The new problem I was tackling involved real-time map generation that does not have boundries, a core difference to my last PCG project, where I had to set the boundries of the level initially. Ultimately I stopped on a Dictionary, since  it is dynamic (C# takes care of that for you) and you can quickly lookup wether a specific tile is already in the list.


The real time map generation works like this:

Generate a 5 x 5 starting tile set, that is made from a variation of 8 different sprites, then place the player in the center.
Every time the Player moves there is an input on the Horizontal or Vertical axes. After the input is received add tiles 3 units away from the input direction.
The newly added tiles can be ground tiles, 33% wall tiles or 10% dungeon entrance tile.

On a trigger collision with the dungeon entrance, the player position is saved, the map is disabled and a dungeon is procedurally generated.

The PCG dungeon building works like this:

The code chooses a random Y on the very left of the dungeon.
After picking the position, the starting tile is added to the dungeon Dictionary type to be revisited later.
After that it looks for adjacent tiles on top, bottom or right (the algorithm is a very simple integration, since it can only build dungeons from left to right and does not build pathways that lead to the left).
It keeps looking for adjacent tiles until it reaches the far right of the dungeon  (the dungeon size is a random square with a width between 50 and 100).
After the main path is built, it is populated with ground tiles and the algorithm starts from the beginning of the Dictionary.
After every iteration of a key-value pair in that Dictionary, the algorithm decides wether to build a "Cave Chamber" or simply put a wall. If a chamber is chosen, the starting location of that chamber is added to a queue to be revisited later.
After the algorithm is done putting walls it goes to the queue in order to generate the chambers.
When all the chambers are generated, the algorithm populates the rest of the cave with walls.

This was my virst project that followed a complete modular structure. 

There is a Board Manager class that takes care of the map and its generation.
There is a Dungeon Manager class that generates dungeons on a dungeon entry.
There is a Game Manager class that is a mediator between the previous two classes, the player and the potential enemies.

This project made me confident to persue further PCG methods.

Link to the github of that project can be found here.
