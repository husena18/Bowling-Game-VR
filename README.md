# Bowling-Game-VR

1.	Add the “Packages” folder in the main folder.
2.	In the “Library” folder, add the “ArtifactDb” file mentioned in the link.
3.	Paste the DYLIB File into the: 
Library \PackageCache\com.unity.burst@1.8.17\.Runtime\libburst-llvm-16.dylib 


You’ll Find all the files and folders mentioned in the following link:
-	https://nuvuniversity-my.sharepoint.com/:f:/g/personal/husena_limdiwala_nuv_ac_in/Ev2uUoVGcXxNv4jG2P2vPkIBb26QGrXL7hgJv7MQia7tBA?e=Oi9iuV



# Virtual Reality [VR] Bowling Game | By: Husena Limdiwala

Task 1: Set Up Your Unity Project & Configure the VR Environment

1.	Create a New Unity Project:

2.	Install XR Plugins:

2.1.	 Go to Windows > Package Manager
2.2.	Search for the XR Interaction Toolkit and install it.
2.3.	Import XR Plugin Management from the Package Manager. 

3.	Set Up XR Rig:

3.1.	 Hierarchy > XR > XR Rig (Action-based)
3.2.	This rig allows the player to move and interact with the environment in VR. 

4.	Set Up Input Actions:

4.1.	 Go to the XR Interaction Toolkit Input Actions and configure them based on the VR controller. Set up actions for grabbing and interacting with objects.

Task 2: Create the Ground Plane and Add a Skybox:

1.	Create the Ground Plane: 

1.1.	 Hierarchy: 3D object > Terrain (Base)

 

1.2.	Size of the terrain should be set, for example, Width = 100, Length = 100
 

2.	Add a Skybox:

2.1.	 Open the Lighting Settings window by choosing Window > Rendering > Lighting Settings and select your skybox there.

 

2.2.	Under the Environment tab, set a Skybox Material. You can use a default skybox or download one from the Asset Store.

 

2.2.1.	Download from the asset store:

 

2.3.	 Adjust lighting settings to match the chosen skybox (e.g., sunlight direction).

 


 

Task 3: Add Environment Objects:
1.	Use Assets for Environment:
1.1.	Download the 3D model of a bowling alley from Sketchfab.com. 
( https://sketchfab.com/3d-models/bowling-lane-b69132ec17b446efbd84ffd367ec6c4a )
 
1.2.	Add these objects to your scene by dragging them from the Project window into the Hierarchy.
 

2.	Add Grabbable Objects:

2.1.	 Create interactive objects (blue ball) that the player can grab and move. 

 

2.2.	 Add a XR Grab Interactable component to these objects.

The Properties are as follows: 
2.2.1.	Add the Interaction Manager
2.2.2.	Distance Calculation: Collider Volume
2.2.3.	Movement Type: Kinematic
2.2.4.	Check Throw On Detach 
2.2.5.	Throw Smoothening: 0.3
2.2.6.	Throw velocity Scale: 0.7
2.2.7.	Throw Angular Velocity: 0.5
2.2.8.	Use Dynamic Attach

 

2.3.	Set up colliders and rigid body on these objects so they behave as expected when grabbed and dropped. 

The Properties for Collider and rigid body are as follows: 
2.3.1.	Check Provide Contacts
2.3.2.	Mass: 2
2.3.3.	Drag: 0
2.3.4.	Angular Drag: 0.5
2.3.5.	Check Use Gravity
2.3.6.	Uncheck Is Kinematic
2.3.7.	Collision Detection: Continuous

 

 

 

Task 4: Configure Lighting and Shadows:

1.	Add Light Sources:

1.1.	 Add a Directional Light (for general lighting) or Point Lights (for local effects).

 

1.2.	Adjust the intensity, colour, and position of the lights.

 


2.	Enable Shadows:

2.1.	Enable shadows in the Inspector for each light source. Choose between Soft Shadows (for smooth shadow edges) or Hard Shadows (for sharp shadows).
 

2.2.	Go to Project Settings > Quality and adjust the shadow resolution for higher quality shadows.

 
 

Task 5: Add Audio:
1.	Add an Audio Source:
1.1.	 Component > Audio > Audio Source and add it to the object.
 
2.	Assign an Audio Clip:
 

3.	Modify the Script to Play Sound on Ground Collision
 
 

Task 6: Implement Basic VR Interaction:
1.	Set Up the Grabbable Object (Bowling Ball):
1.1.	 Make sure the object has a Rigid body and a Collider component.
 

2.	Add XR Grab Interactable
3.	Configure the Grab Interactable:
As mentioned, steps for XR Grab Interactable in Task 3
  
4.	Add Interactable Object for Pins:
4.1.	Select the pins in the Hierarchy and repeat the process of adding XR Grab Interactable and Rigid body components to them.
 

The Properties for Collider and rigid body are as follows: 
4.1.1.	Material: Bowling Pins Physics
 
 
4.1.2.	Mass: 0.5
4.1.3.	Drag: 0, Angular Drag: 0.05
4.1.4.	Check Use Gravity
4.1.5.	Uncheck Is Kinematic
4.1.6.	Collision Detection: Continuous Dynamic
 
 

Task 7. Write Basic Interaction Script:

 

 


1.	 Ballvelocitylimiter.cs:

 







2.	 Ballthrowhandler.cs:

 

















3.	 Ballgrabandthrow.cs:

 

4.	Bowlingball.cs

 


5.	BallResetManager.cs

 

 


6.	LowCenterMass.cs
 

7.	Pins.cs
 
 

8.	PinKinematicController.cs
 

Task 8: Create a Scoring Mechanism:
 

1.	Create the Score Manager
1.1.	Write a script to keep track of the score when pins are knocked down.
 
 

2.	Create Pin Script:

PinManager.cs
 

3.	Attach Pin Manager game object to the Score Manager:
 ’



4.	Add Score UI:
 

Adjust the position and font size, style and color of the score:
 

Assign the Score Text into the Score Manager field:
 

 

Issues And Solutions:

1. Ball Tossing Mechanic:
Problem: This mechanic tosses the ball too hard so that it bounces into the alley and is never seen again.
I also added the `BallVelocityLimiter` script to ensure that the maximum ball speed and angular velocity is so that it doesn't shoot up uncontrollably in the air.
2. Pin Collision Problem
Problem: Pins collide advanced, or fails to respond appropriately to a collision from the ball.
Solution: Changed the properties of pins and added Rigidbody constraints so that only after the ball's throw is enabled are the pins non-kinematic.
3. Problems associated with the scoring system:
Problem: It was really hard for the game to track which person is winning at what point the frame is reset under multifarious conditions, such as when a thrown ball scores or resets the pins on its own.
4. Pin Stability:
Problem: after having received the ball twice, then the pins began to fall.
Solution: Instead, change the pin control script to be the kinematic state responsible so that the pin is stable until colliding with the ball by the fall.
5. Fine-Tuning for Realism
Configured lighting, shadows, and ambient audio so that the game seems glossy.
Detailed environment objects and optimized the grab-and-throw mechanic in such a way that the player has a seamless VR experience.
Conclusion
The project challenged physics interaction issues, accurate implementations of scoring 
mechanisms, and VR interactivity. There was a huge scripting, debugging, and iteration in fine-tuning things to get a relatively more stable and controlled gameplay, hence forming the basis of the complete implementation of a fully functional VR bowling game with realistic pin interaction, scoring, and immersive audio-visual elements.

 
References:

1.	 https://youtu.be/pI8l42F6ZVc?si=PXnhKMEdN3xHcMI5 
2.	 https://youtu.be/gGYtahQjmWQ?si=N1VKKf6P0KAwVCPc
3.	https://youtu.be/-QngemQx9NY?si=IFw5YL5g4V1BtWXL
4.	https://youtu.be/uGq10Tcl3Ns?si=khoZ6hq0iCBFY5jq
5.	https://chatgpt.com/c/6710f640-48b8-8009-9bc2-bd798629d793

