---
layout: default
mathjax: true
---

# <center><span style="color:darkblue">Animation of Projectile Motion with and without Air Resistance</span></center>

<br/>
## Project duration
June, 2021

## Introduction
Projectiles are very common in our daily life, such as throwing a water-balloon, shooting a basketball, shot put, etc. From my AP physics class, I learned that the motion of projectiles has a parabolic trajectory when air resistance is negligible, but we never explored the scenario containing air resistance. This project demonstrates the effect of air resistance on the motion of projectiles through the visualizations of 2-d projectiles in Python. Click here to jump to see the animation result.

Click [here](#_results) to jump to see the animation result.

## Objectives 
The objectives of this projects include
•	To animate the motion of projectiles with and without considering air resistance. 
•	To compute and compare instantaneous locations, velocities, travel distances and energies. 
## Methods
### 1.	Physics and Math
It is well known that air resistance depends on the speed, shape and size of projectiles, density of air, and some other factors. Therefore, it can be a complex phenomenon to study and measure. In this project, we simplify the model by assuming that the drag force of air resistance is proportional to the speed of the projectile and always opposite to the direction of its velocity 

<div class="alert alert-secondary equation">
	<span>\({\vec F_a} =  - k\vec v\) </span><span class="ref-num"> (1)</span>
</div>

<p>where \(k\) is a positive constant describing the air resistance coefficient. By ignoring non-linear components, this approximation might not be very accurate in reality, but it allows separating the drag force into horizontal and vertical directions, respectively, and makes differential equations easy to solve. </p>

<p>Consider a projectile of mass \(m\), initial position, \(\left( { {x_0},{y_0} } \right)\), initial velocity, \({\vec v_0} = \left( { {v_{x,0} },{v_{y,0} } } \right)\) and initial launch angle, \(\theta \) (Figure 1). </p>

<p align="center">
 <img src="{{ "/assets/images/project1/Projectile.png" | relative_url }}" style="border:solid; color:gray" width="350"> 
<br>Figure 1 Illustration of the projectile. 
</p> 

<p>The \(x\)- and \(y\)-components of initial velocity is </p>
<div class="alert alert-secondary equation">
	<span>
		<p><span> \({v_{x,0}} = {v_0}\cos \theta \) </span></p>
		<p><span> \({v_{y,0}} = {v_0}\sin \theta \) </span></p>
	</span>
	<span class="ref-num">(2)</span>
</div>
  
<p>Using the linear model of air resistance (Eq. 1) and Newton’s 2nd law:</p>
<div class="alert alert-secondary equation">
	<span>
		<p><span> \(m\frac{ {d{v_x} } }{ {dt} } =  - k{v_x}\) </span></p>
		<p><span> \(m\frac{ {d{v_y} } }{ {dt} } =  - mg - k{v_y}\) </span></p>
	</span>
	<span class="ref-num">(3)</span>
</div>
 
<p>Solving these differential equations with the initial conditions, gives the instantaneous velocity as a function of time \(t\) </p>

<div class="alert alert-secondary equation">
	<span>
		<p><span> \({v_x}\left( t \right) = {v_{x,0} } \cdot {e^{ - \frac{ {kt}}{m} } }\) </span></p>
		<p><span> \({v_y}\left( t \right) = {v_{y,0} } \cdot {e^{ - \frac{ {kt} }{m} } } + \frac{ {mg} }{k}\left( { {e^{ - \frac{ {kt} }{m} } } - 1} \right)\)  </span></p>
	</span>
	<span class="ref-num">(4)</span>
</div>

	  
<p>Integrating \({v_x}\left( t \right)\) and \({v_y}\left( t \right)\) with respect to \(t\) gives instantaneous positions</p>

<div class="alert alert-secondary equation">
	<span>
		<p><span> \(x\left( t \right) = {x_0} + {v_{x,0}} \times \frac{m}{k}\left( {1 - {e^{ - \frac{ {kt} }{m} } } } \right)\) </span></p>
		<p><span> \(y\left( t \right) = {y_0} + {v_{y,0}} \times \frac{m}{k}\left( {1 - {e^{ - \frac{ {kt} }{m} } } } \right) + \frac{ { {m^2}g} }{ { {k^2} } }\left( {1 - \frac{k}{m}t - {e^{ - \frac{ {kt} }{m} } } } \right)\)   </span></p>
	</span>
	<span class="ref-num">(5)</span>
</div>
	  
<p>The above equations are the general formulas for the linear model of air resistance. In the absence of air resistance, the formulas can be derived from Equation (3) by setting \(k = 0\) as below:</p>

<div class="alert alert-secondary equation">
	<span>
		<p><span> \(m\frac{ {d{v_x} } }{ {dt} } = 0\) </span></p>
		<p><span> \(m\frac{ {d{v_y} } }{ {dt} } = -mg\) </span></p>
	</span>
	<span class="ref-num">(6)</span>
</div>

<div class="alert alert-secondary equation">
	<span>
		<p><span> \({v_x}\left( t \right) = {v_{x,0} }\) </span></p>
		<p><span> \({v_y}\left( t \right) = {v_{y,0} } - gt\) </span></p>
	</span>
	<span class="ref-num">(7)</span>
</div>

 	
<div class="alert alert-secondary equation">
	<span>
		<p><span> \(x\left( t \right) = {x_0} + {v_{x,0} } \times t\)   </span></p>
		<p><span> \(y\left( t \right) = {y_0} + {v_{y,0} } \times t + \frac{1}{2}g{t^2}\) </span></p>
	</span>
	<span class="ref-num">(8)</span>
</div>
	  	
<p>In fact, as an alternative method, if you substitute the Taylor expansion \({e^{ - \frac{ {kt} }{m} } } = 1 - \frac{ {kt} }{m} + \frac{ { { {\left( {\frac{ {kt} }{m}} \right)}^2} } }{ {2!}} + \cdots \) into Equations (4) and (5) and take limit of \(k \to 0\), you will get the same results as Equations (7) and (8). </p>

<p>As for the accumulated travel distance \(d\left( { {t_n} } \right)\), it can computed by adding the new traveling length to the previous accumulated travel length</p>

<div class="alert alert-secondary equation">
	<span> \(d\left( { {t_n} } \right) = d\left( { {t_{n - 1} } } \right) + \Delta d\left( { {t_n} } \right)\) </span><span class="ref-num"> (9)</span>
</div>

<p>The kinetic, potential, and total mechanic energies can be computed using the instantaneous speed and positions, accordingly. </p>

### 2.	Computer programming
The animation part of this project was implemented using Python with the Matplotlib package. The source code is available here. There are 4 major components:

*   In the global scope, the simulation parameters are specified, such as the initial position, velocity, launching angle, mass, air resistance coefficient, and the Gravitational Constant. The drawing and text objects are also created and will updated during animation. 

*   The init() function to reset the drawing and text objects, as well as the intermediate variables. 

*   The animate(i) function to compute the instantaneous quantities on-the-fly and update the drawing and text objects. 

*   The main() function calls animation.FuncAnimation() from the Matplotlib package to create the animation, which repeatedly calls the animate(i) function above to refresh the display. It also saves the animation to video files. 

## <a name="_results"></a>Results and Discussions
The animation video is shown below. The trajectories with and without air resistance are drawn in red and blue, respectively. 

<p align="center">
<video width="640" height="640" controls>
<source src="{{ "/assets/images/project1/Projectile_animation.mp4" | relative_url }}" type="video/mp4">
</video> 
<br>Figure 11 Animation of the 4 optimizers’ update paths from the starting point to the minimum loss. 
</p>

We observed a few differences between the two scenarios.
*   Due to the impact of air resistance, the projectile has a trajectory different from that in absence of air resistance, and it is no longer a parabolic curve.
*   With air resistance, the projectile flies slower than that in absence of air resistance. At the same intervals of time, its speed (magnitude of velocity) and travel distance are lower and smaller. 
*   With air resistance, the projectile loses mechanical energy, which was used to overcome the resistance and converted to heat.  

## Summary
In this independent project, I explored the impact of air resistance on projectiles beyond what was covered in our AP physics classroom. This exploration involved in building a model based on Physics, solving differential equations using math, and making vivid animations using computer programming. The visualized results provide us a view and sense different from textbook. It is a fun and interesting project that anyone can do!