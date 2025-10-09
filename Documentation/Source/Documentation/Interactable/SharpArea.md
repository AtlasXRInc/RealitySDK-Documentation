# Sharp Area Component

The **Sharp Area Component** is a box collider component that enables **stabbing** and **slashing** interactions in your project.  
It can be used to create functional **spikes**, **traps**, **bayonets**, or **bladed weapons**.

You can choose to enable **stabbing**, **slashing**, or both — depending on the behavior you want.

---

## Adding a Sharp Area Component to a Blueprint

1. In the **Components** tab of your Blueprint, click **Add**.  
2. Search for **Reality Sharp Area** and select it.  
3. Position the component and **align its scale and rotation** with the sharp area on the Blueprint you are working with.

> **Tip:**  
> Sometimes you may need more than one Sharp Area Component to accurately simulate your weapon.  
> For example, a katana may use one Sharp Area for the **tip** (stabbing) and another for the **blade** (slashing).

You can align the **stab axis** and **slash axis** either by:

- Changing the corresponding variable in the dropdown, or
- Rotating the entire component in the editor.

!!! note
    
    For complex weapons like a rake, **adding a Sharp Area Component to every spike is not recommended**, as this may negatively impact performance.

---

## Variable Reference

The following tables list all available variables for the **Sharp Area Component**, separated into *Stabbing* and *Slashing* settings.

### Stabbing

| Variable | Description |
|----------|-------------|
| **Can Stab** | Enables stabbing behavior for this sharp area. |
| **Stab Axis** | Axis aligned with the normal direction of the tip. |
| **Position Strength** | TODO |
| **Velocity Strength** | TODO |
| **Minimum Penetration** | Minimum distance required to count as a valid stab. |
| **Maximum Penetration** | Maximum distance the blade can penetrate. |
| **Stab Force Threshold** | Offset applied to the base stab force threshold. Negative requires less force to stab; positive requires more. |
| **Can Be Pushed Deeper** | Toggle on to allow the blade to be pushed deeper into the wound. When Can Be Pushed Deeper is disabled, the stab depth is calculated on the first collision frame and remains fixed at that depth. When enabled, the blade can continue to be pushed deeper into the target up to the Maximum Penetration distance after the initial stab.|
| **Can Twist** | Enables twisting of the blade after penetration. |
| **Twist Limit** | How far twisting is allowed (in degrees or custom units). |
| **Can Swing** | Whether the blade can swing from this area. |
| **Swing Limit** | How far the blade can swing (in degrees or custom units). |

### Slashing

| Variable | Description |
|----------|-------------|
| **Can Slash** | Enables slashing behavior for this sharp area. |
| **Slash Force Threshold** | Offset applied to the base slash force threshold. Negative requires less force to slash; positive requires more. |
| **Slash Axis** | Axis that runs along the blade for slashing direction. |

---

## Positioning Notes

- It's **okay for Sharp Area Components to overlap slightly**. Overlaps will not cause any issues in detection or interaction.
- Make sure each Sharp Area’s scale and axis orientation match the physical shape and intended interaction area of the weapon.

---

## Example: Machete Setup

To see a working example of a Sharp Area Component:

1. Open your **Content Browser**.
2. In the top right, click **Settings** → enable **Show Engine Content**.
3. In the **Engine** directory, search for `RealityFirearm`.
4. Open the Blueprint called **`RealityInteractable_Machete`**.

This Blueprint demonstrates how Sharp Area Components are positioned and configured for both **stabbing** and **slashing** on a single weapon.