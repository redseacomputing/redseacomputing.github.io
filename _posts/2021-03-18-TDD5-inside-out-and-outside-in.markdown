---
layout: post
title:  "TDD for kickstarters- part 5"
date:   2021-03-30 18:19:46 +0100
categories: tdd java
permalink: /:year/:title
---

![design from point of view](../images/TDD5-design-from-point-of-view.png)

## Design from your point of view

For the following read I would like to demonstrate the different approaches with the Mars Rover exercise.
Don't worry, it's for illustrative purposes only.
<br>
<br>
### [Mars Rover](https://kata-log.rocks/mars-rover-kata)

#### Task:

You’re part of the team that explores Mars by sending remotely controlled vehicles to the surface of 
the planet. Develop an API that translates the commands sent from earth to instructions that are 
understood by the rover.

#### Requirements:

* You are given the initial starting point (x,y) of a rover and the direction (N,S,E,W) it is facing.
* The rover receives a character array of commands.
* Implement commands that move the rover forward/backward (f,b).
* Implement commands that turn the rover left/right (l,r).
* Implement wrapping at edges. But be careful, planets are spheres. Connect the x edge to the other x edge, so (1,1) for x-1 to (5,1), but connect vertical edges towards themselves in inverted coordinates, so (1,1) for y-1 connects to (5,1).
* Implement obstacle detection before each move to a new square. If a given sequence of commands encounters an obstacle, the rover moves up to the last possible point, aborts the sequence and reports the obstacle.

### Inside out Design

Inside out testing means that you start test-driving internal
parts of your implementation and putting them all together at the end
for a complete solution.

So, a Mars Rover possibly can:

    
        void left(){
            //Implementation here
        }
        void right(){
            //Implementation here
        }
        void toHomebase(){
            //Implementation here
        }
        int validatePower(){
            //Implementation here
        }



And put them together:

    void go(char... commandsFromEarth){
        for(int i = 0; i < commandsFromEarth.length; i++){
            if(commandsFromEarth[i] == L) left();
            if(commandsFromEarth[i] == R) right();
            .
            .
            .
        }
    }

So you have test driven all the pieces of the jigsaw 
and then you are going to put the jigsaw together to create a method that executes the instructions
with your internal parts.

#### Advantages
* You clearly see where the code is broken or messed up.

#### Disadvantages
* It more close couples your tests to your internal design (your code) and unencapsulates it.
* It is possible that your internal parts does not perfectly fittes together.

> In a multi-layered design, you can end up with Inside-Out in the debugger more often you probably would like.

### Outside in Design

The kind of the API to your Mars rover is a method call that
accepts a sequence of character instructions:
L... turning left
R... turning right
F... move forward
B... move backward
 
    @Test
    public void testMoveForwardCommand(){
        Rover rover = new Rover(0,0,'N');
        char forward = 'F';
        rover.go(forward);
        assertEquals(1, rover.getYCoordinate());
    }

In this approach, all tests are written on that level (client side). They are all
basically going through the API (the go() method).

#### Advantages
* The tests does not have to be maintained that much.
* It low couples the tests from production code

#### Disadvantages
* It is not a comprehensive test coverage possible

>I recommend this interesting article on Outside-In from [Merciless refactorer- Gregor Riegler](https://gregorriegler.com).


This is part five of the TDD kickstart beginner series. Here is [part 6](https://redseacomputing.github.io/2021/TDD6-test-doubles)