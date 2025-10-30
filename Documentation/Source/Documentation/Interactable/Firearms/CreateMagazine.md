# Create Magazines

This page contains the full workflow and reference for external magazine setup, magazine Blueprints/data, the guiding spline workflow, and the Instanced Round Mechanism (ISM) used to visually represent rounds inside magazines.

---

## Weapon-side: Magazine Insertion & Guiding Spline

**Place the Magazine Insertion Collision**

- Add a **Magazine Insertion Collision** component at the magwell entrance on the firearm. This is the collision the magazine will overlap to start guiding/seating.

**Create / align the Magazine Guiding Movement Spline**

1. Temporarily add a helper **Static Mesh** magazine to the scene; parent it to the **Magazine Guiding Movement Spline** and set its local position to **(0,0,0)** — this represents the fully seated pose.
2. Move the **spline** (do not move the helper mesh) until the helper mesh appears perfectly seated in the magwell.
3. With the helper mesh still parented to the spline, drag the helper mesh outwards along the insertion path until it first contacts the firearm’s **Magazine Insertion Collision**. Record the offset from the seated pose and use that for the spline’s second point (this defines guide length).
4. Remove the helper mesh once you have the spline points set.

**Notes**

- Always move the spline to align seating; the helper mesh should remain at (0,0,0) while aligning.
- The spline’s second point (guide length) should represent the magazine’s first contact point with the magwell so the guiding movement looks natural.

---

## Magazine asset: Creating a Reality Magazine

1. Create a new **Blueprint → Reality Magazine**.
2. Create a **Reality Magazine Data Asset** and assign it in the magazine BP.
3. Set the magazine’s **Base Mesh**.
4. Add and position a **Magazine Insertion Collision** on the magazine.  
    - The firearm checks overlap between its own **Magazine Insertion Collision** and the magazine’s **Magazine Insertion Collision** to begin the guiding/seating process.
    - When overlap is detected, the magazine guiding logic takes over and moves the magazine along the guiding spline until it reaches the fully seated pose.

**Magazines are Reality Interactables**
- Magazines inherit from **Reality Interactable**, so they support the standard interactable and grip behaviors. Implement grips as needed for natural pickup and manipulation.

---

## ISM Round Mechanism System (Instanced Rounds)

The **Instanced Round Mechanism (ISM)** visually represents and manages rounds inside a magazine using instancing for performance.

**InstancedRoundGenerator**

- Each **Reality Magazine** can contain an `InstancedRoundGenerator` component (derived from Unreal’s `InstancedStaticMesh`).
- This component:
    - Places repeated round meshes inside the magazine,
    - Reduces draw calls by using instancing,
    - Lets you control spacing/alignment parameters so rounds stack correctly and visually match the magazine interior.

**Example**

- See `RealityMagazine_AK47_Example` for a working magazine setup using the ISM Round Mechanism.