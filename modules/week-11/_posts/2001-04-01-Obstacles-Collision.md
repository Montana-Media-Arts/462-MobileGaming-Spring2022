---
title: Obstacles and Collision
module: 11
jotted: false
---

# Obstacles

I know obstacles and collisions may not have been your favorite so far, but Unity makes it easy to do both!

You know how to add objects to the scene now.  Go ahead and add something new to the scene into which the ship can collide.

After you add the new object, add the RigidBody2D.  Leave the gravity on this time, though.

Press run, the object should fall through the floor.  Feel free to change the Gravity Scale, so it doesn't fall so fast.

Run the project one more time, moving the ship toward the obstacle.  When you hit the obstacle, does it go right through?

# Collision

How do we add collision in Unity?  Up to this point, we leveraged rectangular collision which was okay, but somewhat imprecise.  Let's use Unity's version.  

Select the ship and then click the Component button again.

Now, click on **Physics 2D** and look for **Polygon Collider 2D**.  This type of collision makes the collision box around all of the curves and angles of the ship.  Cool!

Notice how it highlights?

What about the obstacle?

Do the same thing.  

Now, run the project and see if you can make the ship collide with the obstacle.

<a href="https://umontana.zoom.us/rec/play/uJV4fruhrzg3EtKS5QSDA6N5W9S-Kams1iAYqfIPn0u8WnIKOwWgZ7FBauPuiN_fc5c1idvbnjyPieNu?continueMode=true" target="_new">Video</a>