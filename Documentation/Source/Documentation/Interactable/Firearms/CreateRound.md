# Creating Rounds (RealityRound)

A **RealityRound** is a child of **Reality Interactable** used to represent physical rounds in the world. Rounds can be picked up, inserted into internal magazines, or placed directly into chambers for weapons that support manual insertion.

## Basic setup
- Create a new **Blueprint** and select **RealityRound** as the parent class.
- Set the **Base Mesh**.
- Set the **Round Consumed Mesh**.
- If the round should be grabbable, set up grips on the round (see **Grips** section of this documentation).

## Double / multi-rounds (shotgun "double" rounds)
- For rounds representing two projectiles (example: double slug/rounds used in some shotguns), set **Remaining Rounds Amount** to `2` on the so the feeding/chambering logic knows it contains two charges.
- Example asset to reference: `RealityRound_12x70mm_Double`.

## Insertion / collision
- **Round Insertion Collision** is a **Box Component** on the round.
  - When this box overlaps the firearm’s corresponding **RoundInsertionCollision** component, the round will be inserted.
  - This overlap insertion is used for:
    - Reloading **internal magazines** (push rounds into the weapon’s internal store).
    - Placing rounds directly into the **chamber** for weapons that accept single-round insertion even when they have external magazines.
    - It is **not** used for placing rounds into external magazines.
- Position and size the box deliberately — alignment determines the angle/position at which rounds can be inserted.

## Events
- Use the `BP_OnRoundInsertedInInternalMagazine` event to run custom logic when the round is inserted into a firearm’s internal magazine.
    - Useful to updated visuals when a double round is seated.
    - The event is called automatically by the firearm when a round successfully inserts into the internal magazine.