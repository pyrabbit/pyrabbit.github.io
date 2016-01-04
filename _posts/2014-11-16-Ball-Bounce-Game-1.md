---
layout: post
title: Unity Development - Project 1
---

![screenshot]({{ site.url }}/assets/Game.tiff)

This project served as an initial introduction to our game development
engine. I chose to use the Unity game engine due to its popularity, community,
available assets and the overall challenge of trying to make a game that looks and
plays great. Unity allows you to use several different languages to include C# which
is what I used for this project.

#Running the Game
Download the following Windows executable called ‘LaunchGame.exe’.

#Game Instructions
The game will automatically begin and balls will be generated at a random three
dimensional coordinate within the scope of the cube. Additionally, the balls will
generate with a randomly set velocity however as they bounce off objects their
velocity will tend to increase.

#Test Plan
I took a visual approach to my testing plan along with using the current coordinates
of each ball to verify proper game dynamics. When the game begins, all balls
should be placed at a random position inside the cube. By looking at the X,Y,Z
coordinates you can see that the balls are in fact generating randomly inside the
cube. The balls also generate with a random velocity and will increase in velocity
due the cubes frictionless environment. I am unsure how to properly develop test
plans for Unity. There may be some sort of testing framework that exists however I
don’t feel confident enough to use one yet.


#References
Answers.unity3d.com,. (2014). how do I change the color of a sphere? - Unity
Answers. Retrieved 17 November 2014, from http://answers.unity3d.com/
questions/617059/how-do-i-change-the-color-of-a-sphere-1.html

Answers.unity3d.com,. (2014). how do I change the color of a sphere? - Unity
Answers. Retrieved 17 November 2014, from http://answers.unity3d.com/
questions/617059/how-do-i-change-the-color-of-a-sphere-1.html

Answers.unity3d.com,. (2014). Display Object Positions in Gui Box - Unity
Answers. Retrieved 17 November 2014, from http://answers.unity3d.com/
questions/277188/display-object-positions-in-gui-box.html

Answers.unity3d.com,. (2014). How do I find all game objects with the same name?
- Unity Answers. Retrieved 17 November 2014, from http://answers.unity3d.com/
questions/24257/how-do-i-find-all-game-objects-with-the-same-name.html

Msdn.microsoft.com,. (2014). Writing Text to a File. Retrieved 17 November 2014,
from http://msdn.microsoft.com/en-us/library/aa735748(VS.71).aspx
Technologies, U. (2014). Unity - Scripting API: MonoBehaviour.Start().

Docs.unity3d.com. Retrieved 17 November 2014, from http://docs.unity3d.com/
ScriptReference/MonoBehaviour.Start.html

Technologies, U. (2014). Unity - Scripting API: MonoBehaviour.InvokeRepeating.
Docs.unity3d.com. Retrieved 17 November 2014, from http://docs.unity3d.com/
ScriptReference/MonoBehaviour.InvokeRepeating.html

Unity3d.com,. (2014). Unity - Bouncing Ball. Retrieved 17 November 2014, from
http://unity3d.com/learn/tutorials/modules/beginner/physics/assignments/
bouncing-ball
