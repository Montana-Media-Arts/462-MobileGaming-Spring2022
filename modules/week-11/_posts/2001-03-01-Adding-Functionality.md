---
title: Adding Functionality
module: 11
jotted: false
---

# Making our Ship Functional

So, let's make the ship move around!  There are two things we need to make this happen.

To move, the ship requires two things.  

1. It needs what is called the RigidBody2D
2. Script called Move With Arrows.

## RigidBody2D

RigidBody2D is vital to any object because it applies physics properties like gravity and mass.

1. In the **hierarchy**, select the ship.
2. In the **Inspector**, click **Add Component**.
3. In the dropdown, look for **Physics 2D** and click **RigidBody2D**
4. Once the **RigidyBody2D** component is added, run the program.  What happens?
5. We don't want it to fall through the ground, so let's change the **Gravity Scale** to zero.
6. We also don't want to make the ship fly too fast; we will add some **Linear Drag**, which is also like friction.  Change the **Linear Drag** to **10**. 

What about making it move around?  That's where we add code. Lucky for us, we get to use a pre-built script.

## Move With Arrows

1. Click on the **Add Component** again
2. This time, type in the **search** bar **Move With Arrows**
3. After you add the script, press play.  If you use the arrows, the ship should move around.
4. Now, change the speed variable in the **Inspector** and see what happens.

What about obstacles and collisions?

<a href="https://umontana.zoom.us/rec/play/vpcpder8pz83GdOd5gSDVqUrW424L_-s2iFIq_YPn0azUHADNlWlZ7USYeMtsU7QlGaLW7d12O7WUJW8?continueMode=true" target="_new">Video</a>