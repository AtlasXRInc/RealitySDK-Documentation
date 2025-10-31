# Preparing Meshes for Reality Firearm and Reality Interactable

This guide explains how to correctly prepare meshes for use with the **Reality Interactable** and **Reality Firearm** systems.  
It covers proper **scaling**, **orientation**, **pivot point setup**, and **collision** — all of which are essential for correct behavior in VR.

---

## Accessing Reference Assets

To help verify scale and proportions, a **hand reference** is available in the ModKit:

1. Open the **Content Browser**.
2. Enable **Show Engine Content** (top right settings).
3. Navigate to:  
   `Engine → Plugins → Reality → RealityContent → Core → Interactable → Grip`
4. In this folder, you’ll find various reference and example assets.

The **Reality Interactable Firearm** examples include:

- `AK-47`
- `LR-300`
- `M41B`
- `Round`

These examples demonstrate proper setup and can be used as reference when adjusting your own weapons.

---

## Scaling Your Weapon

When preparing your weapon mesh, first ensure it matches the correct **VR scale** using the hand reference.

### Steps

1. **Parent all components** (i.e. magazine, trigger, charging handle) to the base mesh (main part of the weapon).  
   This ensures that when you scale, all parts maintain their relative positions.
2. Select the **parent mesh** and adjust the scale in the details panel.
3. **Unparent** all child meshes so each one has the new scale applied.
4. Select all meshes and open the **Modeling Tools** panel.

### Baking the Transform

1. Go to **XForm → Bake Transform**.
2. Check **Apply to All LODs** and **Bake Rotation**.
3. Click **Accept**.

This sets the new scale and rotation as default (`Scale = 1.0, Rotation = 0°`).

---

## Orientation Setup

For the Reality Firearm system to function properly, weapons must face the **+X-axis**.

### Example

If your model currently faces the **Y-axis**:

1. **Parent all components** (i.e. magazine, trigger, charging handle) to the base mesh (main part of the weapon).
2. Rotate your weapon **90°** so it aligns with the X-axis.
3. Adjust small pitch angles if needed so the barrel is level with the floor.
4. Once aligned, **unparent** the components.
5. Select them all again and **Bake Transform** (rotation and scale).

Now the default rotation should be correct for all parts (0, 0, 0).

---

## Setting Pivot Points

Each mesh acts as a **physics object**, so correct pivot placement is important.

### Centered Pivots

For most meshes (weapon body, magazine, charging handle):

1. Open the **Modeling Tools** and go to the **XForm** tab.
2. Select **Edit Pivot** → **Center**.
3. Click **Accept** to bake the pivot.

### Rotating Parts (Exceptions)

Some components, such as **triggers** or **levers**, need their pivots placed at their rotation point.

1. Use **Edit Pivot** and move the pivot to where the rotation should occur (usually near the hinge).
2. Fine-tune manually in the viewport.
3. Click **Accept** to bake the new pivot.
4. Test the rotation to ensure it behaves naturally.

---

## Adding Simple Collision

Unreal Engine 5 requires meshes with **simple collision** for physics interactions.  
Complex collisions are **not supported** by Reality systems.

### Checking Collision

1. Double-click the mesh to open the **Static Mesh Editor**.
2. Go to **Show → Simple Collision**.  
    - If nothing appears, the mesh doesn’t have simple collision.

### Generating Collision

1. Open **Window → Convex Decomposition**.
2. Adjust the parameters:
    - Higher values = more detailed (but slower to compute).
3. Click **Generate** to create a collision mesh.

You can move, resize, or delete generated collision pieces to refine accuracy.

!!! warning
    For firearms, keep the magazine socket area clear so the magazine can be inserted properly.

### Creating Custom Collision Shapes

You can manually add:

- **Box**
- **Capsule**
- **Sphere**

Then position and scale them to match the mesh.

---

## Important Notes on Collision

- Do **not** enable **“Use Complex Collision as Simple.”**
- Keep **Collision Complexity** set to **Project Default.**
- If you need highly accurate collisions, create them in a 3D modeling tool and reimport.