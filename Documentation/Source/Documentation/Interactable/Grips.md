# Gripping System

There are **two types of grips** available in the Reality Modkit:

- **Procedural Grips** – quick to set up, automatically adapt to any shape, but offer limited fine-tuning.  
- **Animated Grips** – allow for precise, hand-animated interactions such as weapon grips, triggers, or special poses.

---

## Procedural Grips

**Procedural grips** adapt dynamically to the shape of the object using its collision. They’re ideal for general props or objects where precise finger placement isn’t required.

- Very easy to set up  
- Works on any shape  
- No fine-tuning or animation control

All you need to do is define a **collision volume** that determines where gripping becomes active.

> **Note:** Even without procedural gripping set up, the physics system may still let you “pick up” items in a loose way (e.g. wrapping fingers around a gun grip). However, to have the item properly attached to the hand, you must enable procedural gripping. Internally, this uses `AttachComponentToComponent`.

### Registering a Procedural Grip

You do **not** need to add a `RealityGripComponent` or set up any special collision volume to register a procedural grip.

On Begin Play, call:

- `RegisterGripProcedural`  
    - Pass in the **mesh** you want to grip.  
    - Pass in a **struct of grip settings**.

---

## Animated Grips

**Animated grips** are used for precise hand interactions — for example, a pistol grip where the **trigger finger** moves independently when firing.

They rely on playing animations on a **special skeletal mesh hand**, allowing exact control over finger poses and transitions through blendspaces.

### Requirements

- You must use the provided skeletal mesh: **`SKM_HandUE5`**  
  (This is already the default value for the hand field.)
- You need to create an **animation** for the hand.
- You need to create a **blendspace** that includes the relevant hand animations.  
    - This allows smooth finger transitions (e.g. pressing the trigger).

### Setting Up an Animated Grip

1. **Add a `RealityGripComponent`** to your object.  
2. Choose whether it’s for the **left** or **right** hand.  
3. For each hand, assign the corresponding **blendspace**.  
    - Note: Only the blendspace for the selected hand is actually used.  
4. Create a **collision volume** for this grip.  
    - The grip will only activate when the user’s hand overlaps this volume and they pull the grip trigger on their controller.

Each `RealityGripComponent` represents **one grip**.

### Registering an Animated Grip

To register an animated grip, on Begin Play call:

- `RegisterGripAnimation`  
  - Pass in the **RealityGripComponent**  
  - Pass in the **collision volume** (used only to detect overlap and activate the grip)  
  - Pass in a **struct of grip settings**

### Animated Grip Behavior

- When gripping, the **root bone of the hand snaps** to the defined grip location.  
- All finger and hand positioning is driven by the **blendspace**, not physics.
- When the controller releases the grip, the **animated grip deactivates**.

---

## Examples

To see how grips are set up on different firearms and interactable objects, search for **`RealityFirearm`** or **`RealityInteractable`** in the **Content Browser**.  

If no results appear, open the **Content Browser Settings** and enable **“Show Engine Content”** to make these examples visible.