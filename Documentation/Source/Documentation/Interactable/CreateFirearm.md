# Create Firearms
A **Reality Firearm** is a specialized **child class** of [Reality Interactable](./reality-interactable.md) designed specifically for creating firearms in your mods.  
This class includes all the necessary functionality for handling VR weapon interactions, such as grabbing, aiming, firing, and physical collision.

---

## Creating a Reality Firearm Actor

1. **Right-click** in the **Content Browser**.  
2. Select **Create Blueprint Class**.  
3. Search for **Reality Firearm**.  
4. Choose it as the **parent class** for your new blueprint.

Once created, you can customize the firearm’s appearance, behavior, and mechanics by modifying the blueprint.

<!-- TODO Explain the firing system, chambering system and feeding system + API  -->

---
## Grip Auto-Registration

The `RealityFirearm` class comes with some grips **automatically registered** on Begin Play:

- **Charging Handle Grip** → Registered as an **Animated Grip**  

- **Main Grip** → Registered as an **Animated Grip**

- **Main Mesh** → Registered as a **Procedural Grip**
!!! note
    Disabling an animated grip inherited from a parent class can be done by setting the bounds of the associated collision volume to zero. For example, this is done for the charging handle in the sawed off double barrel shotgun.

---

## Viewing Example Firearms

To explore example Reality Firearm blueprints:

1. Open the **Content Browser**.  
2. Click **Settings** (top right).  
3. Enable **Show Engine Content**.  
4. In the **Engine directory**, search for `RealityFirearm`.

You’ll find example blueprints such as:

- `RealityFirearm_AK47_Example`  
- `RealityFirearmDoubleBarrelSawedOff_Example`

These are great references to understand weapon setup, components, and functionality.

---

## Placement in Mod Folder

When you create a mod, a folder named **`ModName Content`** is automatically generated in the **Plugins** folder.

> Make sure your **Reality Firearm** (and all dependencies i.e meshes, textures, animations) are saved inside this folder, or it will **not be packaged** with your mod.

---

## Scaling Interactables
!!! warning
    Do not scale the Root Component directly. Changing the root component’s scale causes physics issues. (The **Root Component** is the top component in the Components hierarchy when a Blueprint is open)

Instead, use the UE5 Editor tools to adjust the size of your mesh:

- **Remodel** or **reimport** the mesh at the correct scale.  
- Alternatively, use the **Static Mesh Editor** to adjust its import scale.