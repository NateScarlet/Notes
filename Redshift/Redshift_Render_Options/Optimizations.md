[Redshift Render Options](http://docs.redshift3d.com/Content/I/Redshift%20Render%20Options.html) > Optimizations

# Optimizations

## Maximum Trace Depth

The trace depth limits control how deep reflections and refractions can go. There exist separate settings for reflection and refraction. The “combined” setting specifies the upper limit for both reflections and refractions. Let’s say, for example, that reflection, refraction and combined are all set to a value of 10. If a ray has already been reflected 8 times, then it can only be reflected or refracted 2 more times because the combined trace depth is 10.

Warning
Raising the trace depth limits can increase rendering times!

Most scenes can get away with fairly low reflection and refraction trace depth limits. This is especially true for reflections. How often can you see a reflection of another reflection of another reflection… and so on?

Refractions, on the other hand, can be more challenging. Scenes that contain glass might require the refraction trace depth limit to be raised to avoid incorrect results behind a few layers of glass, as shown below:

| Refraction trace depth limit set to 3. Even though it might look correct, several refractions are skipped. | Refraction trace depth limit raised to 16. Both the refractions and shadows are now correct. |
| ---------------------------------------- | ---------------------------------------- |
| ![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000340.png) | ![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000341.png) |

 

Similarly, an “opposing mirrors” scene like the one shown below will require the reflection trace depth limit raised.

| Reflection trace depth limit set to 3. The mirror-in-mirror reflections of the sphere are cut too early. | Reflection trace depth limit raised to 16. The sphere is reflected several more times. |
| ---------------------------------------- | ---------------------------------------- |
| ![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000342.png) | ![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000343.png) |

## Hair Min Pixel Width

Please click [here](http://docs.redshift3d.com/Content/I/Hair%20Min%20Pixel%20Width.html#Start) for more information on the function and parameters of hair min pixel width.

## Cut-off Thresholds

Warning
For advanced users only! Incorrect settings can generate noisy images or long rendering times!

As rays go through reflections, refractions or shadows, they get tinted and become dimmer. For example, a ray coming from the camera might hit a very faint mirror. Whatever is reflected on that mirror will be dim. When the rays become dim, they contribute very little to the final image so there is no point for the renderer to keep bouncing them around.

The Cut-off threshold set of parameters allow the user to specify minimum values that are considered “black” and allow the renderer to terminate tracing earlier. The defaults should work fine for most scenes but, in some extreme cases, a very dark mirror might be reflecting an extremely bright piece of geometry. If the renderer “cuts off” the mirrored rays early, grain will appear. If you suspect this is happening to your scene, you can try lowering these numbers. To disable this optimization altogether, set the values to 0.0.

The test scene below shows what happens if there are very bright objects in the scene and the cutoff thresholds are not low enough. In the middle of the scene there is a glass reflective and refractive sphere. Around it are 4 very bright self-illuminating spheres. The reflection and refraction trace depths are set to 16 so the reflections/refractions of the self-illuminating spheres ‘repeat’ many times inside the glass sphere.

The scene setup

![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000344.png)

All cutoffs are disabled. This is the reference (best quality) image.

![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000345.png)

| Cutoffs set to 0.1. This is an aggressive setting. Notice that several reflections/refractions are now rendering noisy. | Cutoffs set to 0.01. A big improvement over the last image, but there’s still some noise in the deeper reflections. | Cutoffs set to 0.001. This is the default value. In this case, it produces a near-identical result to the reference image. |
| ---------------------------------------- | ---------------------------------------- | ---------------------------------------- |
| ![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000346.png) | ![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000347.png) | ![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000348.png) |

 

## Russian-Roulette

Warning
For advanced users only! Incorrect settings can generate noisy images or long rendering times!

Certain shaders need to shoot multiple different kinds of rays. For example, a glass shader needs to shoot a ray for reflection and another one for refraction. The architectural shader can shoot two reflection rays (with different gloss values) and one refraction ray. The car paint shader shoots two reflection rays (with different gloss values). When the rays of such shaders ‘see’ other shaders of the same kind, the number of rays that have to be shot can grow exponentially with increasing trace depths. The initial two rays of a glass shader might become 4 rays on the next trace depth, then 8, then 16, 32, 64, and so on.

Russian-Roulette allows the renderer to shoot only one kind of ray once the importance of the ray is low. For example, a glass seen through a very faint mirror can often get away with sometimes shooting a reflection ray and some other times shooting a refraction ray. Choosing which kind of ray to shoot (reflection or refraction) is driven by shader parameters. If a glass, for example, is very transparent and only has a very faint amount of reflection, the renderer will mostly choose refractive rays versus reflective ones.

The “Importance Threshold” decides when the renderer will start performing this optimization. Very low numbers mean “start doing it for very dim rays” while higher numbers mean “do it for slightly brighter rays”. So the higher the number, the earlier the optimization will happen. Starting it too early, though, can introduce grain artifacts. If you see grain in your glass and you are suspecting the Russian-Roulette, you can try lowering this number to 0.001. To disable this optimization completely, set it to 0.0.

The “Falloff” parameter ‘eases’ into the Russian-Roulette optimization. This means that once a ray’s intensity crosses the “Importance Threshold” value the renderer won’t go abruptly into Russian Roulette but will do it gradually. This improves potential noise-banding artifacts. How gradually the renderer will ease into Russian-Roulette optimization is controlled by the “Falloff” parameter. Setting this parameter to 0.0 will enable the optimization abruptly, while 1.0 does it very smoothly. It’s very rare that users will need to adjust this parameter, so its advised you leave it at 0.5.

To demonstrate the Russian-roulette parameters, we’ll use the same scene we used for the cut-offs.

Russian-Roulette is disabled. This is what the frame is supposed to look like.

![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000345.png)

| Importance Threshold set to 0.1. The renderer has to choose between reflection and refraction way too early which produces excessive noise! | Importance Threshold set to 0.01. While there is less noise compared to before, it’s still visible. | Importance Threshold set to 0.001 (the default). Russian-roulette now happens very rarely, which eliminates all noise. |
| ---------------------------------------- | ---------------------------------------- | ---------------------------------------- |
| ![img](http://docs.redshift3d.com/Content/Resources/Images/I/0300000A18.png) | ![img](http://docs.redshift3d.com/Content/Resources/Images/I/0300000B16.png) | ![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000345.png) |

## Texture Sampling

Redshift supports high quality texture mapping via ‘Anisotropic’ filtering. Redshift also supports fast but lower quality texture mapping techniques such as ‘Bilinear’ (blurry) and ‘Point’ (blocky).

Most scenes only need high-quality texture mapping for parts of the image that are directly visible to the camera, i.e. the “primary rays”. Secondary rays (reflections, refractions, GI, lights) and shadow rays are often less visually important so they can get away with using lower-quality texture sampling techniques. For this reason, by default, Redshift enables ‘Anisotropic’ for primary rays and ‘Bilinear’ for secondary and shadow rays.

Tip
If you’re rendering a scene that uses very clear mirrors or glass and seem to be seeing blurry textures through those mirrors, you might want to increase the quality of the secondary rays to ‘Anisotropic’. Mind you, though, that this can increase rendering times!

MIP-maps are pre-filtered (blurred) versions of the textures and are automatically computed by Redshift behind the scenes. MIP-maps are useful in making textures appear less noisy when viewed from far away. Each texture has several MIP-maps associated with it. For example, a 1024x1024 texture will have a 512x512, 256x256, 128x128, 64x64, 32x32, 16x16, 8x8, 4x4, 2x2 and 1x1 MIP maps. Each time the renderer needs to pick a samples for texture mapping, it selects two consecutive MIP-maps (for example 256x256 and 128x128) depending on how far away the textured object is from the camera and then filters in-between them. The best filtering for this job is called “tri-linear interpolation”. The “MIP Filtering Trace Depth Threshold” forces the renderer to disable “tri-linear” filtering between MIP-map levels after a specified trace depth, which will help performance but at the potential cost of introducing banding artifacts. Generally, banding artifacts will not be visible beyond certain trace depths, so it is recommended that you use the default settings and allow the renderer to use switch to “bi-linear” filtering after the first trace depth.

The “Copy Pre-Converted Textures to Cache Folder” option is used in junction with textures that have been pre-converted using the ‘TextureProcessor’ tool. By default this option is enabled, the assumption being that the local texture cache folder has better IO performance than the source texture folder, which is common for example when source textures are stored on slower network drives or when the local texture cache folder is on an SSD drive while the source texture folder is on a mechanical drive. By copying the pre-converted textures to the local machine cache folder, the out-of-core texture file streaming during rendering can be significantly faster, which can have a significant impact on rendering performance. This option should be disabled when the IO performance of the texture cache folder is equal to or lower than that of the source texture folder.

## Global Overrides

The “Enable Reflections” and “Enable Refractions” options globally enable/disable reflections and refractions respectively.

The “Enable Subsurface Scattering” option bypasses all subsurface scattering preprocessing and renders the SSS shaders as diffuse.

Similarly, “Enable Tessellation And Displacement” enables/disables all tessellation and displacement.

The “Enable Emission” option globally enables/disables emission on materials.

------

Copyright © 2016 Redshift Rendering Technologies, Inc.