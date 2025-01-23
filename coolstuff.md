# A Comprehensive Unity Tutorial
### By Bokai Bi, Discord @KoishiHat

## Index
[Philosophical Points](#philosophical-points)  
Basic Unity Concepts  
Basic Scripting  
Advanced Scripting  

# Philosophical Points
Getting ideas right is more important than technical knowledge
- Video games are usually **simple in algorithms but complex in implementation**. Games contain many objects that interact with each other in specific ways, resulting in large amounts of interdependent logic for any large enough project. 
- A good programmer manages the complexity by **abstracting at the correct level**, **reducing redundant code** and **making the code more understandable**. 
  - Please do not overly abstract. **Premature abstraction is the root of all software evils**.
- Programming in Unity, like dealing with any complex API, involves a large amount of **searching things up and referencing the Unity documentation**. Your first step whenever encountering something you don’t know should be **searching online**.
  - Small caveat, I recommend **against** overly relying on “how to do x in Unity” videos. Searching the documentation and trying to put the pieces together will help you improve quickly, while mechanically copying videos online can also result in inappropriate mixing of implementation approaches.
- AI can make development a lot easier, but is **heavily recommended against** for inexperienced developers. If you do want to use AI, make sure you fully understand the code you’re using. 
  - Anecdotally, in-editor tools like Github Copilot works much better than simply asking CharGPT in the browser, as it provides the AI with more context (which gamedev is heavily dependent upon).

# Basic Unity Concepts
Short FAQ:
- What Unity version should I use?
  - Usually I recommend using the newest, but if you work in a team make sure everyone has the same version.
- What license should I get?
  - Personal is completely sufficient. Apply for a student plan if you can and want, but it’s not necessary at all (I’d even say it’s not worth your time).
- What’s the difference between Unity 2D and 3D?
  - Unity is fundamentally a 3D engine - Unity2D is just Unity3D ignoring the z-axis. In this guide, we will use Unity2D as its simplicity allows us to illustrate concepts more clearly  

In this tutorial, I will try to introduce concepts first, and then show concrete examples to illustrate them. You're encouraged to follow along on your own device as it allows you to experiment.  
Let’s get started:

## Concept: A Unity game is made up of Scenes.
- Every moment in a Unity game happens some scene
- You can load scenes additively on top of the current scene, but you can ignore this until needed.
- A scene is a unit of gameplay. The following are common scenes:
  - Title screen
  - Credits
  - Levels
  - Minigames  

Let's create a new project from Unity Hub after installing a Unity editor version:
![image](https://github.com/user-attachments/assets/5854486e-0945-4ca6-ac67-e59666dab762)
This will take a while. Want to follow along? You can kill some time by watching me shill cool things in the collapsed section below (or just browser your phone I guess).
<details>
  <summary>Fun & Joy</summary>  
  
  Catfish  
  ![fish-catfish](https://github.com/user-attachments/assets/07d2f3f8-b917-4cc0-8162-f1ca9c0ca90d)

  [Check out our indie Touhou doujin game Evernight](https://www.instagram.com/evernight_devteam)

  My game recommendations:
  - Touhou Project (the greatest video game series of all time you should check it out)
  - Baba is You
  - Balatro
  - [Flip of Light (by our great composer at Team Evernight)](https://store.steampowered.com/app/2015460/Flip_of_Light/)
  - Ib
  - Outer Wilds
  - Omori
  - Sid Meier's Civilization VI
  - Yume Nikki

  [My best Beat Saber play](https://www.twitch.tv/videos/2196824993)

  
  [My anime list](https://myanimelist.net/profile/KoishiHat)

  Catfish  
  ![catfish-world-yuri-grisendi](https://github.com/user-attachments/assets/443032b9-b45d-42d4-9be0-491c441815c4)
</details>

Project created? You should be greeted with a screen like this:  
![image](https://github.com/user-attachments/assets/73a9d5b4-6635-4413-a5a6-f4824197a209)

It's a lot of stuff! Let's focus on one section at a time. This is the **scene hierarchy**. It displays all the GameObjects in the current scene.  
![image](https://github.com/user-attachments/assets/5cb8cdf7-68b0-41c0-827a-317d018a9f6e)

## Concept: A scene is a hierarchy (tree) of GameObjects.
A GameObject is the fundamental building block of your scenes. The following are all GameObjects (or groups of them):
- Player character
- Enemies
- Game environment
- UI Button
- Particle effect generator
- Or anything in the game, really

We are going to make a rudimentary "platformer" today. Let's first try to create an object to be our platform. You can right click in the hierarchy and click "Create Empty", name the object "platform".  
![image](https://github.com/user-attachments/assets/4531db4f-d77f-439d-b98e-a0f75bdfcc1c)  
If you select the object and look in the Scene tab, you should see... nothing.  
![image](https://github.com/user-attachments/assets/48625f06-e7c9-4428-b3f6-22b4acab0d47)  
Why is that?

A GameObject, by itself, does not do anything. It has no appearance, no behavior, no interaction with other objects, nothing. Technically, all GameObjects come with a transform (position, rotation, and scale). However, a transform doesn’t mean anything when the object has no behavior.  
## Concept: A GameObject can have an arbitrary amount of components. Components are solely responsible for all behaviors of GameObject. 
The following are common components:
- SpriteRenderer: Renders a sprite (image) where the object is.
- BoxCollider2D: A collider to either enable collision or collision detection (trigger)
- Rigidbody2D: Gives an object physics simulation.
- Animator: Animates objects by changing arbitrary properties of components over time
- Camera: The camera! The game will not render if there is no object with a camera component attached in the scene.
- Tilemap: A 2D tilemap. ~~My biggest enemy~~

Let's make our platform visible by adding the "sprite renderer" component. Select the object, then click "Add Component" in the Inspector tab. Search for "Sprite Renderer" and add it.  
![image](https://github.com/user-attachments/assets/7e71d28b-ced6-403c-be8e-b134f1f90631)
You just added a Sprite Renderer to your object, but it doesn't know what sprite to render. Let's add a sprite to it. Here I'm using an image I grabbed from Wikipedia.  
![Ameiurus_melas_by_Duane_Raver](https://github.com/user-attachments/assets/3616b011-2b0c-4e37-ac88-e7ce4af44bfe)
Drag the image into the Assets tab in the bottom to import it as a sprite asset. You can now drag the asset to the Sprite slot in the SpriteRenderer component.  
![image](https://github.com/user-attachments/assets/93a2174f-26dc-4043-a964-bfa3bf5218ad)  
The platform arrives! You can click the Game tab (right of the Scene tab) to see how it looks in-game.  
![image](https://github.com/user-attachments/assets/c5ef1c9c-2545-4aaf-8cb7-869d5c82db34)  
The platform is way too big. To fix this, go back to the Scene tab and make it a proper platform by using the transform tools or by changing the numbers in the transform component of the platform (try both!).  
Now, let's add a player character. In the hierarchy, right click and add a 2D Object -> Sprites -> Triangle, name it "Player". Note that this is **completely** equivalent to creating an empty object, adding a SpriteRenderer, then making it render a triangle sprite.  
![image](https://github.com/user-attachments/assets/94251cee-b28d-4c61-842f-7c7021c4499e)  





