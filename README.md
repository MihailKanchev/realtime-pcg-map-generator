<p>After reverse engineering the level generation in The Binding of Isaac my curiosity for PCG spiked.</p>
<p>
<br>
</p>
<p>Being a long-term fan of the Diablo series I was always captivated by their level design and enemies, and how unique, yet consistent, they were with every new playthrough. This led me to try and implement a simillar system.</p>
<p>
<br>
</p>
<p>Unlike my previous attempt with PCG that was using arrays, I decided to delve deeper in the Data Structures I have at hand. The new problem I was tackling involved real-time map generation that does not have boundries, a core difference to my last PCG
project, where I had to set the boundries of the level initially. Ultimately I stopped on a <strong>Dictionary</strong>, since &nbsp;it is dynamic (C# takes care of that for you) and you can quickly lookup wether a specific tile is already in the list.</p>
<p>
<br>
</p>
<p>The real time map generation works like this:</p>
<ol>
<li>Generate a 5 x 5 starting tile set, that is made from a variation of 8 different sprites, then place the player in the center.</li>
<li>Every time the Player moves there is an input on the Horizontal or Vertical axes. After the input is received add tiles 3 units away from the input direction.</li>
<li>The newly added tiles can be ground tiles, 33% wall tiles or 10% dungeon entrance tile.</li>
</ol>
<p>
<br>
</p>
<p>On a trigger collision with the dungeon entrance, the player position is saved, the map is disabled and a dungeon is procedurally generated.</p>
<p>The PCG dungeon building works like this:</p>
<ol>
<li>The code chooses a random Y on the very left of the dungeon.</li>
<li>After picking the position, the starting tile is added to the dungeon Dictionary type to be revisited later.</li>
<li>After that it looks for adjacent tiles on top, bottom or right (the algorithm is a very simple integration, since it can only build dungeons from left to right and does not build pathways that lead to the left).</li>
<li>It keeps looking for adjacent tiles until it reaches the far right of the dungeon &nbsp;(the dungeon size is a random square with a width between 50 and 100).</li>
<li>After the main path is built, it is populated with ground tiles and the algorithm starts from the beginning of the Dictionary.</li>
<li>After every iteration of a key-value pair in that Dictionary, the algorithm decides wether to build a &quot;Cave Chamber&quot; or simply put a wall. If a chamber is chosen, the starting location of that chamber is added to a queue to be revisited later.</li>
<li>After the algorithm is done putting walls it goes to the queue in order to generate the chambers.</li>
<li>When all the chambers are generated, the algorithm populates the rest of the cave with walls.</li>
</ol>
<p>
<br>
</p>
<p>This was my virst project that followed a complete modular structure.&nbsp;</p>
<ul>
<li>There is a Board Manager class that takes care of the map and its generation.</li>
<li>There is a Dungeon Manager class that generates dungeons on a dungeon entry.</li>
<li>There is a Game Manager class that is a mediator between the previous two classes, the player and the potential enemies.</li>
</ul>
<p>
<br>
</p>
<p>This project made me confident to persue further PCG methods.</p>
<p>Link to the github of that project can be found here.</p>
