# Building & Testing Your Mod

Your mod is an **Unreal Engine plugin**. Plugins can live standalone in any Unreal project and be packaged into any game.  

For now, you **cannot test your plugin in Beyond**. You must test it inside a packaged game and run it on your Quest headset.

---

## No VR Preview in Editor

**VR Preview testing inside Unreal Editor is not supported.**  
When you're ready to test your mod, you need to:

1. **Build** the mod.
2. **Install** it onto your Quest headset.
3. Launch it from your headset.

There are two main ways to do this:

- **Local Sideloading** (Build + Install directly to headset)  
- **Mod.io Upload** (Cloud-based distribution)

---

## Building & Installing (Local Sideload)

Do not use the standard Unreal packaging menu.  
Instead, always use the **Reality menu → Build / Install / Run**.

!!! warning
    You cannot install mods if you're logged into a **secondary Meta account**. Sideloading only works with the **primary (admin) account** and requires Dev Mode to be enabled.

### Steps

1. In Unreal Editor, go to the **Reality** dropdown menu (top menu bar).
2. Make sure the mod you want to build is **selected**
3. From the Reality menu, choose:

    - **Build** → Builds the mod (cooks assets + runs necessary processes)  
    - **Install** → Transfers the built mod to your headset via sideload  
    - **Run** → Not functional yet

Once installed, a **standalone game** will appear on your headset under **“Unknown Sources”**.

### Rebuilding & Multiple Mods

- To update a mod you’ve already installed, simply **Build + Install** again.
- To test another mod, **select it** and repeat Build + Install.
- You **cannot uninstall mods** from the headset manually.
- To test multiple mods at once, build and install them **one by one**.

---

## Connecting to Mod.io (In Editor)

To use Mod.io in, you need to **authenticate** your Mod.io account from the editor.

### 1. Configure Your Email

- Open **Reality → Settings**.
- In the **Mail** field, type the email you want to use with Mod.io.

### 2. Authenticate & Get OTP

- Go to **Reality → Authenticate**.  
- This will send a **One-Time Password (OTP)** to your email.

If you don't have a Mod.io account, use this OTP to **create one**. Then repeat step **2**.

### 3. Enter OTP in Settings

- Go back to **Reality → Settings**.
- Enter the received OTP into the **Mail Code** field.
- Then go back to **Reality → Authenticate** again.

Once successful:

- Restart the editor.
- The red circle next to **Authenticate** should turn **green**, indicating you're signed in.

### Troubleshooting

!!! warning
    If you see the following error, it means the OTP was already used. 
    ```
    Authentication error: The email security code has already been redeemed.
    ```
    To fix it:

    - Clear the **Mail Code** field in Reality → Settings.
    - Click **Reality → Authenticate** again to get a new OTP emailed to you.

    
---

## Publishing Mods to Mod.io (Cloud Distribution)

Once you have a standalone game on your headset that was packaged from Reality, you can also distribute and test updates of your mod through **Mod.io**.  

Unlike local sideloading, Mod.io:

- Works with **secondary Meta accounts**
- Does **not** require Dev Mode
- Distributes mods through the cloud

This is especially useful for:

- Testing in **multiplayer**
- Sharing mods between creators

---

### Uploading Your Mod to Mod.io

1. Select your mod in the Unreal Editor.  
2. From the mod’s dropdown menu, choose **Publish/Update**.  
   This uploads your mod to Mod.io.

!!! note
    For now, **multiplayer testing** requires publishing your mod to Mod.io.

!!! warning
    When updating an existing mod on Mod.io, go to the Reality dropdown, hit **Edit Mod**, and increase the **Version Number** string manually. There also must be at least one new change to your source files (blueprints) for the update to work. Then hit the **Publish/Update** button.

---

### Sharing Mods Between Creators

If you want to test your mod with **someone else’s mod** (e.g., their weapon + your shield), there are two ways:

1. They can **share their content with everyone**:
    - Inside their plugin’s content folder (the root folder), create a folder called `Shared`.
    - Place the mod files there for others to access.
    - All files placed in the `Shared` folder will be pushed under a -dev version to Mod.io so modders can get source files of a GameMode for example

2. They can **send you their mod files directly**, and you place them into your project.

!!! warning
    If you delete the manifest file in **Reality > Mods > YourMod** you will not be able to update your mod again.