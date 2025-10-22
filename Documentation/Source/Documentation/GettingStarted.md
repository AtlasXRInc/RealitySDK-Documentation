# Installing RealitySDK and Unreality Engine


* Download RealitySDK.zip from the [Unreality Releases page](https://github.com/AtlasXRInc/Unreality/releases)
    * Move the RealitySDK.zip file to the root of your drive (e.g., C:\). ⚠️ This prevents long file path issues with Unreal Engine.
    * Right-click the file and select Extract All...


![ExtractRealitySDK](../Data/Screenshot/ExtractRealitySDK.png)
This will be your root folder for the Unreality Engine


* Now download the Unreality Engine (all six Engine.zip.00X files from the same GitHub releases page).
    * Place all six .00X files inside the extracted RealitySDK folder. (⚠️ See picture)
    * Double-click RealitySetup.

![ExtractUnrealityEngine](../Data/Screenshot/ExtractUnrealityEngine.png)


This process will extract the Unreality Engine and install the RealitySDK along with all required dependencies.

Once the installation is complete, Unreal Engine will prompt a confirmation window — click Allow to proceed. The engine will then launch automatically.

!!!warning
    This requires **at least 55 GB of free space**.

---

## Understanding Unreality vs Reality

* **Unreality Engine** is Atlas XR and Meta’s fork of Unreal Engine, optimized for VR.
  It’s updated rarely and is the base engine you’ll build on.
* **RealitySDK** is the modkit.
  It’s updated frequently and contains the SDK tools you’ll use when creating mods.

---

## Setting Up Your Project

### If You Don’t Have a Modkit Unreal Project Yet

1. **Open Unreality**. It will take few minutes to compile the first time you open it.
2. In the Unreal Project Browser:

    - Select **Blank Project**
    - Blueprint project (not C++)

3. Click **Create** to make a new project.

4. Once the project opens:

    * From the top ribbon, click **Edit → Plugins**.
    * Search for **Reality**.
    * If it's disabled, click the checkbox to enable it.
    * Restart the editor when prompted.

---

### If You Already Have a Modkit Project
Make sure you are using the correct Unreal version. Right-click your `.uproject` file → **Switch Unreal Engine version** → select the path to **Unreality**.

---

## Create Your First Mod

Once your project is set up:

1. In the Unreal Editor, open the **Reality** dropdown (top menu bar).
2. Select **New Mod**.

<!-- 
TODO Later
Add correct project settings android sdk
Add about getting Quest in dev mode

-->