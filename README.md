# io_scene_mudrunner
This is a DirectX exporter for Blender that creates files compatible with Spintires: MudRunner.

MudRunner's limitations on DirectX files are annoying to manually work around in Blender.  To save myself trouble, I modified Blender to export DirectX files compatible with MudRunner with no manual workarounds necessary.

Big caveat: this exporter has only been tested with static models and grasses.  I.e. it has not been tested with any models with armatures.  It definitely won't work any better, and it may work worse for those models.

This Blender addon is known to work with Blender 2.78.  It is based on the DirectX exporter that has been packaged with Blender since at least 2.69, so it should work with those versions as well.  However, there's a good chance that it won't work with Blender 2.80.

## To Install

Download the [io_scene_mudrunner.zip file](io_scene_mudrunner.zip).  Your browser might complain about potential malware simply because it's a ZIP file from GitHub.  If you want to check for yourself, you can extract the ZIP contents and diff them against the original DirectX exporter script.  The original script should be in a directory something like `C:\Program Files\Blender Foundation\Blender\2.78\scripts\addons\io_scene_x`.

To install the addon, run Blender and select `File -> User Preferences... (Ctrl-Alt-U)`.  Click on the "Add-ons" tab, then click "Install from File..." at the bottom.  Navigate to your downloaded `io_scene_mudrunner.zip` file and install it.  The preferences window shows the new `Import-Export: DirectX X Format for Spintires MudRunner` addon.  Put a checkmark in the box next to it to enable it, and then click "Save User Settings" at the bottom.

You can now export with `File -> Export -> MudRunner (.x)`.  The export dialog looks much like the old DirectX exporter, but with a new checkbox for `Flatten Transforms to Meshes`.  Check this box to enjoy hassle-free exporting.
