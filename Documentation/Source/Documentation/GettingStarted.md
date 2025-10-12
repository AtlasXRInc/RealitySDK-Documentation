# How to Get The Reality SDK (Beyond Sandbox Modkit)

- Download the Reality modkit installer (RealityInstaller.zip): [https://github.com/AtlasXRInc/RealitySDK-dev/releases/tag/RealityInstaller](https://github.com/AtlasXRInc/RealitySDK-dev/releases/tag/RealityInstaller)  
- Unzip it in the folder where you want to install Unreality (our fork of Unreal).  
  - It’s recommended to unzip it at the root directory (C:\RealityInstaller) to avoid issues with long file paths.
- Open PowerShell as Administrator and navigate to the extracted directory:

  ```powershell
  cd path\to\RealityInstaller
  ```

* Run the installer:

  ```powershell
  .\Install.bat
  ```
!!!warning

    This requires **at least 55 GB of free space**.

* The installer sets up:

    * Atlas XR’s **Unreality Engine** fork
    * The **Reality Modkit plugin**
    * ADB & Java (Used to build and sideload your mods to Quest)


Once installed, at the root of your installation folder, **run `Launch Unreal Editor.exe` at least once** to complete the setup.

---

## Understanding Unreality vs Reality

* **Unreality** is Atlas XR and Meta’s fork of Unreal Engine, optimized for VR.
  It’s updated rarely and is the base engine you’ll build on.
* **Reality** is the modkit.
  It’s updated frequently and contains the SDK tools you’ll use when creating mods.

---

## Setting Up Your Project

### If You Don’t Have a Modkit Unreal Project Yet

1. **Open Unreality**. It will take few minutes to compile the first time you open it.
2. In the Unreal Project Browser:

    - Select **Blank Project**
    - Blueprint project (not C++)
    - Target platform: **Mobile**
    - Quality Preset: **Scalable**

3. Click **Create** to make a new project.

!!! note

    You may see a popup regarding Shader Model 6.
    This can be safely ignored.

4. Once the project opens:

    * From the top ribbon, click **Edit → Plugins**.
    * Search for **Reality**.
    * Click the checkbox to enable it.
    * Restart the editor when prompted.

5. Replace the config files with the provided Reality config files to match rendering and collision settings.

---

### If You Already Have a Modkit Project

1. Delete the old **Reality SDK 0.1/.2** plugin.
2. Make sure you are using the correct Unreal version. Right-click your `.uproject` file → **Switch Unreal Engine version** → select the path to **Unreality**.
3. Replace the config files with the new Reality config files.

---

## Create Your First Mod

Once your project is set up:

1. In the Unreal Editor, open the **Reality** dropdown (top menu bar).
2. Select **New Mod**.

<!-- 
TODO
Add correct project settings android sdk
Add about getting Quest in dev mode

-->