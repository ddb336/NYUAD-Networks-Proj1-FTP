# FTP-Daniel-Aisha
*Building an application protocol that runs on top of the sockets.*

## Description

This project implements a client-server FTP system in C.

### How to run

First, run <code>make</code>. This will build the executables. You can put the 
<code>FTPserver</code> and <code>FTPclient</code> exectuables in different 
directories if necessary, and then run them by copying the makefile info output 
example. 

For the server, run <code>./FTPserver</code><br>

For the client, do <code>./FTPclient 127.0.0.1 9000</code>. 
This will open the client instance and try to connect to local host, which has
IP address 127.0.0.1, on port 9000, which is the server's default port.

## Checkpoint 1

At this stage of the project, we have implemented the USER, PASS and QUIT 
commands in the *FTPclient.c*. The client can connect to the server and do 
basic authentication, but none of the file transfer is yet implemented.

To test checkpoint one, run the server with: <br>
<code>gcc -o FTPserver FTPserver.c && ./FTPserver</code><br>
And then run the client with <br>
<code>gcc -o FTPclient FTPclient.c && ./FTPclient 127.0.0.1 9000</code><br>
After this, authenticate with one of the following user-password pairs:<br>
<ul>
    <li><code>USER Aisha PASS AHPass</code></li>
    <li><code>USER Daniel PASS DBPass</code></li>
</ul>

## Final Version 

For the final version of the project, we have implement the **PUT, GET, CD, !CD, LS, !LS, PWD**, and **!PWD** commands in *FTPserver.c* and *FTPclient.c*. We have incoorported these functions with previously developed USER and PASS commands that serve as a way to authenticate the user in the beginning. The PUT commands is used to upload a file from the current client directory to the current server directory. GET command is used to download a file from the current server directory to the current client directory. Both of the command are executed such that a new TCP connection is established on a different port for the data transfer. The port is picked any of the available port, which prevents the issue of choosing unavailable ports and refused connections. 

For navigating the directories, we have implemented the CD, LS, PWD commands which can change the current directory, list all the files under the current directory and displays the current directory. The work for both client and the server, so that each of them can move between the directories and inspect them. 
We have expanded our user-password pairs to contain instructor's name, hence the valid pairs are: 

<ul>
    <li><code>USER Khalid PASS KMPass</code></li>
    <li><code>USER Aisha PASS AHPass</code></li>
    <li><code>USER Daniel PASS DBPass</code></li>
</ul>


An example of execution of all commands on the client side looks like: 

<ul>
    <li><code>USER Aisha </code></li>
    <code> 331 Username OK, password required! </code>
     <li><code>PASS AHPass</code></li>
    <code>Authentication complete!</code>    
    <li><code>PUT new.txt</code></li>
    <code>Sending file : new.txt Connecting to port 12793 for file transfer. PUT function completed.</code>   
    <li><code>GET tests.txt</code></li>
    <code>The transfer of the file from server starts...
    Connecting to port 16121 for file transfer.
    Transfer of the file tests.txt done. New file is saved as Client-tests.txt. 
    Port closed.</code>
    <li><code>CD Server</code></li>
    <code>Successfully changed directory.</code>   
    <li><code>LS </code></li>
    <code>FTPserver FTPserver.c Server-new.txt </code>    
    <li><code>PWD </code></li>
    <code>/Users/aishahodzic/Documents/GitHub/FTP-Daniel-Aisha/Server </code>
    <li><code>QUIT </code></li>
    
  
</ul>

We have developed the *FTPserver.c* and *FTPclient.c* such that they are able to respond with an appropriate error messages in case of any inconsistency. Most importantly, error messages are displayed in case of lacking user authentication, invalid ftp commands, non-existent files being requested for upload or download and user typing an incorrect password. 

We have testing our program for a number of scenarios, including the transfer of different files which you can see under **tests.txt** file. 




RSA implementation (for future):
http://www.trytoprogram.com/c-examples/c-program-to-encrypt-and-decrypt-string/
