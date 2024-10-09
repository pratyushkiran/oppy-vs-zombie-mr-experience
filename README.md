# Oppy vs Zombie MR Experience in Unity Game Engine

Sure! I'll break down the steps described in the documentation for setting up a Mixed Reality experience in Unity using the Meta SDK, specifically for Meta Quest 3 and Quest Pro. The goal of the experience is to enable passthrough of the physical environment, understand the scene (i.e., mapping of real-world objects), and allow interactions between virtual objects and the physical world using Unity's tools and Meta's SDK.

### Steps Breakdown:

### 1. **Downloading the Base Project**

Meta has provided a Unity project that is pre-configured with Meta SDK version 60. The project includes necessary settings and configurations to simplify the process:
   - **Download the project** from a GitHub link provided in the documentation (use the link provided in the video description).
   - **Open the project** in Unity Hub using Unity editor version `2022.3.13f1 LTS` or higher. Ensure this version is used as the Depth API requires this or later versions of Unity.

### 2. **Unity Project Setup**

   - **Switch Platform to Android**: 
     - Open `File` > `Build Settings`.
     - Select `Android` and then click on `Switch Platform` (Quest 3 and Quest Pro use Android as the underlying OS).

   - **Create a New Scene**:
     - In the `Scenes` folder, create a new scene named `MRExperience`.
     - Double-click the scene to open it.

### 3. **Setting Up for Mixed Reality**

   Meta’s SDK provides tools to make Mixed Reality setup easier. You'll be using **Meta’s Building Blocks** for this, a set of tools that simplify the process of setting up MR in Unity.

   - **Access Building Blocks**:
     - Go to `Oculus Tools` > `Building Blocks`. 
     - This will open a window that you can dock for easy access.

   - **Replace Main Camera**:
     - Delete the `Main Camera` from the scene.
     - In the Building Blocks window, add a **Camera Rig** to your scene. This will handle tracking for the headset and hand movements.

   - **Testing the Default Setup**:
     - Connect your Meta Quest headset to your laptop via **Link** or **Air Link**.
     - Press **Play** to test. You’ll be able to see the default virtual environment, though hand visuals are not yet set up.

### 4. **Enable Passthrough**

Passthrough allows you to see the physical world while wearing the headset.

   - In the Building Blocks window, search for `PassThrough`.
   - Click to enable **Passthrough**. This will:
     - Add the **OVR Passthrough Layer**, enabling passthrough functionality.
     - Change the `OVR Manager` settings to enable passthrough support.

   - **Test Passthrough**:
     - Press **Play** to see the passthrough effect where your physical environment becomes visible in the headset.

### 5. **Enable Scene Understanding**

Scene Understanding allows your app to interact with the physical world by recognizing real-world objects like walls, tables, floors, etc.

   - In Building Blocks, search for `EffectMesh`.
   - Click to add it to the scene. This adds:
     - An `Effect Mesh` component that generates meshes over the real-world objects.
     - The `MUtilityKit` with the `MUK` script, which lets you query the physical environment (e.g., position of walls or tables).

   - **Set Mesh Collider**: 
     - Enable **Colliders** on the Effect Mesh so virtual objects can interact with the real world (e.g., colliding with physical objects like walls).

   - **Customize Mesh Generation**:
     - By default, the mesh will be generated for all objects in the scene (walls, floors, tables, etc.). If you want to target specific objects:
       - In the `Labels` option, you can choose which scene objects to generate meshes for (e.g., only the floor or walls).
     
   - **Testing Scene Understanding**:
     - Press **Play** to see the generated meshes. Your scene will show the physical objects, like tables and walls, represented as meshes.

### 6. **Setting Custom Mesh Materials**

If you want different materials for different scene objects:
   - **Duplicate the Effect Mesh**:
     - Create two separate Effect Meshes, one for the floor and one for the rest of the objects (e.g., walls).
   - **Assign Materials**:
     - Assign different materials for each mesh (e.g., assign one material for the floor, another for walls).
   - **Set Initialization Order**:
     - Remove the individual `MUK Start` components from each Effect Mesh.
     - Use the `MUtilityKit` to initialize the meshes in the correct order, ensuring a proper execution sequence.

### 7. **Adding Interactions and Virtual Objects**

To interact with virtual objects using hand tracking and controllers:
   - **Add Controllers and Hand Tracking**:
     - In Building Blocks, search for `Controllers` and `Hand Tracking`. Add them to your scene.
     - This will add left and right controllers as well as hand tracking.

   - **Add Hand Grab Interaction**:
     - Search for `Grabbable Item` in Building Blocks. 
     - Add it to the scene. This creates grab interactors for left and right hands.
     - Delete the default grabbable item, as it’s not needed.

   - **Test Hand Tracking**:
     - Press **Play** to see your hands tracked. When you grab a controller, the system should automatically switch from hand tracking to controllers.

### 8. **Adding Virtual Objects**

You can add virtual objects to the scene that interact with the physical world:
   - **Import Unity Package**: 
     - Download and import the package from the description (the package contains the visual effects, prefabs, scripts, and audio files necessary for the experience).
   
   - **Game Setup**:
     - Create an empty GameObject in your scene and name it `EnemySpawner`.
     - Add the `FindEnemySpawnLocation` component to the spawner, which allows you to randomly spawn enemies within the physical room. Assign a spawn object (e.g., a coffin prefab) for the enemies.

   - **Create NavMesh for Movement**:
     - Create another empty GameObject and name it `NavMeshGenerator`.
     - Add the `GenerateNavMesh` component. This generates a navigation mesh (NavMesh) during runtime, allowing virtual enemies to move around your physical environment.
     - After the room initialization is complete, the NavMesh will be generated, and the enemies will spawn at random locations.

### 9. **Finalize and Customize Experience**

   - **Custom Character and Interactions**:
     - Add the OPI character prefab to your scene, which can be controlled via the controller’s joystick. OPI can also jump over physical objects.
     - Add enemies that spawn in random locations. These can walk around the room and can be interacted with (e.g., grabbed and thrown).

   - **Game Logic**:
     - Set up spawn timers and enemy behaviors (e.g., spawning enemies at intervals).
     - Customize enemy interactions and character animations to add more depth to your experience.

### Summary of Steps:

1. **Download** the base Unity project and ensure you’re using the correct Unity editor version.
2. **Switch platform** to Android and create a new scene.
3. **Set up** Mixed Reality features using Meta's Building Blocks.
4. **Enable Passthrough** to see the real world while using the headset.
5. **Enable Scene Understanding** to detect and interact with real-world objects.
6. **Customize** the effect mesh materials and their initialization order.
7. **Add hand tracking and controller input** for interactions.
8. **Add virtual objects** and set up enemy spawning logic.
9. **Test** and iterate on your game logic and Mixed Reality interactions.

This guide takes you from setting up the Unity project through to building an immersive MR experience.
