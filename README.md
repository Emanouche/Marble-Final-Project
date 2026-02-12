# Project Title
Marble Course
## Synopsis
This is part of my final project at Southwest Tech. I made a small marble platforming course featuring 5 short levels. When Player starts the game they are welcome to a small intro screen which tells them the controls and contain s a start button that when clicked starts the game. The objective of each level is to read the red goal to go to the next level. It contains various scripts which allows level transition, control of the marble with wasd + space to jump, camera following the ball, triggers to move on to different scenes/levels, reset the marble when it makes contact with an invisible kill zone underneath the level when players fall off the level, moving platforms between two points and the ability to quit a build of the game when pressing the escape key. 

## Motivation
I did this for my final project in my Software Development course at Southwest Technical College. I'm interested in game development and wanted to have a bit more practice with Unity. This project looks basic, but taught me a lot about how C# scripts and objects interact in Unity and how to design simple levels as well as to how smoothly transition between multiple scenes

## How to Run
To run it is simple, import the folder in this repository as a project in Unity. Then you can look at the files, levels, scripts, etc. You can also make a build out of the project to be able to run the game outside of the editor. I used Unity version 6000.2.7f2 for this project.

## Code Example
I made 9 C# scripts total for this project to run smoothly, here is one which basically allows the player to move the marble around and make it jump. using wasd + space.
```
using UnityEngine;

public class MarbleController : MonoBehaviour
{
    [Header("Movement Settings")]
    public float moveForce = 10f;    // Strength of movement force
    public float jumpForce = 5f;     // Strength of jump impulse

    [Header("Ground Check")]
    public float groundCheckDistance = 0.6f; // How far the raycast checks for ground
    public LayerMask groundLayer;            // Which layers count as ground

    private Rigidbody rb; // Rigidbody reference

    void Start()
    {
        rb = GetComponent<Rigidbody>(); // Cache Rigidbody
    }

    void FixedUpdate()
    {
        HandleMovement(); // Movement logic
        HandleJump();     // Jump logic
    }

    void HandleMovement()
    {
        float h = Input.GetAxis("Horizontal"); // Left/Right input
        float v = Input.GetAxis("Vertical");   // Forward/Back input

        // Camera directions
        Vector3 camForward = Camera.main.transform.forward;
        Vector3 camRight = Camera.main.transform.right;

        // Remove vertical tilt
        camForward.y = 0f;
        camRight.y = 0f;

        camForward.Normalize(); // Clean vectors
        camRight.Normalize();

        // Movement relative to camera
        Vector3 moveDir = camForward * v + camRight * h;

        rb.AddForce(moveDir * moveForce); // Apply movement force
    }

    void HandleJump()
    {
        // Jump only when grounded and Space is held
        if (Input.GetKey(KeyCode.Space) && IsGrounded())
        {
            rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse); // Jump impulse
        }
    }

    bool IsGrounded()
    {
        // Raycast downward to detect ground
        return Physics.Raycast(transform.position, Vector3.down, groundCheckDistance, groundLayer);
    }
}
```

## Screenshot
Here is a screenshot of the project
<img width="1365" height="718" alt="Screenshot level 5" src="https://github.com/user-attachments/assets/a8a72d04-ce74-4a81-8731-427966c7d96f" />


