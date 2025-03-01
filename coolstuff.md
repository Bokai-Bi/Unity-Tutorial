# A Conceptual Tutorial to Unity
### By Bokai Bi, Discord @KoishiHat

## Index
[Philosophical Points](#philosophical-points)  
[Basic Unity Concepts](#basic-unity-concepts)  
[Basic Scripting](#basic-scripting)  
[Advanced Scripting](#advanced-scripting)  

This tutorial focuses on a foundational understanding of how Unity works rather than knowledge on how to do specific things, which from experience is often what beginners lack. This will be comparatively dense and read more like a textbook. For a more gentle introduction, check out [this](https://www.youtube.com/watch?v=XtQMytORBmM) video.

# Philosophical Points
> Getting ideas right is more important than technical knowledge
- Video games are usually **simple in algorithms but complex in implementation**. Games contain many objects that interact with each other in specific ways, resulting in large amounts of interdependent logic for any large enough project. This **will** be different from programming you've done in the past.
- A good game programmer manages the complexity by **abstracting at the correct level**, **reducing redundant code** and **making the code more understandable**. 
  - Please do not overly abstract. **Premature abstraction is the root of all software evils**.
- Programming in Unity, like dealing with any complex API, involves a large amount of **searching things up and referencing the Unity documentation**. Your first step whenever encountering anything you don’t know should be **searching online**.
  - Small caveat, I recommend **against** overly relying on “how to do x in Unity” videos. Searching the documentation and trying to put the pieces together will not only help you improve quickly, but also allow you to customize your solution for your specific usecase. When you watch those videos, try to make sure you understand why things are done the way they are.
- AI can make development a lot faster, but is **heavily recommended against** for inexperienced developers. If you do want to use AI, make sure you fully understand the code you’re using. 
  - Anecdotally, in-editor tools like Github Copilot works much, much better than simply asking CharGPT in the browser, as it provides the AI with more context (which gamedev is heavily dependent upon).

# Basic Unity Concepts
> That's a LOT of concepts

Short FAQ:
- What Unity version should I use?
  - Usually I recommend using the newest, but if you work in a team make sure everyone has the same version.
- What license should I get?
  - Personal is completely sufficient. Apply for a student plan if you can and want, but it’s not necessary at all (I’d even say it’s not worth your time).
- What’s the difference between Unity 2D and 3D?
  - Unity is fundamentally a 3D engine - Unity2D is just Unity3D ignoring the z-axis. In this guide, we will use Unity2D as its simplicity allows us to illustrate concepts more clearly.  

In this tutorial, I will try to introduce concepts first, and then show concrete examples to illustrate them. You're heavily encouraged to follow along on your own device as it allows you to experiment.  
Let’s get started:

## Concept: A Unity game is made up of Scenes.
- Every moment in a Unity game happens in some scene.
- A scene is a distinct unit of gameplay. The following are common scenes:
  - Title screen
  - Credits
  - Levels
  - Minigames  

Let's create a new project from Unity Hub after installing a Unity editor version:
![image](https://github.com/user-attachments/assets/5854486e-0945-4ca6-ac67-e59666dab762)
This will take a while. Want to follow along? You can kill some time by watching me shill cool things in the collapsed section below (or just browse your phone I guess).
<details>
  <summary>Fun & Joy</summary>  
  
  Catfish  
  ![fish-catfish](https://github.com/user-attachments/assets/07d2f3f8-b917-4cc0-8162-f1ca9c0ca90d)  

  [My anime list](https://myanimelist.net/profile/KoishiHat)  

  [Check out our indie Touhou doujin game Evernight](https://www.instagram.com/evernight_devteam)

  My game recommendations:
  - Touhou Project (the greatest video game series of all time you should check it out)
  - Baba is You
  - Balatro
  - [Flip of Light (very cool platformer)](https://store.steampowered.com/app/2015460/Flip_of_Light/)
  - Ib
  - Outer Wilds
  - Omori
  - Sid Meier's Civilization VI
  - Yume Nikki

  [My best Beat Saber play](https://www.twitch.tv/videos/2196824993)

  Catfish  
  ![catfish-world-yuri-grisendi](https://github.com/user-attachments/assets/443032b9-b45d-42d4-9be0-491c441815c4)
</details>

Project created? You should be greeted with a screen like this:  
![image](https://github.com/user-attachments/assets/73a9d5b4-6635-4413-a5a6-f4824197a209)

It's a lot of stuff! Let's focus on one section at a time. This is the **scene hierarchy**. It displays all the GameObjects in the current scene.  
![image](https://github.com/user-attachments/assets/5cb8cdf7-68b0-41c0-827a-317d018a9f6e)

## Concept: A scene is a collection of GameObjects.
A GameObject is the fundamental building block of your scenes. Everything in your game is made up of one or more GameObjects:
- Player character
- Enemies
- Game environment
- UI Buttons
- Anything in the game, really

A GameObject, by itself, is an empty container that only has a transform (position, rotation, and scale). It has no behavior otherwise.
We are going to make a basic "platformer" today. Let's first try to create an object to be our platform. You can right click in the hierarchy and click "Create Empty", name the object "platform".  
![image](https://github.com/user-attachments/assets/4531db4f-d77f-439d-b98e-a0f75bdfcc1c)  
If you select the object and look in the Scene tab, you should see... nothing.  
![image](https://github.com/user-attachments/assets/48625f06-e7c9-4428-b3f6-22b4acab0d47)  
This makes sense since an empty GameObject has no behavior. To make it show a platform, we can add a new component to it.

## Concept: A GameObject can have an arbitrary amount of components. Components are solely responsible for all behaviors of a GameObject. 
The following are common components:
- SpriteRenderer: Renders a sprite (image) where the object is.
- BoxCollider2D: A collider for collision
- Rigidbody2D: Gives an object physics simulation.
- Animator: Animates objects by changing properties of components over time
- Camera: The camera! The game will not render if there is no object with a camera component attached in the scene.

Let's make our platform visible by adding the "sprite renderer" component. Select the object, then click "Add Component" in the Inspector tab. Search for "Sprite Renderer" and add it.  
![image](https://github.com/user-attachments/assets/7e71d28b-ced6-403c-be8e-b134f1f90631)  
You just added a Sprite Renderer to your object, but it doesn't know what sprite to render. Let's add a sprite to it. Here I'm using an image I grabbed from Wikipedia.  
![Ameiurus_melas_by_Duane_Raver](https://github.com/user-attachments/assets/3616b011-2b0c-4e37-ac88-e7ce4af44bfe)  
Drag the image into the Assets tab in the bottom to import it into Unity as a sprite asset. You can now drag the asset to the Sprite slot in the SpriteRenderer component.  
![image](https://github.com/user-attachments/assets/93a2174f-26dc-4043-a964-bfa3bf5218ad)  
The platform arrives! You can click the Game tab (right of the Scene tab) to see how it looks in-game.  
![image](https://github.com/user-attachments/assets/c5ef1c9c-2545-4aaf-8cb7-869d5c82db34)  
The platform is way too big. To fix this, go back to the Scene tab and make it a proper platform by using the transform tools or by changing the numbers in the transform component of the platform (try both!).  
![image](https://github.com/user-attachments/assets/ba4ab3e8-5e6f-40bc-9918-fc61a651fd5b)(These are the transform tools)

Now, let's add a player character. In the hierarchy, right click and add a 2D Object -> Sprites -> Triangle, name it "Player". Note that this is **completely** equivalent to creating an empty object, adding a SpriteRenderer, then making it render a triangle sprite.  
![image](https://github.com/user-attachments/assets/94251cee-b28d-4c61-842f-7c7021c4499e)  

If you click on the Play button on the top of the window, you'll see that... nothing happens. This is because the only components we've given our objects are SpriteRenderers - they render sprites, but nothing more.  
To fix this, let's give our player character physics simulation. Let's add a Rigidbody2D component to the Player object.  
![image](https://github.com/user-attachments/assets/e9a13104-c57b-4abc-857b-cf557d44af44)  
That's a lot of fields! We don't have to worry about them for now.
<details><summary>I want to know more about how each of the fields in Rigidbody2D works!</summary>
Recall the philosophy section - you should search it up online, it's a good skill :)  
  
![Buy a man eat fish, He day, Teach fish man To a lifetime](https://github.com/user-attachments/assets/8ca4b6f5-aacf-4620-8fa0-b0a8803416fc)
</details>  

Now click the play button again. What happens?  
The player fell through the platform. The Rigidbody2D subjected the player to gravity, but neither the player nor the platform has a collider. To make the player stand on the platform, add a BoxCollider2D component to both objects.

Click play again, now the player correctly stands on the platform!
![image](https://github.com/user-attachments/assets/df960c60-c7cf-41f2-8d1f-402243a5dc92)

# Basic Scripting
> This is cute and all, but I thought we’re doing coding?  

Unity only comes with so many built-in components. Sometimes you want something slightly different from a built-in component, other times what you want isn’t included at all! It’s time to write your own components (yay!)

## Concept: A custom component (aka “script”) is a developer-written C# class that inherits from MonoBehavior.
- Don't worry about what MonoBehavior means - in short, it marks a class as a Unity component that can be attached to GameObjects.
- You can attach it to GameObjects to give them custom behavior you designed via code.
- Most C# ideas (control flow like `if` and `for`, data structures like `List`s) work normally. We will focus on Unity-specific mechanisms.
- This is your chance to write arbitrary code - let your imagination run wild! 

Going back to our "platformer" example. We now want to allow the player to control the player character object horizontally. There are a lot of ways to achieve player movement, and Unity can't provide them all. Let's therefore write our own player control component.  
Attach a new component to the player object, type in "PlayerMovement", and click "New Script". Once you have created the new script, open it from the Assets tab to start editing.  

![image](https://github.com/user-attachments/assets/e756f8ab-882a-46f0-9be5-38e321c402b0)  
This is how the file should look like (I'm using Visual Studio Code, which I also recommend for beginners). Let's break this down.
- The class PlayerMovement derives from MonoBehavior. This class is the component that is attached to GameObjects.
  - You can declare additional classes in the file, for example if you need a custom data structure. Those classes will not be part of the component.
- The functions `Start` and `Update` are special Unity functions that are called by the engine at specific points (see image). 
- You are free to add additional helper functions and member variables to the class. Your helper functions will not be automatically called by Unity.

Now, I'll give you the building blocks you need to implement movement. Try to do it yourself before checking my solution!
<details>
  <summary>Unity API</summary>  
  
  - `gameObject` - the name `gameObject` is a variable of type `GameObject` that refers to the GameObject the script is attached to.
  - `GetComponent<T>()` - A member function of the `GameObject` class that returns the component T attached to the GameObject that the member function is called on. In plain words, `gameObject.GetComponent<Transform>()` will give a reference to the `Transform` component on the current GameObject.
  - `transform.position` - A `Vector3` that represents the position of a transform. Editing individual fields is not allowed, but reassignment is okay. E.g. `transform.position.x += 1;` will not compile, but `transform.position += new Vector3(1,0,0);` is valid.
  - `Time.deltaTime` - A float value that represents how many seconds have past since the last frame. (Why is this important?)
  - `Input.GetKey(keycode)` - Returns a boolean on whether the key with `keycode` is pressed in the current moment. Keycodes are generally in the format of `KeyCode.W` for the W key, when unsure check Unity documentation.
</details>

<details>
  <summary>Reference Answer</summary>

  ![image](https://github.com/user-attachments/assets/f8dcf2fd-f356-48b5-9d3d-ba1de70666c1)

  On every frame, we check whether A/D is pressed. If so, we increment the position on the x-axis by a variable `speed`. You will notice that we are multiplying by a value `Time.deltaTime`, which gives the amount of seconds since the last frame. Why is this necessary? Let's consider a case without it. `Update()` is called once a frame. Suppose we do simply do `transform.position += new Vector3(speed,0,0)`, the player will be moved speed\*60 units to the right on a computer running the game at 60 frames per second, while only moving speed\*30 units to the right on a computer running 30fps. In fact, if a computer fluctuates its framerate, your player will be moving at a variable speed. Think about how multiplying by `Time.deltaTime` removes the effect of framerates.
</details>

<details>
  <summary>Exercise on deltaTime</summary>

  Which one of the following needs to be adjusted by deltaTime?
  - Enlarging an object by a constant rate in `Update()`
    - Yes
  - Smoothly moving an arrow from one UI element to another 
    - Yes
  - Teleporting an object from one place to another
    - No
      
</details>

Now, your player should move correctly on the platform! But our job is not over yet. Making a good game involves a lot of numerical tweaking to improve player experience. Right now, if you want to change the player speed, you'll have to change it in the script and re-compile. To make the process quicker, declare the `speed` variable either as `public float speed` or `[SerializeField] float speed`. You should now see this field you can edit in the editor.  
![image](https://github.com/user-attachments/assets/8ad833ed-3bb7-4015-bf76-f32dabe8abef)  
<details>
  <summary>What's the advantage of making fields editable in editor?</summary>  

  - You get to change values faster without having to edit code and recompile.
  - You can have multiple instances of the same component that give different behavior.
    - For example, you can write a component `rangedEnemy.cs` and make `int health`, `float speed`, `float damage`, and `GameObject projectile` editable fields in the editor. Then, you can attach the same component to multiple enemies and have them behave differently depending on the fields, instead of having to write multiple scripts. 
</details>  
<details>
  <summary>What is a SerializeField?</summary>  
  Unity makes all public variables editable in the editor. If you want to make a private variable editable, you'll need to mark it [SerializeField]. 
</details>

Recommended Exercises:
- Try to make another GameObject with the `PlayerMovement` component in the scene and give it a different speed in editor. How does it work?
- Declare an in-editor editable GameObject variable inside `PlayerMovement` and drag an object from the hierarchy into the field in the Unity editor. You now have a reference to an in-scene GameObject in your script. Try to do fun things with it in your code! (try `Instantiate` and `Destroy`, be careful about putting things directly in `Update` if you don't want it to execute every frame).

In the last step of this guide I want you to create an obstacle that deletes the player GameObject upon contact. Following the spirit of this guide, you'll be figuring out yourself how to do it using things we learned thus far and your favorite search engine for whatever you don't know how to do. Have fun!

# Advanced Scripting
> When you're too deep into the rabbit hole

This is a bonus section - a bunch of useful tools that would be helpful as you find your current tools insufficient. We'll only go into their general purpose here, for more detail please consult the documentation.
<details>
  <summary>Coroutines</summary>
  
  A coroutine is a separate, concurrently running "thread". Suppose you want to do x every frame for 10 seconds, then do y once and wait for 5 seconds, then finally for 20 seconds do z every 1.5 seconds. You can achieve this through a lot of conditionals in `Update`, but a more performant and readable approach would be to use Coroutines.  
  ```
  # declare the coroutine
  IEnumerator doStuff(string arg1) {
    Debug.Log(arg1); # coroutines can take arguments too!
    float startTime = Time.time; 
    while (Time.time < startTime + 10) {
      x();
      yield return null; # pause execution of coroutine, then resume next frame
    }
    y();
    yield return new WaitForSeconds(5); # pause execution for 5 seconds
    startTime = Time.time;
    while (Time.time < startTime + 20) {
      z();
      yield return new WaitForSeconds(1.5f);
    }
  }
  void SomeDriver() { 
    StartCoroutine(doStuff("HI")); # a driver starts the coroutine using StartCoroutine
  }
```
</details>
<details>
  <summary>Global Static State</summary>

  What if you want to store some data that persist through scene changes and can be accessed from anywhere in the game (e.g. settings)? One possible way to do this is through the `static` keyword. When you declare a variable as `static`, the variable belongs to the class rather than specific instances of the class. This means that its value persists through scenes and can also be accessed from the class name alone. Here's an example:  
  ```
# inside Settings.cs
public static int volume; # this can be read and write from anywhere else using Settings.volume.
```  
Note that in order to access a variable from other classes, it must be `public`. When not specified, C# variables default to `private`  
Another thing static variables are used for is to provide a reference to a sole-instance. For example, if you know only one GameObject will ever have the `Player` component, you can provide an easily accessible reference to the player object by doing this:  
```
# inside Player.cs
public static Player player;
void Start() {
  player = this;
}
```  
Upon initialization, the player would set the static class variable `player` to itself. Now, any other class can easily access the player by the name `Player.player`.
</details>

<details>
  <summary>Interfaces</summary>
  
  Suppose you have 50 different kinds of enemies, each with their own class. You want to write some code that can do something (e.g. deal damage) to any enemy. How would you do it? One way to do this is through interfaces. An interface is a specification that provides some number of functions. A class is said to implement the interface if it implements all functions specified by the interface. 
  ```
  # inside IEnemy.cs
  public interface IEnemy {
    public void TakeDamage(float damage);
    public string getName();
  }

  # inside each of your enemy scripts
  public class EnemyType1 : MonoBehavior, IEnemy { # specifies that EnemyType1 implements IEnemy
    public void TakeDamage(float damage) {...}
    public string getName() {...} # A class must implement all functions specified by its interfaces
  }

  # inside some code elsewhere
  public void DealDamage(IEnemy enemy, float amount) {
    enemy.TakeDamage(amount); # any class that implements IEnemy can be passed in as enemy here.
  }
  ```
</details>
