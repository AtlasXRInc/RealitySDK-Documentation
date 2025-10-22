# Create Firearms

A **Reality Firearm** is a specialized **child class** of [Reality Interactable](./reality-interactable.md) designed for VR weapons.  
It includes built-in grabbing, aiming, firing, and physics. The `RealityFirearm` class lets you build ~90% of weapons out of the box and is modular enough for the remaining 10%.

---

## Creating a Reality Firearm Actor (from scratch)

1. **Right-click** in the **Content Browser** → **Create Blueprint Class**.  
2. Search for **RealityFirearm** and choose it as the **parent class**.  
3. Open the Blueprint and customize components, visuals, and behavior.

> You’ll configure behavior via three systems in the Data Asset: **Feeding**, **Chambering**, and **Firing**.

---

## Faster Start: Duplicate an Example (recommended)

1. Enable **Show Engine Content** (Content Browser → **Settings**).  
2. Browse the Reality Content plugin library (e.g., `Library/Interactable/Firearm`).  
3. Duplicate an example firearm (e.g., **AK-47**) and its **Data Asset**.  
4. Rename (e.g., `BP_Firearm_M16`, `DA_Firearm_M16`).  
5. Move both into your mod’s **folder** (Plugins → your mod).
6. In the **class defaults** of the new firearm, search for **Data** and assign your new data asset there.

!!! warning
    Assets **outside** your mod’s `ModName Content` folder will **not be packaged**.

---

## Grip Auto-Registration

On **Begin Play**, `RealityFirearm` registers:

- **Charging Handle Grip** → **Animated Grip**  
- **Main Grip** → **Animated Grip**  
- **Main Mesh** → **Procedural Grip**

!!! note
    To disable an inherited animated grip, set its collision volume bounds to **zero** (e.g., the charging handle on the Sawed-Off Double Barrel).

---

## Viewing Example Firearms

Find example Blueprints such as:

- `RealityFirearm_AK47_Example`  
- `RealityFirearmDoubleBarrelSawedOff_Example`  
- `RealityFirearm_Revolver_Magnum_Example`

These are excellent references for setup and modularity. They also show broader variations—e.g., the **Revolver** class extends the firearm system with a **physics-based spinning cylinder**.

---

## Assemble Your Firearm (component pass)

After duplicating an example, swap meshes and place helpers:

- **Base Mesh** → your weapon body.
- **Main Grip & Collision** → align to the pistol grip.  
- **Charging Handle Mesh** → set mesh, position as needed.
- **Charging Handle Grip & Collision** → place grip and collision where hands should grab.  
- **Bolt Mesh** → set and position mesh (supports **decoupled** bolt).  
    - **Chamber Round Mesh** → at bolt top (shows chambered round).  
- **Distance Grip Indicator** → typical at the pistol grip.  
- **Firing Location** → set position at muzzle.  
- **Firing Mode Selector Mesh** → set mesh and position.  
- **Round Ejection Transform** → position at ejection port.  
- **Chamber Smoke Transform** → position at chamber/ejection area.  
- **Trigger Mesh** → set and align.  
- **Recoil Target** → where recoil force gets applied to the weapon, usually placed slightly above the weapon (tune by testing).  
- **Action Release Button (Bolt Catch)** → closes the bolt when the collision is hit.
    - **Mesh** position at desired location
    - **Button Collision** set size and location.
- **Round Insertion Collision** → For applicable weapons, the location where rounds are manually inserted into the chamber or internal magazine

Remove irrelevant example components (e.g., AK-specific bits) to keep things clean.

!!! tip
    When aligning **Grips**, set the root location correctly for both the left and right hands. Ensure proper positioning by setting the correct blend space asset.

---

## Magazine & Guiding Spline

**Weapon side**

- Place **Magazine Insertion Collision** at the magwell entrance.  
- Create/align the **Magazine Guiding Movement Spline**:
    1. Temporarily add a helper **Static Mesh** magazine with position set to **(0,0,0)** parented to the **Magazine Guiding Movement Spline** (represents fully seated pose).  
    2. Move the **spline** (not the magazine) until seating is correct.  
    3. Drag the helper magazine static mesh out along the insertion path to find first collision contact with the  **Magazine Insertion Collision**; use that offset for the second spline point of the **Magazine Guiding Movement Spline** (guide length).  
    4. Remove the helper mesh.

**Magazine asset**

1. Create **Blueprint → Reality Magazine**
2. Create **Reality Magazine Data Asset** and assign it in the BP.  
3. Set **Base Mesh**
4. Place **Magazine Insertion Collision** appropriately. Overlap collision will be checked between this and the corresponding **Magazine Insertion Collision** component in the firearm.
    - When they overlap, this begins the magazine guiding process

> Magazines inherit from **Reality Interactable**, so they support standard interactable behavior.

---

## Link the Firearm to Its Data Asset

In the firearm BP → **Class Defaults → Type Data**, assign your firearm **Data Asset** (e.g., `DA_Firearm_M16`).  
All tuning happens here, grouped into **Feeding**, **Chambering**, **Firing**.

---

## Firearm Input (Data Asset)

- **Input mapping**  
    - **Action 1 (Trigger)** → Typically set to Fire
    - **Action 2 (A/X depending on controller)** → Typically set to Release Magazine  
    - **Action 3 (B/Circle depending on controller)** → Custom (e.g., **Change Firing Mode**, or **Action Release** on some pistols)

---

## Firing System (Data Asset)

This system handles trigger behavior, fire rate, recoil, and visual/audio effects.

- **Fire Rate** (seconds between shots)  
- **Damage**  
- **Trigger Max Rotation** (measure on your trigger mesh; enter positive degrees)

**Audio**

- **Firing Sound**
- Optional:
    - **Firing Distance Sound** → Custom sound for people hearing the firing from far away
    - **Firing Loop Sound** → Specific loop sound for automatic weapons (falls back to **Firing Sound** if none is set) 
    - **Firing Loop Distance Sound**
    - **Firing Stop Tail Sound** with **Start Delay** → Additional specific sound to play when the last shot is fired
    - **Firing Dry Sound** (no rounds)
    - **Firing Dry Cocked Sound**
    - **Firing Safe Sound** → Firing sound if the weapon is on safe

**VFX**

- **Firing Muzzle Flash** (default)
    - Can set overrides for burst or automatic firing
- **Chamber Smoke on Fire** (spawns at **Chamber Smoke Transform** component's location on the firearm)

**Recoil**

- **Force Vertical**
- **Force Vertical Two Hands Multiplier**
- **Recoil Force Back**
- **Recoil Force Back Two Hands Multiplier**

**Firing Modes**

- Add modes (e.g., **Automatic**, **Semi-Automatic**, **Safe**).  
    - **Array order sets default mode** (first = active on start).  
- **Burst Fire Shot Amount** (if using Burst).  
- Selector
    - **Selector Animations** (thumb animation montages)
    - **Logic Delays** (sync to thumb contact).  
    - **Selector Rotations** → set per mode to match your selector component.
- **SFX**

---

## Chambering System (Data Asset)

This system manages the bolt, charging handle, and round ejection behavior.

> Disabling features removes related components at runtime to save performance

**Charging Handle**

- **Enabled** (if present)
- **Max Pull Distance**
- **Distance to Chamber New Round**
- **Can Release Charging Handle by Partial Pull Motion** (primarily for pistols)
    - When true, allows the player to release the slide/charging-handle by performing a partial rearward pull and releasing (a short “nudge” or slingshot) to let the bolt/slide snap forward
    - When false, the player must either fully rack the charging handle or press the slide release/bolt catch.
- **Slides Back on Fire** → Enable if shooting moves the charging handle
- **Hold Charging Handle Retracted on Last Round Fired**

**Decoupled Bolt**

- **Bolt Slide-Back Distance on Fire** → set rearward travel when firing.

**Turn Bolt** (bolt-action primarily for snipers)

- **Turn Bolt Max Angle** before pull.

**Action Release Button (Bolt Catch)**

- **Has Action Release Button**
- **Can Hit Action Release Button**
- Optional **Delta Location/Rotation after Lock-Back** → After the last round when the charging handle is open, used for if you want to change the button location/rotation
- Optional **Thumb Animation** → If the button is reachable from the pistol grip hand, can play an animation to hit the button
- **SFX**
- **Press Logic Delay** → If you don't want logic to continue executing before the thumb animation is finished

**Round Ejection**

- **Eject From Chamber on Firing** → enabled/disabled

    - Uses the **Round Ejection Transform** component's location in the firearm
    
- **Ejection/collision SFX**
- **VFX** (Niagara particle system representing a full/consumed).

---

## Feeding System (Data Asset)

This system controls how ammunition enters the weapon (magazines, internal stores, manual loading).

- **Has External Magazine** → enable for detachable mags.  
- **Compatible Magazine Classes** → add your magazine class (children of a base class are supported).  
- **Force Hand Release on Magazine Clipping** → optional auto-release on seat.  
- **SFX** → optional clip/release sounds.
- **Internal Magazine** (primarily for shotguns/snipers)
    - set enabled/disabled
    - set magazine capacity
- **Manual Round Insertion**
    - set enabled/disabled
    - set **Compatible Round Class**
    - set SFX

---

## Gameplay (Data Asset)

- **Abilities** → ensure the firearm has **Firearm Fire Ability** (required; GAS/multiplayer).  


---

## Scaling Interactables

!!! warning
    Do **not** scale the **Root Component**. Scaling the root causes physics issues.

Use UE tools instead:

- Re-model/re-import at the correct scale, or  
- Adjust **Import Scale** in the **Static Mesh Editor**.

<!--
# Create Firearms
A **Reality Firearm** is a specialized **child class** of [Reality Interactable](./reality-interactable.md) designed specifically for creating firearms in your mods.  
This class includes all the necessary functionality for handling VR weapon interactions, such as grabbing, aiming, firing, and physical collision.  
The `RealityFirearm` class is designed to easily let you make 90% of existing weapons out of the box and is modular enough to set up the remaining 10%.

---

## Creating a Reality Firearm Actor

1. **Right-click** in the **Content Browser**.  
2. Select **Create Blueprint Class**.  
3. Search for **Reality Firearm**.  
4. Choose it as the **parent class** for your new blueprint.

Once created, you can customize the firearm’s appearance, behavior, and mechanics by modifying the blueprint.

<!-- TODO Explain the firing system, chambering system and feeding system + API  -->
<!--
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
- `RealityFirearm_Revolver_Magnum_Example`

These examples are excellent references for understanding weapon setup, components, and functionality. They also demonstrate how the modular system can be used to create specialized mechanisms or broader variations, such as the **Revolver** class, which extends the firearm system to include a physics based spinning cylinder.

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
-->