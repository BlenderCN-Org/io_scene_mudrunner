# io_scene_mudrunner
This is a DirectX exporter for Blender that creates files compatible with Spintires: MudRunner.

The below documentation provides terse information about the exporter.  More extensive documentation and screenshots can be found in the 'MudRunner Exporter for Blender' section of the [Big Book of MudRunner Map Making](https://steamcommunity.com/sharedfiles/filedetails/?id=1583079240).

MudRunner's limitations on DirectX files are annoying to manually work around in Blender.  To save myself trouble, I modified Blender to export DirectX files compatible with MudRunner with no manual workarounds necessary.

This Blender addon is known to work with Blender 2.78.  It is based on the DirectX exporter that has been packaged with Blender since at least 2.69, so it should work with those versions as well.  However, it does not work with Blender 2.80.

Documentation for the original exporter is [here](https://en.blender.org/index.php/Extensions:2.6/Py/Scripts/Import-Export/DirectX_Exporter).

# To Install

Download the GitHub repository as a [ZIP file](https://github.com/fred-rum/io_scene_mudrunner/archive/master.zip).

To install the addon, run Blender and select `File -> User Preferences... (Ctrl-Alt-U)`.  Click on the "Add-ons" tab, then click "Install from File..." at the bottom.  Navigate to your downloaded `io_scene_mudrunner-master.zip` file and install it.

Once installed, the new `Import-Export: DirectX Exporter for Spintires MudRunner` addon can be found in the `Supported Level: Testing` tab on the left.  Put a checkmark in the box next to the addon to enable it, and then click "Save User Settings" at the bottom to keep it enabled for all future Blender sessions.

# To Use

With the addon, export with `File -> Export -> MudRunner (.x)`.  The export dialog looks much like the old DirectX exporter, but with some different export options.

By default, `Export Selected Objects Only` is unchecked because that's always what \*I\* want.  If your scene has extra objects that you don't want to export, you can check this box to only export the selected objects.  Note that virtual things like the camera and lights are never exported regardless of this setting.

If you use the default `Coordinate System: Left-Handed` and `Up Axis: Y`, then you don't need to rotate or mirror your model.  The exporter will handle that for you.

Different types of MudRunner objects have varying support for coordinate space transformations in the object hierarchy.  Choose the `Propagate` setting accordingly, or leave the `Propagate` setting as `auto` for the exporter to choose for you.

For a static model, overlay model, or grass, set `Propagate: All`.  All transformations are pushed into the meshes, leaving the object hierarchy as simple place holders.

For a dynamic model or plant, set `Propagate: Scale bodies, else All` to keep locations and rotations for body frames, but push all other transformations into the meshes.  Leaving locations and rotations for body frames makes constraints easier to set up.  Meanwhile, a weighted mesh requires that all transforms are propagated to the mesh level.  Plus, propagating all transforms generally works better in the presense of non-uniform scaling.

Caveat: With the left-handed coordinate system, at least one axis must be inverted from its Blender orientation.  The model displays exactly correctly, but constraints need to be set with respect to the inverted axes.  You can choose which axis is inverted with the `Invert` option.  This option only has an effect with `Propagate: Scale`.

Second caveat: if the scale is not the same in all axes, it can result in shear.  MudRunner can't handle it, and neither can `Propagate: Scale` or `Scale bodies, else All`.

The `Propagate: Auto` setting acts as `Propagate: Scale bodies, else All` when exporting a model with more than one body frame (as determined by looking for child frames that start with 'cdt', lower or upper case).  When exporting a model with fewer then two body frames, it acts as `Propagate: All`. If you have a dynamic model or plant with only a single body, and you want that body to keep its location and rotation transforms, you must select your `Propagate` option manually.

By default, the `Export Materials` box is checked to support a mesh with multiple materials.

By default, the `Export Skin Weights` box is checked to support deformable meshes for dynamic models and especially plants.  The new `Discard Armature Name` box is also checked so that the body frame can be trivially named the same as the bone to sync up their behavior.

# Keyboard Shortcut

You can set a keyboard shortcut in Blender for the MudRunner Exporter.  *Right click* `File -> Export -> MudRunner (.x)` in the menu and choose `Add Shortcut`.  I like Ctrl-Shift-E as my shortcut.  Be sure to save your User Preferences for future Blender sessions.
