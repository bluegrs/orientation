# Welcome to _blueGRS_!
Documentation for new team members to familiarize with blueGRS workflow.

Files to generate the images used in this readme are located in the repository
in case documentation updates are required.

## Current Projects

**Blueberry-Pi**

> A glove that tracks the user's hand orientation precisely with 9 degrees of freedom. The glove sends a server hand orientation data wirelessly to be used as a controller for video games, simulation, or 3D modeling. The project will also include a driver that the server can install to communicate with the device and interpret the data that it sends.

**Dark Blue Sky**

> A space exploration video game where the player is a most-wanted space pirate who wonders around space stealing money from travelers, racing around asteroids at high speed, and running away from space police. _Dark Blue Sky_ is designed to be the first Blueberry-Pi compatible software, showing one practical way that the glove could be used.

## Git Workflow
**Summary**

> All _blueGRS_ repositories must follow this workflow in order to ensure a working 
version is always publicly available. New team members can run a working version
of the project on the master (release) branch before jumping into the development 
(staging) branches to add new features.

![github_workflow](https://user-images.githubusercontent.com/40513675/58377950-79deb980-7f58-11e9-8f16-8db008be333c.jpg)

_NOTE: Click to view a larger, higher quality version of this image._

**Contact**

Daniel Hamilton [(@sweatpantsdanny)](https://github.com/sweatpantsdanny).

**File Generator Directory**

[Git Workflow Directory](https://github.com/bluegrs/orientation/tree/master/git_workflow)

## Code Standards
**Summary**

> Because _blueGRS_ is a team-based project, several members of a team may contribute to each file. Readable code is better code - don't be afraid to overcomment. At the minimum, each chunk of code should have a comment at the beginning summarizing the goal of the function, if-branch, for-loop, etc. and the expected inputs and outputs. Below are some ideas that may be helpful for communicating the goal of your code.

- **A brief summary of the whole file at the top of the document..**
```c#
/*
 *  DESCRIPTION:
 *  This class implements all PLAYER-specific movement controls.
 *  
 *  UPDATES:
 *  5/19/2019 - Horizontal and jumping player movement.
 *  
 *  TODO:
 *  ~ If the player is touching the side of the ground tilemap,
 *    do something to stop the player from jumping infinitely.
 *  ~ Make everything related to Time.deltaTime so it runs the same
 *    on all computers.
 */

using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
```

- **Function names that make sense..**

```c#
private void GetVerticalMovement()
```
```c#
private void SetStartingTime()
```
```c#
public void LoadStartingRoom() 
```

- **Enough comments that the reader doesn't have to decipher your code to understand its goals..**
```c#
// This function checks if the left (a) or right (d) buttons are 
// being pressed and sets the player velocity.
private void GetHorizontalMovement() {

    Vector2 move = Vector2.zero;

    // Sets x to either -1f, 0, or 1 to show that the player
    // is moving left, not moving, or moving right.
    move.x = Input.GetAxis("Horizontal");

    // Evaluate if the player and its children need to flip directions
    // based on horizontal player movement.
    // NOTE: If player is facing RIGHT and the LEFT button is being pressed.
    //       OR if the player is facing LEFT and the RIGHT button is pressed.
    if (    move.x > 0 && transform.localScale.x == -1
        ||  move.x < 0 && transform.localScale.x == 1   )
    {
        // Flip the X scale and keep all other scaling properties the same.
        transform.localScale = new Vector3(transform.localScale.x * -1f,
            transform.localScale.y, transform.localScale.z);
    }

    // Adjust the player's velocity.
    rigidbody.velocity = new Vector2(move.x * moveSpeed,
        rigidbody.velocity.y);
 }
 ```
