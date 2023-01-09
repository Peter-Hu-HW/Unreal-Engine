# General Procedure
https://docs.unrealengine.com/5.0/en-US/using-the-android-vulkan-mobile-renderer-in-unreal-engine/ \
Go to “Edit → Project settings → Platforms → Windows → Default RHI” and select DirectX 11 or Vulkan 

# Detailed Instructions
() - means optional
## Building for Vulkan
1. Once the project has loaded, go to Edit > Project Settings, then under Engine, go to the Rendering section (and make sure that Mobile HDR has been enabled.)

2. Below the APKPackaging section in the Build section, make sure that the following options are enabled:
(Support OpenGL ES3.1)
Support Vulkan

3. From the menu bar, go to File > Package Project > Android, and select the Android(ASTC) option.

4. Go to “Edit → Project settings → Platforms → Windows → Default RHI” and select DirectX 11 or Vulkan 

## Enabling Vulkan Preview Rendering in Editor
If you have enabled Vulkan in your project as described above, a preview rendering option will appear automatically. \
1. On the Main Toolbar, click on the Settings button and go to the Preview Rendering Level option. Select the Android Vulkan option to enable the Vulkan preview in the UE4 Viewport.

2. To enable Vulkan Render with the Mobile Preview Render: From the Main Toolbar, go to the Edit option and then select the Editor Preferences option from the main menu.

3. In the General section under the Experimental category, expand the PIE section then select the checkmark box next to the Allow Vulkan Mobile Preview option.

4. On the Main Toolbar, change the Play Mode from Play this level in the selected viewport to the Vulkan Mobile Preview (PIE) option by clicking on the small white triangle next to the play button, selecting Vulkan Mobile Preview (PIE) from the drop down list.

(5. Click on the Play button that is on the Main Toolbar to launch your UE4 project in a new preview window with Vulkan Render enabled. If everything has been setup successfully, you should see something similar to the image below.)

## Debugging with Mobile Vulkan Preview
Add breakpoint in source file (e.g. \Engine\Source\Runtime\Renderer\Private\MobileShadingRenderer.cpp) before launching the VS solution.