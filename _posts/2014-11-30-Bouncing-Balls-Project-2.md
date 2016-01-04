---
layout: post
title: Unity Development - Project 2
---

For this project, we expanded upon the ball and cube model that we have
been developing over the past few weeks. To include what we had done previously,
some of the main features we had to include with this iteration were:

1. Changing the gravity every five seconds. I chose to change world gravity
as opposed each individual game object.
2. Provide more granular log data to include velocity and gravity changes.
3. Instantiate the cube object a total of four times and have balls randomly
generate within the bounds of their respective parents.

#Running the Game
Download and extract the falling zip file:

Inside the ‘OrahoodProject2’ directory, you will find a Windows executable called
‘OrahoodProject2.exe’.

#Game Instructions
There is no user interaction with this particular project however if you want to
view the log files they can be found in the following directory:
/OrahoodProject2/RedBallLogFile.txt
/OrahoodProject2/YellowBallLogFile.txt
/OrahoodProject2/GreenBallLogFile.txt

#Programming Notes
This was a really fun project and I took advantage of using some of the free assets
that are available on the Unity Asset Store. I would highly recommend fellow
students to use assets on the store to better help them create their future projects. I
found it much easier to use world gravity as opposed to changing each individual
GameObjects’ gravity.

#Test Data
Since there is no test framework for this particular game, I tested my program my
ensuring that the game was running as intended. I verified the locations of the balls
in game by using the GUI Labels to display the position of each ball, its velocity
and world gravity settings. I also verified that the game logged data to a text file as
intended.

#References
Answers.unity3d.com,. (2014). How to get the velocity of an object - Unity
Answers. Retrieved 1 December 2014, from http://answers.unity3d.com/
questions/385102/how-to-get-the-velocity-of-an-object.html

Assetstore.unity3d.com,. (2014). Asset Store. Retrieved 1 December 2014, from
https://www.assetstore.unity3d.com/en/

Forum.unity3d.com,. (2014). Randomly generate objects inside of a box | Unity
Community. Retrieved 1 December 2014, from http://forum.unity3d.com/
threads/randomly-generate-objects-inside-of-a-box.95088/

Technologies, U. (2014). Unity - Scripting API: Physics.gravity. Docs.unity3d.com.
Retrieved 1 December 2014, from http://docs.unity3d.com/ScriptReference/
Physics-gravity.html

Unity?, H. (2014). How can I set a Skybox as my background in Unity?.
Stackoverflow.com. Retrieved 1 December 2014, from http://stackoverflow.com/
questions/12047501/how-can-i-set-a-skybox-as-my-background-in-unity
