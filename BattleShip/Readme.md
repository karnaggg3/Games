GAME SERVER  
  
Overall objective  
  
The objective is the realization of a game server software (Battleship) installed on a Unix machine called "Unix server".  
Each player will use client software located on a machine called a "Unix Client" connected to the Unix server over a network.  
  
Application Administrator  
A particular user called "game administrator" will be able to create and destroy users of the game server.  
The administrator will initialize a game by placing the ships "to be sunk" on the battlefield, and setting the number of players required for that game.  
During the player registration phase for the next game, the administrator will be aware of the applications and may refuse the registration of a player. This user must be able to connect from any client terminal.  
  
Human Machine Interface  
  
The state of the game will be accessible in real time via an interactive "client" interface allowing to authenticate a player by (username and password).  
  
Course of the game  
As soon as the administrator has completed the initialization of the game, each player can apply for the next game.  
After having authenticated with the game server, and as soon as the number of players who are candidates and accepted by the administrator is reached, each player will be able to play in turn, by providing the coordinates of the "move" played. The game server will respond "hit in the water", "hit" or "sunk" to the player, and will update the game status and score in real time on the screen of all players.  
A box touched will be marked "T", and will become "C" when the boat is sunk. Hits "in the water" will not be marked.  
The administrator will be the only one to see all the boats on his screen.  
The game server will determine the end of the game (when all boats are sunk) and the winner will be the player who has the most hits that hit or sunk a boat.  
 	Page 1/2  
  
Technical constraints  
  
Architecture of the application.  
The server will communicate with the clients via sockets.  
  
The server that is a single executable binary (servgame) will consist of two independent modules with a clearly defined common interface.  
-	The module for managing the game and storing the state of the game in shared memory (gestpart.c with an include of protoserv.h).  
-	The customer communications management module (comserv.c with an include from protoserv.h).  The server will have to make sure that each player's turn is respected.  
  
The client part, which is a single executable binary (client game), implemented in each client workstation, will consist of two independent modules with a clearly defined common interface :  
-	The module takes into account the Man_Machine dialog through screens and menus. (ihm.c with an include of protoclient.h). This module will allow to manage the dialog with a player or with the administrator.  
The distinction will be made at the application login: the administrator will be able to connect from any client workstation.  
-	The module for managing communications with the server via sockets (comclient.c with an include from protoserv.h).  
  
It is imperative to respect this architecture.  
  
How to store the state of the game  
  
The game status will be stored in shared memory.  
