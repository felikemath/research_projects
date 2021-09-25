---
layout: default
mathjax: true
show_viewon: true
repolink: https://github.com/felikemath/P3_Bouncing_Ball_Simulation_Game
---

# <center><span style="color:darkblue">Multi-Ball Bouncing Simulation and Game</span></center>

<br/>
## Project duration
July-August, 2021

Click [**<span style="color:blue">here</span>**](#_results) to jump to see the animation result.


## Summary

In this project, I developed a bouncing ball game to illustrate the physics concept of Conservation of Momentum. In this game, multiple friction-free balls of different masses and sizes are moving at different directions and speeds inside a space surrounded by four friction-free walls. When collided with one another, the balls will bounce away, just like those in pool games. The ball will also bounce back when hitting any of the walls. Additionally, the player can move a bat towards left or right along the bottom wall. If a ball hits the bottom wall, the player loses points. If a ball hits the bat, the player gains points. Ultimately, the player’s objective is to move the bat so that the falling balls hit the bat instead of the bottom wall.

While there is still a lot of space for improvement from perspective of a computer game, the focus of this project is the simulation of motion, collision and the bouncing between the balls, between the balls and walls, and between the balls and bat, so that they would look realistic. This requires accurate calculation of the speeds and directions of each ball after collisions, which depends on their speeds and directions before the collision, depends on their masses and sizes, and depends on the collision type (ball-and-ball, ball-and-wall, ball-and-corner of bat, ball-and-sides of bat). Through the law of conservation of momentum and kinetic energy, which I learned in AP Physics, I was able to calculate such values.

This game was implemented in Python.

The `class ballclass()` is defined to hold ball states, such as the mass, size, location, speed with direction, etc. This class also has a few member methods to help handle the ball-bat collisions:

-   `def Is_Ball_in_Box_Range_Simple(self, boxrect)` checks whether the ball hits the bat (box).
-   `def Check_Ball_Hit_BoxTopLeftCorner(self, boxrect)` checks whether the ball hits the top-left corner of the bat.
-   `def Check_Ball_Hit_BoxTopRightCorner(self, boxrect)` checks whether the ball hits the top-left corner of the bat.
-   `def Calc_BallSpeed_on_BoxTopLeftCorner(self, boxrect, boxspeed)` calculates the speed and direction of the ball after hitting and bouncing back from the top-left corner of the bat.
-   `def Calc_BallSpeed_on_BoxTopRightCorner(self, boxrect, boxspeed)` calculates the speed and direction of the ball after hitting and bouncing back from the top-right corner of the bat.
 

The `main()` function starts with the instantiation of 4 (by default) balls with mass, initial speeds and locations. The game will progress through the “while True” loop until the player presses the “_Esc_” key or closes the game window. The main tasks handled inside the while loop include

-   moving the bat left or right if the player presses the _Left_ or _Right_ Arrow key, respectively. Pressing the _SHIFT_ key at the same time increases the speed.  
-   looping over each ball to update its state based on its previous location and speed. If the ball would hit either a wall, a corner of the bat, or a side of the bat, compute its new speed to bounce back. 
-   looping over each pair of balls to check if a collision occurs between them. If yes, compute the new speed and direction of both balls. 
-   calling the `blit()` function from the _PyGame_ package for each drawing object to refresh display at its new location.  


<button class="button button1"><a href="https://github.com/felikemath/P3_Bouncing_Ball_Simulation_Game">View the Project on GitHub</a></button>


## <a name="_results"></a>Results - Recorded Video Clip of Demo of the game
Here is an example of video clip of a game using 4 balls of different relative mass of 1.0, 1.0, 2.0 and 4.0. Please click the Replay button to view the video.

<p align="center">
<video width="760" height="760" controls>
<source src="{{ "/assets/images/project3/recording_of_Bouncing_Balls_Game.mp4" | relative_url }}" type="video/mp4">
</video> 
</p>

<br/>
<br/>
