# Compositing Workflows

The **Compositing Workflow** nodes deal with the bread and butter functions required in compositing, but within a VR environment.

• **C_Blender** - is used as a Merge node to combine all images together after manually correcting a stitch.

• **C_Tracker** - similar to Nuke's standard Tracker, but calibrated for pattern tracking in latlong space. Keyframe tracking is not currently supported in latlong space.

• **C_SphericalTransform** - is a tool to convert between different projections, both 360 and partial frame, allowing you to rotate and define the space with a variety of different controls.

• **C_MetaDataTransform** - allows you to apply camera rotations and insert rotation metadata into the metadata stream.

• **C_RayRender** - is a ray tracing renderer alternative to Nuke’s ScanlineRender. It has a number of advantages over scanline-based renderers in a VR context, including:

• the ability to render polar regions in a spherical mapping correctly, without the artifacts inherent in scanline-based rendering in these areas, and

• support for lens shaders, allowing slit scan rendering of multi-view spherical maps. This provides a more natural viewing environment for VR material.

• **C_DisparityGenerator** - computes the disparity vectors between two views, similar to Ocula's O_DisparityGenerator node, which can help when quality checking a solve or warping an image.