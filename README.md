Follow-Flock
============

An algorithm for following/hunting while keeping a flock-like behavior.
Was origanally done in java/processing, very poorly. (see Below)
This Repo is dedicated to optimizing and prettifying this algorithm

### The Algorithm
The basic logic is as follows:
* Move towards the "target" 
  * Locate target
  * Calculate velocity towards target, on a scale of 0-1
  * Mulitply the above by speed and add to current velocity
* Flock and repel from the flock
  * To lazy to fill this out now

### Now The Actual Algorithm
* A vector is a point class that thinks it's an angle

1. Vector New Velocity = Target Vector - This Vector
2. Normalize New Velocity'
3. Mulitply New Velocity By Desired Speed
4. For Each Ball In The Hoard
5. Vector Velocity Modifier = This Vector - That Vector
6. Divide Velocity Modifier By The Distance From That Vector''
7. Multiply Velocity Modifier By (Attraction Modifier * Size Of Ball) / The Distance From That Vector
8. Add Velocity Modifier To New Velocity
9. Velocity = New Velocity
10. When Added To The Position Vector The Ball Will Seek The Target But Avoid Collision With The Hoard

* Notes:
  * 'Normalize means to scale down the x and y such that the magnitude, sqrt(X^2+Y^2), is 1
  * ''This value can sometimes be less than or equal to 0



### The Hacked Up Implementation
```java
  void calcRepulse(ArrayList<? extends Ball> list)
  {

    for ( Ball b: list)
    {
      PVector temp = new PVector();
      temp = PVector.sub(position, b.position);
      if (position.dist(b.position)<=0)
      {
        temp.div(.00001);   
        temp.mult(ATTRACTION*size/sq(.000001));
      }
      else
      {
        temp.div(position.dist(b.position));   
        temp.mult(ATTRACTION*size/sq(position.dist(b.position)));
      }
      velocity.add(temp);
    }
  }

  void getAcceleration(PVector player)
  {
    PVector temp = PVector.sub(player, position);
    temp.normalize();
    velocity.add(temp);
  }
```
