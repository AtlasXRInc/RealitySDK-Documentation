## Creating a Reality Interactable Actor

1. **Right-click** in the **Content Browser**.  
2. Select **Create Blueprint Class**.  
3. Search for **Reality Interactable**.  
4. Choose it as the **parent class** for your new blueprint.
5. Create and link the appropriate **data asset** in the details panel of your actor
    - Each Reality Interactable actor **needs** a data asset or you will get errors
    - Generic RealityInteractable actors should use the RealityInteractableData asset
    - Otherwise, use the Data Asset corresponding to the **correct child class** (i.e RealityRoundData for RealityRound, RealityMagazineData for RealityMagazine)
        - You can look at examples `/All/EngineData/Plugins/Reality/Library/Interactable` to see how data assets are used correctly

!!! tip
    Use Reality Interactable for anything that requires **physics-based interaction**.

### Examples of What Should *Not* Be Interactable

- Decorative props that don’t need physics interaction  
- Non-physical gameplay elements (e.g., trigger volumes, UI components)

---

## Converting an Existing Actor to a Reality Interactable

If you already have an actor and want to make it interactable:

1. Open the existing actor’s **Blueprint**.  
2. In the **top ribbon**, click **Class Settings**.  
3. In the **Details Panel**, set the **Parent Class** to `Reality Interactable`.

---

## Viewing Example Interactables

To explore example Reality Interactable blueprints:

1. Open the **Content Browser**.  
2. Click **Settings** (top right).  
3. Enable **Show Engine Content**.  
4. In the **Engine directory**, search for `RealityInteractable`.

You’ll find blueprints such as:

- `RealityInteractable_DoorHandle`  
- `RealityInteractable_Machete`

These can be great references for setup and best practices.

---

## Placement in Mod Folder

When you create a mod, a folder named **`ModName Content`** is automatically generated in the **Plugins** folder.

> Make sure your **Reality Interactable actor** (and all dependencies i.e meshes, textures, animations) are saved inside this folder, or it will **not be packaged** with your mod.

---

## Scaling Interactables
!!! warning
    Do not scale the Root Component directly. Changing the root component’s scale causes physics issues. (The **Root Component** is the top component in the Components hierarchy when a Blueprint is open)

Instead, use the UE5 Editor tools to adjust the size of your mesh:

- **Remodel** or **reimport** the mesh at the correct scale.  
- Alternatively, use the **Static Mesh Editor** to adjust its import scale.