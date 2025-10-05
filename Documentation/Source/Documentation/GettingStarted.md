# How to Get Reality SDK 0.3

- Download the modkit installer (RealityStandalone.zip): [https://github.com/AtlasXRInc/RealitySDK-dev/releases/tag/RealityStandalone](https://github.com/AtlasXRInc/RealitySDK-dev/releases/tag/RealityStandalone)  
- Unzip it in the folder where you want to install Unreality (our fork of Unreal).  
  - It’s recommended to unzip it at the root directory (C:\RealityStandalone) to avoid issues with long file paths.
- Open PowerShell as Administrator and navigate to the extracted directory:

  ```powershell
  cd path\to\RealityStandalone
  ```

* Run the installer:

  ```powershell
  .\Install.bat
  ```
!!!warning

    This requires **at least 52 GB of free space**.

* The installer sets up:

    * Meta’s **Unreality Engine** fork
    * The **Reality plugin**
    * ADB
    * Java


Once installed, **run `Unreality.exe` at least once** to complete the setup.

---

## Understanding Unreality vs Reality

* **Unreality** is Meta’s fork of Unreal Engine, optimized for VR.
  It’s updated rarely and is the base engine you’ll build on.
* **Reality** is a plugin on top of Unreality.
  It’s updated frequently and contains the SDK tools you’ll use when creating mods.

---

## Setting Up Your Project

### If You Don’t Have a Modkit Unreal Project Yet

1. **Open Unreality**.
2. In the Unreal Project Browser:

    - Select **Blank Project**
    - Blueprint project
    - Scalable quality
    - Target platform: **Mobile**

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
2. Right-click your `.uproject` file → **Switch Unreal Engine version** → select the path to **Unreality**.
3. Replace the config files with the new Reality config files.

---

## Create Your First Mod

Once your project is set up:

1. In the Unreal Editor, open the **Reality** dropdown (top menu bar).
2. Select **New Mod**.