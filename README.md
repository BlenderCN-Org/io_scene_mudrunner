# io_scene_mudrunner
This is a DirectX exporter for Blender that creates files compatible with Spintires: MudRunner.

MudRunner's limitations on DirectX files are annoying to manually work around in Blender.  To save myself trouble, I modified Blender to export DirectX files compatible with MudRunner with no manual workarounds necessary.

Big caveat: this exporter has only been tested with grasses, static models, and a few dynamic models with simple armatures.  It has not been tested with any models or trucks that require bones to be exported.  It definitely won't work any better, and it may work worse for those models.

This Blender addon is known to work with Blender 2.78.  It is based on the DirectX exporter that has been packaged with Blender since at least 2.69, so it should work with those versions as well.  However, there's a good chance that it won't work with Blender 2.80.

Documentation for the original exporter is [here](https://en.blender.org/index.php/Extensions:2.6/Py/Scripts/Import-Export/DirectX_Exporter).

# To Install

Download the GitHub repository as a [ZIP file](https://github.com/fred-rum/io_scene_mudrunner/archive/master.zip).

To install the addon, run Blender and select `File -> User Preferences... (Ctrl-Alt-U)`.  Click on the "Add-ons" tab, then click "Install from File..." at the bottom.  Navigate to your downloaded `io_scene_mudrunner-master.zip` file and install it.

Once installed, the new `Import-Export: DirectX X Format for Spintires MudRunner` addon can be found in the `Supported Level: Testing` tab on the left.  Put a checkmark in the box next to the addon to enable it, and then click "Save User Settings" at the bottom to keep it enabled for all future Blender sessions.

# To Use

With the addon, export with `File -> Export -> MudRunner (.x)`.  The export dialog looks much like the old DirectX exporter, but with some different export options.

By default, `Export Selected Objects Only` is unchecked because that's always what \*I\* want.  If your scene has extra objects that you don't want to export, you can check this box to only export the selected objects.  Note that virtual things like the camera and lights are never exported regardless of this setting.

If you set `Coordinate System: Left-Handed` and `Up Axis: Y`, then you don't need to rotate or mirror your model.  The exporter will handle that for you.

MudRunner can handle different amounts of information in the object hierarchy depending on what kind of thing you're exporting.  Choose the `Propagate` setting accordingly.

For a grass, set `Propagate: All`.  All transformations are pushed into the meshes, leaving the object hierarchy as simple place holders.

For a dynamic model, set `Propagate: Scale` to keep positions and rotations in the hierarchy, but push scales into the meshes.  This makes constraints easier to set up.

Caveat: With the left-handed coordinate system, at least one axis must be inverted from its Blender orientation.  The model displays exactly correctly, but constraints need to be set with respect to the inverted axes.  You can choose which axis is inverted with the `Invert` option.  This option only has an effect with `Propagate: Scale`.

Second caveat: if the scale is not the same in all axes, it can result in shear.  MudRunner can't handle it, and neither can `Propagate: Scale`.

For a static model, set `Propagate: Scale` or `Propagate: All`.  With no constraints to set, either can be used.

The new `FlattenCoordinateRoot` setting should generally remain checked.  This removes the extra layer of hierarchy that the original DirectX exporter used to set the coordinate system.

# Keyboard Shortcut

You can set a keyboard shortcut in Blender for the MudRunner Exporter.  *Right click* `File -> Export -> MudRunner (.x)` in the menu and choose `Add Shortcut`.  I like Ctrl-Shift-E as my shortcut.  Be sure to save your User Preferences for future Blender sessions.
