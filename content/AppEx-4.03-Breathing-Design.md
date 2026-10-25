
# Application Exercise: Inheritance Design for Breathing Activity

First, view the demonstration video at:

https://video.byui.edu/media/t/1_e36t63t0 (approx. 5 minutes)

Then you and your team will begin to design the first two classes: `Activity` which is responsible for attributes and behaviors common to all activities, and `BreathingActivity`, responsible for attributes and behaviors specific to meditative breathing but distinct from meditative reflecting or listing.

You have identified the following potential attributes and behaviors:

| candidate member   | description                                  |
| ------------------ | -------------------------------------------- |
| _name              | activity's name                              |
| _description       | activity's description                       |
| _duration          | how long the user wants the activity to last |
| ShowPrologue()     | display the activity's name and description  |
| ShowEpilogue()     | display a concluding message                 |
| ShowSpinner(int s) | show an animation for `s` seconds            |
| BreatheIn()        | display breathing instruction                |
| BreatheOut()       | display breathing instruction                |

## Question

Which candidates belong in the base `Activity` class? Which belong in the derived `BreathingActivity` class? Which belong neither -- possibly some other class? Jot down your reasoning for why each candidate does or does not belong in a given class.

### option A

![Option A](BreathingA.png)

### option B

![Option B](BreathingB.png)

### option C

![Option C](BreathingC.png)

### option D

Some other inheritance design. (Sketch it now. Jot down your reasons, identifying one concrete advantage to your design that makes it superior to the other three choices. Be prepared to draw it on a whiteboard and defend your design in the classroom.)

## After discussion: continue designing

You still need to decide how a class for the reflection activity, another for the list-writing activity, and the `Main` method of `Program.cs` fit into your design. Revise as you feel inspired. Design an additional helper class if you think of one that has a clear responsibility and doesn't fit naturally in the existing classes.
