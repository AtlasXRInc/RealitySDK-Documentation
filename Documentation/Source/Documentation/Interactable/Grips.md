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
2. In the details panel, you can set the preview to be the **left** or **right** hand.  
3. For each hand, assign the corresponding **blendspace**.
    - For a given grip, the left and right hands will most likely need to have different positions. Make sure for the left and right preview, the hand mesh is aligned and positioned as desired.
4. Create a **collision volume** for this grip.
    - Set the collision preset to InteractiveComponent
    - The grip will only activate when the user’s hand overlaps this volume and they pull the grip trigger on their controller.

Each `RealityGripComponent` represents **one grip**. You can add **multiple** animated grips (e.g., main grip, charging handle grip). **Register each one** with its own collision volume.

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

## Creating Custom Hand Poses (for Animated Grips)

This section walks through making a **custom hand pose animation** for `SKM_HandUE5` and setting it up with a **Blendspace**.

### 1) Duplicate a Base Hand Animation

- In `/All/EngineData/Plugins/Reality/Core/Interactable/Grip`, locate the default **A_HandUE5** animation sequence.  
- **Duplicate it** into **your mod folder**
    - (important for packaging; only assets inside your mod folder can be referenced by your mod)

### 2) Editor & Constraints While Posing

Open the duplicated hand animation and follow these constraints:

- **Do NOT move/rotate/scale**:
    - The **root**.
    - The **hand_r**.
    - Any **Metacarpal** bones.
- **Only rotate** **finger bones** to pose the hand.  
    - Avoid translating or scaling finger bones to maintain realism.

### 3) Preview Your Object in the Hand Animation

To pose the hand around your object:

1. Right click on the **Root** and hit `Add Socket` and then right click on the **socket** and hit `Add Preview Asset`
2. **Temporarily** move/rotate the **socket** and (temporarily) the **hand_r** bone so the preview object sits correctly in the hand for posing convenience.  
     - **Keyframe** (By hitting the +Key button) to capture these temporary transforms so the hand and object line up while you pose fingers.

<!-- > You’ll **remove** any keys you added for `NR`/Root later. Those transforms are only helpers for posing. -->

### 4) Pose the Fingers

- Go through all the fingers and each bone, posing it as desired.
    - Reminder: **do not** use metacarpals
- Hit **+Key** again to add a key once your pose is set so the rotations for the finger bones are saved.

### 5) Clean Up the Temporary Keys

- **Delete** the **hand_r** track.  
  Keeping transforms there will **cause issues** at runtime.
- Remove the **preview mesh**
- Delete the **temporary socket**.

Now you have a clean **hand pose animation** containing only the finger rotations.

### 6) (Optional) Bake the Pose

- Use **Create Asset → Create Animation → Current Pose** to **bake** the pose so it contains no  keys.

### 7) Create a Blendspace & Add the Pose(s)

- Create a **1D Blendspace** for `SKM_HandUE5`.
- Drag in your **pose animation**.  
    - For a **single static pose**, the position in the blendspace **doesn’t matter**.
    - For grips that need **stateful finger behavior**. Drag in the rest of the animations you want to use in the blendspace.
- You can also author **2D Blendspaces** if you need a second input dimension.

### 8) Assign the Blendspace to the Grip

- In your `RealityGripComponent`, assign the blendspace per-hand (right/left).

---

## Grip Settings (Procedural & Animated)

When calling **Register** nodes, fill the **Grip Settings / Hand Grip Info** struct:

- **Grip Name**: Required string used for later reference. Do not leave empty.
- **Can Rotate With Two Hands**:
    - **True**: If gripped with two hands, rotation is influenced by **both** hands.
    - **False**: Rotation follows the **first** hand that grabbed.
- **Grip Priority**:
    - When multiple grips are eligible, the one with **higher priority** is chosen.
    - If priorities are equal and one grip is **Animated** and the other **Procedural**, the system **prioritizes the Animated** grip.
    - If priorities are equal and types equal, the **first encountered** is chosen.
- **Allow Multiple Hand Grips**:
    - For **Procedural** grips on long props (e.g., poles), you may want **multiple hands** to grip the same procedural target.
    - For **Animated** grips like a main weapon grip, you typically **Disable** so you don’t get two right hands / left+right clipping the same slot.
- **Custom Sounds**:
    - Optional **Grip** and **Release** sounds can be assigned and will play on events.

---

## Runtime & Performance Notes

- **`RealityGripComponent`** used for **Animated** grips is **destroyed after registration**.  
  Its **data** is retained; do **not** try to reference the component at runtime.
- Procedural grips do **not** require a `RealityGripComponent` and do **not** require their own collision volume.

---

## Examples

To see how grips are set up on different firearms and interactable objects, search for **`RealityFirearm`** or **`RealityInteractable`** in the **Content Browser**.  

If no results appear, open the **Content Browser Settings** and enable **“Show Engine Content”** to make these examples visible.