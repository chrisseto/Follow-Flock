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
