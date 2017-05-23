# Introduction to CaraVR

CaraVR is a suite of nodes designed to assist compositing of mono and stereo live action 360 footage in post-production. All CaraVR nodes integrate seamlessly into Nuke and are applied to your clips as any other node. They can all be animated using the standard Nuke animation tools.

The CaraVR nodes can be separated into three broad categories: **stitching**, **workflow**, and **review**. These categories are outlined below.

# Stitching

The** Stitching** nodes take care of the process of aligning your camera rig output and joining the separate images into a single, cohesive frame. You can also perform some optional global colour corrections at this stage.

• **C_CameraSolver** - calculates the geometry for the multi-camera rig. This defines the location and orientation for each camera so that the images can be stitched. See [Stitching Camera Rigs](../solving_rigs/solver/solving_and_stitching.html#C_Camera) for more information.

• **C_Stitcher** - automatically generates a spherical lat-long by warping and blending between the different input images. See [Stitching Images Together](../solving_rigs/stitcher/stitching_cameras.html) for more information.

• **C_ColourMatcher** - an optional step to perform global gain-based colour correction for all the views in a rig to balance out differences in exposure and white balance. See [C_ColourMatcher](../solving_rigs/c_colourmatcher.html) for more information.

# Workflow

The **Workflow** nodes deal with the bread and butter functions required in compositing, but within a VR environment.

• **C_SphericalTransform** - a tool to convert between different projections, both 360 and partial frame, allowing you to rotate and define the space with a variety of different controls.

• **C_Blender** - is used as a Merge node to combine all images together after manually correcting a stitch.

• **C_DisparityGenerator** - computes the disparity vectors between two views, similar to Ocula's O_DisparityGenerator node, which can help when quality checking a solve.

• **C_RayRender** - a ray tracing renderer alternative to Nuke’s ScanlineRender. It has a number of advantages over scanline-based renderers in a VR context, including:

• the ability to render polar regions in a spherical mapping correctly, without the artefacts inherent in scanline-based rendering in these areas, and

• support for lens shaders, allowing slit scan rendering of multi-view spherical maps. This provides a more natural viewing environment for VR material.

• **C_Tracker** - similar to Nuke's standard Tracker, but calibrated for pattern tracking in lat-long space. Keyframe tracking is not currently supported in lat-long space.

• **C_MetaDataTransform** - allows you to apply camera rotations and insert rotation metadata into the metadata stream.

# Review

CaraVR provides a monitor out plug-in for the Oculus CV1, DK2, and HTC Vive, which work in a similar way to Nuke’s existing SDI plug-ins. They're handled by the official Oculus SDK on Windows, by OpenHMD on Mac OS X and Linux, and by SteamVR for the HTC Vive. See [Reviewing Your Work](../review_tools/review_sdi_out.html) for more information.