CREDITS: Johnny Nguyen & Taze B.

![image](https://github.com/jnguyen02/projectcodes/assets/111792553/bf91cceb-b732-44ad-9a59-75bc30fc787d)

**INTRO:**

This is a simple online tic tac toe game with extra features such as a surrender and draw option. The program also supports multiple game sessions at once (up to 100).

**IMPLEMENTATION:**

Sockets are used to create a connection between server and client. The open_listener function initialize a socket and sets it to listen on a specified port. The server accepts connection and assigns the client to a tic tac toe game session. Sessions are assigned every time two clients connect to the server.

In the loop, pthread_create is use to create new thread for each game session. It calls the ttt_session function which initializes and start the game. Each game session is given a session id, which is allocated in memory. Pthread allows multiple games to run concurrently.

The function ttt_session contain the game logic. It uses write() to send prompts to the clients and read() to get user inptus such as move,ff, or draw etc. The sockets for each player is set to nonblocking flag, which prevent the client from blocking information when their opponent commit an action.

**STRING FORMATTING:**

After each action/input is made from the client such as connecting to the server or making a move, a protocol is printed. 

For instance turn|bytes|x|enter row,column|

A buffer "content" is being used to create a message that can be sent to the server/clients. It uses several strings that are formatted and concateenated togther with sprintf() and strcat(). Strlen() is use to get the bytes of the strings. Additionally for user inputs commands like move, strlen(cmd)-1 is used to remove the '\n' from the string.


**RUNNING THE CODE:**

In a linux environment, compile the program by calling 'make' in this folder terminal. Simply start the server with ./server portnumber. If you have your own client feel free to use it, or use the one provided in this folder.

example)
./server 16000
./client domain 16000

**SERVER SIDE:**
![image](https://github.com/jnguyen02/projectcodes/assets/111792553/d1ef512b-c8be-4a29-9e11-fa4e1abe476b)

**CLIENT SIDE:**
![image](https://github.com/jnguyen02/projectcodes/assets/111792553/e2333da0-faed-43bc-9f51-02e9ed14f528)



**TEST PLAN:**

This is a broad overview of what to examine and test. Please note that messages/prompts will appear after the completion of each item listed below, confirming that the function is working as intended.

**Testing network connectivity:**
 - Compile and start up the server with ./server portnumber
 Expected output: "listening for incoming connections is printed"
 - Verify that connection works and gamestart with two players 
 Expected output: Enter name prompt will display
 - Verify that two or more players can connect to the server and play the game. (Test for multithreading)
 Expected result: should work

**Testing gameplay:**
 - Enter moves for both players and verify that the game board updates accordingly
 - Verify that the game ends when a player wins or the game is tied
 - Verify that players cannot make moves outside the game board
 - Verify each options work, i.e. request for draw, surrender, move
 Expected results: servere should be able to handle 
 
**Testing performance:**
 - Test the game with a large number of players and verify that the server can handle the load (test having like 5+ games running concurrently)
  Expected results: server should be able to handle
 - Repeatedly do a command like draw, while doing other things simulatiously like connecting another client to the server. (Stress test)
  Expected results: server should be able to handle
  
**Other tests:**
 - Check to make sure all the errors display correctly when inputting wrong messages, names that are taken, invalid moves etc.
 - Test what happens when the server closes while the clients are still in the game
  Expected results: game will end, clients will get kicked out

  
Of course, this is just bare minimum, in the real-world, we would have more complex measures such as security to protect the user data from being leaked such as their ip/connections, and test the game with slow network connections and verify that the game remains playable etc (perhaps with some sort of network emulator tool).



