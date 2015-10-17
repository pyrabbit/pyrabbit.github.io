---
layout: post
title: Creating a Basic Kismet Client with Java
---

Kismet is a great tool for wireless survey and collection but many of the 802.11 tools out in the wild leave a lot to be desired. I often find myself wanting to create something very specific to fit my own needs. Luckily for us, programming with Kismet is not all that hard and frankly, Kismet is awesome so we don't have to reinvent the wheel here.

##Basic structure of Kismet
This tutorial will make a whole lot more sense if you understand how Kismet operates. Kismet is actually divided up into several different services: `kismet_server, kismet_client, and kismet_drone.` We will be working with the server and client in this tutorial but know there is some pretty cool stuff you can do with a drones. Maybe that will be a topic for the future.

Now if you have worked with kismet in the past you may be familiar with the GUI that is ran inside your terminal. It is important to understand that when you are using that GUI you are actually interacting with an instance of a kismet client. In the background there is a kismet server instance running and this server passes data to any client connected to it via the localhost on TCP port 2501. Essentially, the kismet server is just blasting out all the network data it discovers onto your localhost. Because it is TCP, it is relatively extract the kismet data programmatically. But there are a few steps we must do first before we can start pulling out all the data.

##Start an instance of kismet server
Ensure that you have your wireless network card plugged in. I use the Alfa AWUS036NHA with the Atheros chipset and find that it works quite well. Open up a new terminal and enter the following command.

`kismet_server -c wlan0`

This is all you need to get your kismet server up and running.

##Creating the KismetClient object
We are going to create a `KismetClient` object that we can use to connect and interact with the kismet server. Additionally, we are going to have two constructors.

1. The first constructor will have the default server and port settings needed to connect with the kismet server.
2. The second constructor will allow the developer to specify the server and port of the kismet server.

So lets get started...

	public class KismetClient implements Runnable {
    	// Declare variables
    	final private String host;
    	final private int port;

        public KismetClient() {
        	this.port = 2501;
        	this.host = "localhost";
    	}

    	public KismetClient(String h, int p) {
        	this.port = p;
        	this.host = h;     
    	}
    }

##Creating a method to connect to server
What we need now is a way to interact with our object and connect to our kismet server. It wouldn't hurt to know the basics of socket programming before tackling this tutorial but it is not required. This actually serves as a perfect example of how socket programming works.

Lets go ahead and create a method that allows us to connect to the server. I designed this method to return a boolean value so we can do some basic error handling inside or main loop. Additionally, within our method we are going to do some basic trapping incase we receive any exceptions.

    public boolean connectToServer() throws ConnectException {
        try {
            // Open a socket connection. Think of this as the door that lets the kismet data enter our program
            socket = new Socket(this.host, this.port);

            // Create BufferReader/Writer for talking with Kismet Server
            fromServer = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            toServer = new BufferedWriter(new OutputStreamWriter(socket.getOutputStream()));

            // Announce connection to console
            System.out.println("Connected to " + this.host + ":" + this.port);

            // Send Kismet commands
            toServer.write("!0 REMOVE TIME\r\n");
            toServer.write("!0 ENABLE BSSID bssid,channel,type\r\n");

            // Flush the output stream
            toServer.flush();

            // Begin a new thread
            Thread thread = new Thread(this);
            thread.start();

            // Respond with valid connection
            return true;
        } catch (ConnectException ex) {
            // Respond with invalid connection
            System.err.println("Cannot connect to kismet server, it is probably down.");
            return false;
        }
    }

Hopefully the comments should explain whats going on but there are a few specific things that warrant an explanation. By default, when we connect our client to the kismet server we will only receive a time message. In order to get data about our networks we need to create a subscription to a specific kismet protocol. You can read up a little bit more on the kismet protocols on this copy of the kismet documentation found here: http://www.blueskylark.org/kismetaclient/protocol.htm

Note these two snippets of code below. The first is a command that is being sent to the kismet server via our BufferWriter object we created. Each command sent to the kismet server must begin with our client id: `!0`. After our id we send the command and the kismet protocol that we want to apply it to. Here you can see we are unsubscribing from the `TIME` protocol.
`toServer.write("!0 REMOVE TIME\r\n");`

Subscribing is just as easy and you can see below that we are subscribing to the `BSSID` protocol and three of its fields. This makes getting the data that is important to us extremely easy.
`toServer.write("!0 ENABLE BSSID bssid,channel,type\r\n");`

You can learn more about the kismet protocols, fields and commands in the link above. But we are just creating a very basic example, it's up to you to make something useful.

##Disconnecting our client from the kismet server

Just like the method we created that connected our client to the server. Let's create a method that allows us to disconnect from the server as well. This is pretty straight forward as we only need to close the socket.

    public void disconnectFromServer() {
        try {
            // Close the socket connection
            socket.close();
            System.out.println("You disconnected from the local server.");
        } catch (Exception ex) {
            System.err.println(ex);
        }
    }

##Implementing our mandatory abstract methods
When we created our `connectToServer()` method we created and started an instance of a thread. When you use threads, it is mandatory that you implement all of the abstract methods that come along with it. In this particular example we only have to implement the `run()` method. In this particular example we are not doing anything fancy, we are going to just print the next BSSID packet that comes through.

	@Override
	public void run() {
        try {
            while(true) {
                	// grab next kismet message
                	String kismetData = fromServer.readLine();
                	System.out.println(kismetData);
            	}
        } catch (Exception ex) {
            System.err.println(ex);
        }
    }

##Make sure you got all your imports

Ensure that you have all the imports that you need to make your kismet client work

	import java.io.BufferedReader;
	import java.io.BufferedWriter;
	import java.io.IOException;
	import java.io.InputStreamReader;
	import java.io.OutputStreamWriter;
	import java.net.ConnectException;
	import java.net.Socket;
	import java.net.UnknownHostException;

##Finally lets create our main method
Keep your code clean and put `KismetClient()` insides its on Java file `KismetClient.java`. We will create a new file inside the same directory called `KismetExample.java`.

	public class KismetExample {
    	public static void main(String[] args) {
        	KismetClient conn = new KismetClient();
           	if (conn.connectToServer()) {
                System.out.println("Success!");
            }
        }
    }

Hopefully, it should work! Please let me know if this example helped you and I have also provided some challenges to you if you wish to expand on this guide.

##Challenges
1. Create a method that allows the developer to subscribe to specific protocols instead of hard coding in his subscriptions. This method should be part of the `KismetClient()` object.

2. Write the `run()` method so it only outputs data for open networks.

3. Handle GPS data so you can share the location of open networks with your friends.

4. Create a method that allows you to scan certain channels.

5. Identify unassociated clients and what networks they are probing for.
