[Redshift Render Options](http://docs.redshift3d.com/Content/I/Redshift%20Render%20Options.html) > Gamma

# Gamma

## General

Gamma correction (also known as “color correction”) adjusts the colors of the final image so that they match the typical response of computer monitors. Due to legacy reasons, a computer monitor displays colors on a 2.2 gamma curve. What this means is that the color gray (0.5, 0.5, 0.5) actually shows up as (0.22, 0.22, 0.22), i.e. a darker shade of gray instead of a shade that is exactly between black (0.0, 0.0, 0.0) and white (1.0, 1.0, 1.0) – as one would expect.

Gamma correction remedies that inaccuracy.

The following two pictures show a gray diffuse-lit sphere with and without gamma correction:

| Gamma 1.0 (off)                          | Gamma 2.2                                |
| ---------------------------------------- | ---------------------------------------- |
| ![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000158.png) | ![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000159.png) |

Sometimes users prefer that the renderer produces a “linear” (gamma 1.0) image so that they can manually perform gamma correction, color curves and other final adjustments using an external editing program. For this reason, Redshift provides separate gamma controls for what is shown in the 3D modeling package (“Display Gamma”) and the final image file (“File Output Gamma”). This allows the user to preview with gamma correction while saving out linear (gamma 1.0) images.

The “Automatic” setting in the “File Output” gamma works as follows: if the final image file is using an 8-bit format (such as TGA or PNG), the “Display Gamma” value will be applied to it. If the file is using a higher color precision image format (such as OpenEXR), no gamma correction will be applied to it. This is in line with composition packages like Nuke which, by default, assume high color precision images being linear and 8-bit images using an sRGB or Gamma 2.2 color space.

## Gamma Correction And Adaptive Sampling

Redshift’s adaptive sampling algorithms are gamma-aware as gamma correction can significantly shift the image intensities and, therefore, the relative ‘visual importance’ of a pixel. All the adaptive sampling algorithms use the “Sampling Gamma” value. We strongly recommend that the “Sampling gamma” value matches your final “intent” with regards to gamma. I.e. if you are planning on either gamma-correcting the image externally or having Redshift correct it for you, please set the sampling gamma to the same value.

In the majority of cases, leaving this setting to its default “same as display gamma” setting will be sufficient.

## Gamma Correction And Textures

When gamma correction is used, the color profile of your textures has to be set accordingly. Setting it to “Automatic” will work fine for most cases. That mode assumes that any 8-bit image format (such as TGA, BMP, etc) is set to a 2.2 gamma and that higher-color-precision images (such as OpenEXR) are already linear. In most of the cases these assumptions are right. Also please note that you only need to do that for textures that are pictures. BumpMaps, NormalMaps and other kinds of control textures should not be adjusted! The importance of properly setting the texture color profile is shown below.

The first image, is the texture itself (the default Softimage XSI texture). The second and third images are both rendered with gamma 2.2.

Original texture

![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000160.png)

| Gamma 2.2 render using an incorrect image clip color profile (“linear”). The texture looks washed out. | Gamma 2.2 render using the correct image clip color profile (“automatic” – “srgb” would work too). Texture looks like original. |
| ---------------------------------------- | ---------------------------------------- |
| ![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000161.png) | ![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000162.png) |

In XSI, you can adjust the color profile of your texture clip as shown below:

![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000163.png)

In Maya, you can adjust the color profile of your File node, as shown below:

![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000164.png)

## Gamma Correction And AOVs

The rules for gamma correction on AOVs are the same as the main beauty pass: if “File Output Gamma” is set to “Automatic”, any AOV that is using an 8-bit format will be written out using the “Display Gamma” value while higher color precision image formats will be written out linear (gamma 1.0).

So if your “Display Gamma” is set at 2.2, and open the produced AOV image files in an image viewing program, 8-bit file formats like PNG or TGA will look brighter than format like OpenEXR. This is expected behavior. As mentioned previously, most applications assuming files like OpenEXR to be linear (gamma 1.0) and files like PNG to be sRGB.

We recommend users leaving the “apply color correction” option enabled for any AOV that allows it.

 

------

Copyright © 2016 Redshift Rendering Technologies, Inc.