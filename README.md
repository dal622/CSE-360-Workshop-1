# CSE-360-Workshop-1
==========
Question 1
==========

I took the code from github labeled as “point-robot-simulator.ipynb” and modified the control policy so that it would draw a tilted ellipse. First, I searched for the parametric equations for an ellipse. I found this website (https://www.mathopenref.com/coordparamellipse.html), which explained that the parametric equations for an ellipse are the following:

x = a cos t
y = b sin t     

*Where x, y are the coordinates of any point of the ellipse and a, b are the radii along the x-axis and y-axis, respectively. 

    I implemented this in my code with the following from block 4:
        ux = -4*sin(t)
        uy = 2*cos(t)
    
To tilt the ellipse, I realized that I would have to rotate vectors since the control policy controls velocity. To do so, I knew I would have to use the Angle-Sum Rule (https://matthew-brett.github.io/teaching/rotation_2d.html). I implemented this in my code by taking the calculated velocities from the previous part and plugging them into the Angle-Sum Rule:
ux = -(ux*cos(pi/6)-uy*sin(pi/6))
uy = ux*sin(pi/6)-uy*cos(pi/6)

==========
Question 2
==========

a) To create the starfish shape, I used the parametric equations found from the website given in the problem statement and used that as my control policy as seen from block 4:
    ux = -sin(t)*sin(5*t)+5*cos(t)*cos(5*t)-2*sin(t)
    uy = cos(t)*sin(5*t)+5*sin(t)*cos(5*t)+2*cos(t)
    
b) To simulate vertical wind, I added a random number generator that would add an array to x from block 5. Since we only want a vertical disturbance, the first number of the pair will always be 0. The following is my implemented code:
x = simulate(Δt, x, u) + array([0, randint(0, 2)])

c) Next, to implement the PI-controller, we would have to calculate error. Here, I calculated the ideal position and the actual position of the point robot. Subtracting these two values would give us the error associated with the disturbance. After calculating the error, we can now calculate our new control policy, which has the equation:

   u =kp*error + ki*simulate(Δt, error, x) 
 
   Finally, we simulate this new control policy to give our corrected path. 
    ***I couldn’t get this part to fully work, I believe the issue lies with kp and ki. I don’t know what to set it as.
    
==========
Question 3
==========

To create a 3-D helix shape, I knew that I would need three different velocities for each direction. I updated the control policy in block 4 so that it would return an array of length 3. Next, I searched for the parametric equations for a helix, which lead me to this website (https://mathworld.wolfram.com/Helix.html). I came up with the following control policy: 
  ux = t
  uy = sin(t)
  uz = cos(t)
    Next, in order to plot in 3-D, I made the a 3-D axis and plotted normally in block 6:
  fig = plt.figure()
  ax = plt.axes(projection='3d')
  ax.plot(x, y, z, 'green');
    *Note I wasn’t sure how to make the animation 3-D, but I did plot it in 3-D

==========
Question 4
==========

For this solution, I used the code from the github provided labeled as “trajectories.ipynb”.  Here, I mapped out the path that I would have to take by hand in order to avoid the obstacles. Since we aren’t concerned with smoothness of lines, I made straight lines to each point. 

==========
Question 5
==========

For this solution,  I used the same code from solution 4 and added the code from github under the block named “Polynomial Trajectories”. Here, we are concerned with smoothness of lines and avoiding obstacles. To do this, I implemented a trial-and-error approach to the problem, where I would change the starting and ending velocities between points. If a line collided with an obstacle I would know to change either the starting velocity or ending velocity. 
