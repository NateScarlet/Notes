[Global Illumination](http://docs.redshift3d.com/Content/I/Global%20Illumination.html) > The Irradiance Cache GI Engine

# The Irradiance Cache GI Engine

## How It Works

Global illumination often changes slowly over surfaces. This means that several neighboring pixels could share similar GI lighting without visible artifacts. This, in turn, means we don’t necessarily have to individually compute GI lighting for each pixel on the screen. Irradiance caching takes advantage of this observation and computes GI at sparse points around the image. As a result, rendering takes much less time.

These individual GI points are called “Irradiance Cache Points” and are using during rendering (through interpolation and filtering) to produce a smooth, final result. The figures below show how Irradiance Caching works.

During the irradiance cache computation pass, points are stored on surfaces visible by the camera. On flat areas, lighting changes slowly so few points are needed. Corners typically need more points.

![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000177.png)

During rendering, final shaded pixels (white) are GI-lit using the previously constructed irradiance cache points. That is much faster than computing GI for each individual pixel.

![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000178.png)

The Irradiance Cache can only be used as a primary GI engine.  When multiple GI bounces are needed, the Irradiance Cache can be combined with:

- The Brute-Force secondary GI engine
- The Photon Mapping secondary GI engine
- The Irradiance Point Cloud secondary GI engine

The Irradiance Cache has several benefits:

- It can produce smooth images several times faster than Brute-Force
- The results can be saved to disk for each animation frame. So if you’re tweaking things like antialiasing, glossy “num rays”, area lighting “num samples” and other quality parameters (non-related to GI), you can simply load the GI results and perform quick iterations.
- Certain scenes (like archviz ones) use relatively flat geometry. For example, the floor or the walls of an architectural interior. The irradiance cache can provide a significant performance benefit for such scenes.
- Increasing the final image resolution often does not increase the irradiance cache time linearly. I.e. going from 1280x720 to 2560x1400 (i.e. 4 times more pixels), you might find the irradiance cache processing time taking less than 4 times longer. This depends on the scene complexity and the irradiance cache settings.

The Irradiance Cache has some limitations too:

- Irradiance Cache Points are computed during a separate rendering pass so interactive feedback isn’t possible.
- While a low number of rays shows up as grain in brute-force GI, a low number of rays shows up as “splotches” and flickering in animations with irradiance cache. These artifacts can be more visually distracting than grain.
- There are several user parameters that control point spacing and the overall quality. Proper configuration of these is important for splotch-free and flicker-free results. Learning how to use these settings will involve some trial-and-error.
- If the scene contains a lot of geometric detail (example: foliage covering a big part of the screen), too many irradiance cache points might have to be generated. This cancels the benefits of the irradiance cache algorithm and, even worse, places a burden on GPU memory resources because of the many points which will have to be stored. For these scenes, brute-force might be a better choice. Thankfully Redshift contains a [“force-brute-force” per-object option](http://docs.redshift3d.com/Content/I/Visibility.html#GlobalIllumination) so that such problematic objects can use brute-force instead, while everything else uses the irradiance cache.

## Settings

### Mode/Filename

When “Mode” is set to “Rebuild (don’t save)”, Redshift will compute a new irradiance cache from scratch (for each frame) but will not save it to disk. The frame will be rendered to completion.

When “Mode” is set to “Rebuild (prepass only)”, Redshift will compute a new irradiance cache from scratch (for each frame) and will save it to the user-specified file. The final rendering pass will be skipped.

When “Mode” is set to “Rebuild”, Redshift will compute a new irradiance cache from scratch (for each frame) and will save it to the user-specified file. The frame will be rendered to completion.

When “Mode” is set to “Load”, the computation stage is skipped and the data is loaded from the user-specified file. The frame will be rendered to completion.

### Flythrough Mode

Enabling “Flythrough mode” allows Redshift to compute the current frame’s irradiance cache points using the last frame’s points. This mode should only be used on flythrough animations, i.e. only when the camera is moving. If any objects or lights move, this mode will produce visual artifacts. Since this mode helps with construction of irradiance cache points, it’s only available on the two “Rebuild” modes and is grayed out for “Load”.

### Number of frames to blend

The “Number of frames to blend” parameter is only enabled when the “Mode” is set to “Load”. It allows averaging the results of multiple irradiance cache files (one for each frame) together in order to improve any flickering effects that might be present because of insufficient quality settings and/or difficult lighting situations. Please refer to [this section](http://docs.redshift3d.com/Content/I/The%20Irradiance%20Cache%20GI%20Engine.html#HowToUsePrepass) below for more information on how to use the “Rebuild (prepass)” and “Load” modes. Since this mode has to do with loading and blending multiple frames before rendering, it’s only available for the “Load” mode and is grayed out for the “Rebuild” modes.

Irradiance Cache data is view-dependant which means that it has to be re-generated when either the camera or any objects move. It also has to be regenerated if lights change (position or intensity) and if materials are adjusted. However, there are a few settings that do not affect the irradiance cache:

1. All antialiasing settings
2. Any parameter that has to do with “number of samples”. For example “number of glossy rays”, “number of area light samples”, “depth of field num samples”

If you are making any last-minute adjustments to your frame and tweaking these kinds of parameters you can save some time by re-using the irradiance cache you computed last time using the “Load” mode.

### Show Calculation

This option will show a very rough estimate of the irradiance cache points as they are computed. It will almost certainly contain noise and some visual glitches – don’t worry, though, these are to be expected!

### Use Separate Points For Secondary Rays

By default, points generated by primary (camera) rays are stored together with points generated by secondary rays such as reflection and refraction. While this is typically ok, sometimes there can be flickering artifacts caused by this because the point densities can vary wildly. If you’re getting flickering artifacts on scenes using reflections/refractions, this option will treat the points separately and try to avoid such issues. Treating the points separately incurs a (typically) small performance and storage cost, so enabling this option is advisable only if such flickering issues occur.

Note 
If you’re getting irradiance cache flickering issues, we recommended rendering a few frames with and without reflections/refractions. You can globally enable/disable reflections/refractions in the [Redshift optimizations](http://docs.redshift3d.com/Content/I/Optimizations.html#Start) tab. Please ensure that you enable the “use separate points for secondary rays” option only if you are see flickering with reflections/refractions enabled and no flickering with reflection/refraction disabled!

### Visualize Points

Enabling this will render the irradiance cache points as small discs. We also add a bit of color to each point to make sure that even near-black ones can be seen.

This mode is useful in finding out if some settings are too aggressive. For example if you see a mostly flat part of the image containing too many points this might (possibly) mean that “Color Threshold” is too aggressive.

Using this mode can also help users better understand the effect that thresholds can have on the point densities.

### Min-Max Rate

When the renderer computes the Irradiance Cache Points, it does that in multiple “resolution passes”. It starts with a low-resolution pass and then progressively renders at higher and higher resolutions. The lower resolution passes take care of flat surfaces or low-contrast lighting and the higher resolution passes insert points around areas of more detail and/or contrast. In some ways, this is similar to how adaptive antialiasing works.

The Min-Max rates control the lowest and highest resolutions that the irradiance caching will use to insert points. Here’s what the numbers mean:

- -5 means “divide resolution by 32”
- -4 means “divide resolution by 16”
- -3 means “divide resolution by 8”
- -2 means “divide resolution by 4”
- -1 means “divide resolution by 2”
- 0 means “use final resolution”
- 1 means “use 4 samples per final resolution pixel”

Example:

For a 1920x1080 frame a setting of (-3, 0) will render in four passes:

1. 240x135
2. 480x270
3. 960x540
4. 1920x1080

Most scenes will render fine with the default (-3, 0) setting. If your scene requires very high-resolution (like 4K, for example) you might want to lower the min rate to something like -4 or -5, especially if it doesn’t contain too much detail.

If your scene contains sub-pixel detail, you might see artifacts around that detail if you use a max rate setting of 0. In these cases, it’s advisable that you raise the max rate to 1. Generally speaking, if the max rate is not high enough, small details will be missed and the final render might have GI artifacts appearing as too bright or dark pixels, splotches and light ‘leaking’.

While working on your scene (and doing draft renders), these artifacts might not be as important as rendering speed. For these cases, a max rate of -1 might provide reasonable results. For final renders, though, (and especially if you are rendering animations) it is advisable to use a max rate of 0 or 1.

### Color/Distance/Normal Thresholds

As mentioned above, Irradiance Caching places fewer points on flat or low-contrast surfaces. Redshift provides three threshold parameters to allow the user to define what is considered “flat” or “low contrast”. Later down in this document there are some visual examples showing how these parameters affect the final image quality.

The “Color Threshold” parameter detects contrast in the irradiance cache points and inserts more of them around areas of high contrast. The lower you make this number, the sharper your GI shadows will be but also more points will have to be computed, which means longer rendering times. The values for this parameter should typically range between 0.01 and 0.001. For draft renders you can set this to 2.0 which will introduce the least amount of points and render the fastest but will make the GI shadows blurry and might also introduce flickering during animations. One thing that is important to remember is that you have to use enough rays (described below) to get a reasonable amount of lighting smoothness on your irradiance cache points before lowing the color threshold parameter. Not doing so will make the algorithm incorrectly think that there is GI contrast detail and will introduce even more points.

The “Distance Threshold” parameter controls the number of points near corners and creases. Corners and creases often make GI change rapidly so several irradiance cache points will be needed around them in order to catch these rapid lighting changes. There are “very low”, “low”, “medium” and “high” quality settings. The higher the quality, the more points will be inserted. The default “medium” setting should work fine for most cases. If you are doing draft renders you can use the “low” or “very low” settings – this will introduce the least amount of points around corners/creases and renderer the fastest but will make corner GI lighting blurry (and possibly splotchy) and might also introduce flickering during animations.

The “Normal Threshold” parameter controls how the curvature of objects affects the point density. Just like corners and creases, curved surfaces also can translate into rapid changes of lighting. There are “low”, “medium” and “high” quality settings for this parameter. A lower quality setting will insert fewer points on curved surfaces and vice-versa. The default “medium” setting should work fine for most cases. If lighting appears to be too soft or you’re getting some flickering (during animations) on curved surfaces, you can try using the “high” setting. During draft rendering you can use the “low” setting which will introduce the least amount of points but will make GI lighting too soft on abrupt curvatures and might also introduce flickering during animations.

### Min Detail

The thresholds mentioned above might introduce a very high number of points which can use lots of memory and make rendering slower. The “Min Detail” parameter allows you to control the screen-space density of points in a global manner. A value of 2.0 means “try to not insert points that are closer than two pixels apart”. A value of 4.0 is for four pixels, etc.

For final renders you should set this value to 0.0. For draft renders you can try increasing it to something like 4.0 or 8.0. The higher the number, the fewer points will be created which will make the rendering faster but also blurrier and potentially with animation flickering.

### Radius Factor

During final rendering, the irradiance cache points are used to interpolate final GI lighting. The “Radius factor” parameter allows the user to control the ‘area of influence’ of the irradiance cache points. Using large numbers will make the GI lighting a bit blurrier but also with fewer splotches. For the majority of cases you should use a setting of 2.0. During draft renders (and with low quality threshold settings) you can try a setting of 4.0.

Using values larger than 2.0 might have some impact on memory and also final rendering performance.

### Num Rays / Adaptive Amount / Adaptive Threshold

The “Num Rays” parameter controls the quality of each irradiance cache point. The lighting at each point is computed in a way similar to brute-force GI, i.e. several rays are shot out of it. Using too few rays will introduce a “splotchy” effect that is very distracting. Scenes that contain several lights (or fewer big lights) can typically use fewer rays (between 500 and 1000). If the scene contains very few bright lights or not enough lighting is coming through small openings (windows) the number of rays might have to be increased a lot to get clean results. We have seen architectural interior scenes that require numbers such as 2000 – 4000 for a perfectly clean result.

Not all irradiance cache points need the same number of rays. For example, some points might be in ‘exposed’ areas and can be seen by several lights – these points only need a few rays to get a clean result. Other points, on the other hand, might be hidden behind objects and might have a hard time finding light – these points need more rays. Redshift takes care of this situation using adaptive sampling, i.e. it automatically adjusts the number of rays for each irradiance cache point. The user, though, has to specify a couple of parameters to help Redshift make the necessary choices during adaptive sampling,

The “Adaptive Amount” parameter controls the percentage of rays that should be shot initially. For example, if “Num Rays” is 1000 and “Adaptive Amount” is at 0.8, this means that 80% of the rays will be adjusted (i.e. 800 rays) and the initial 20% of the rays will be shot (i.e. 200 rays). If the value was at 0.3, this means that 30% of the rays will be adjusted (300 rays) and 70% of the rays will be shot (700 rays in this example). So, the lower you make this number, the less adaptive the algorithm is. Setting this parameter to 0 means that Redshift will shoot all 1000 rays for each point. Scenes of reasonable contrast will work fine with the default 0.85 value. If you even work with a scene that has extreme contrast (i.e. very strong indirect illumination coming from a small light source, or a far away light source), it might be necessary to reduce this number to something like 0.5 in order to avoid ‘early termination’ artifacts. Early termination is when the algorithm thinks that there no more lighting to be gathered and stops abruptly – even though there might be more lighting that could have been gathered with more rays. Another way of fixing this issue is leaving the “Adaptive Amount” as-is but actually raising the “Num Samples”. This means that the algorithm will shoot more initial rays and will have a much better chance of finding any ‘difficult’ light sources.

The “Adaptive Error Threshold” controls how many of the remaining rays will be used. Like mentioned above, the algorithm always shoots a percentage of the rays initially. These initial rays are used to compute a contrast value which is compared against “Adaptive Error Threshold”. The comparison defines how many more rays will be needed for that irradiance cache point. The lower this parameter, the more ‘sensitive’ the algorithm becomes - which means that more rays will be shot. If your renders exhibit persistent ‘splotches’ (meaning: you increased the “Num Rays” but the results are still not clean) the reason might be “Adaptive Error Threshold”: you could try reducing it to values like 0.005 or even 0.001.

### Num Smoothing Passes

Normally, in order to remove splotchy artifacts one has to increase “Num Samples”. A faster alternative is to simply blur the irradiance cache points together. This is what “Num Smoothing Passes” does. Setting this parameter to zero will do no smoothing. The more smoothing passes you do, the smoother the final result.

Smoothing the results will cause some loss of GI detail (shadows) and might introduce a bit of flickering in animations - but both of these issues might be acceptable during draft rendering. Usually a value of 1 is an acceptable compromise: it rarely causes issues during animations, it only causes a bit of loss of sharpness and the final results do look smoother.

## How To Use The Settings To Get A Clean Result

Here we show some common issues you might encounter and how to adjust your settings in order to solve these issues.

### Case 1 : Thin details have splotches around them and/or are flickering during animation

Solution Step A: Ensure “Min Radius” is set to zero

Solution Step B: Increase “Max rate”

Below we show a simple scene that contains some thin detail on the wall. If the max rate is not high enough you might see the kind of artifact shown below. In these cases, increasing the max rate will help reduce or eliminate the issue.

Please note that the scenes below use strong antialiasing settings. We did this intentionally to show that the issues are not related to antialiasing – which is a common misconception among users when they encounter this issue.

| Scene uses a “Min Rate” of -3 and a “Max Rate” of -1. The max rate being -1 is the reason why there are lighting artifacts around the thin geometry | Increasing the max rate to 0 solves these issues. Similarly, if you get artifacts with a “Max Rate” of 0, you could increase it to 1. |
| ---------------------------------------- | ---------------------------------------- |
| ![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000179.png) | ![img](http://docs.redshift3d.com/Content/Resources/Images/I/02000004.jpg) |

### Case 2 : The GI solution contains splotches in specific areas. There is ‘crawling’ around these areas in animations.

Solution Step A: Increase “Num Rays” if it’s relatively small (less than 1000 rays)

Solution Step B: If “Num Rays” is already a large number (2000-3000 rays or more) decrease “Adaptive Error Threshold”

Solution Step C: If “Num Rays” is already large and “Adaptive Error Threshold” is already small, decrease “Adaptive Amount”

Even though Redshift uses an adaptive sampling scheme, it has to operate within certain user-defined parameters: “Num Rays”, “Adaptive Error Threshold” and “Adaptive Amount”. When these parameters are too constrained (for example: too few rays) rendering might be faster but it also introduces artifacts. Here we show how to adjust these parameters to avoid visual artifacts.

Below is a scene that is using a small number of rays (100) and is showing visible splotches in corners. Adaptive Amount is 0.85 and Error Threshold is 0.01. Adjusting these two parameters would have no effect on the splotches because the number of rays is too small. So, in this case, the first thing we should do is increase “Num Rays”.

| Using only 100 rays. Splotches visible on wall corners and between the wall blades. Irradiance cache computation time: 1.5 seconds. | Using 2000 rays. Splotches are improved a lot but the still some faint artifacts on the walls. Irradiance cache computation time: 2.4 seconds. |
| ---------------------------------------- | ---------------------------------------- |
| ![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000180.png) | ![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000181.png) |

The second image looks much better, but still has a very faint issue on the wall/ceiling corner. Most of the time this is not an issue in still images but it might show up as a slight ‘ripple’ in animations.

The problem here is that the default adaptive threshold of 0.01 is preventing the system from using enough rays. Halving it to 0.005 uses more rays but helps produce a clean result. This is shown below.

For a near-perfect frame we decrease “Adaptive error threshold” to 0.005. Irradiance cache computation time: 3.8 seconds.

![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000182.png)

So how exactly should someone adjust the “Adaptive Amount” and “Adaptive Error Threshold” parameters?

There are two main issues that can come with improperly adjusted adaptive sampling parameters:

1. The adaptive error threshold is too high which means that not enough rays will be used. This can cause splotchy results.
2. The adaptive amount is too high which makes the algorithm terminate too early and miss lighting. Again, the result is splotchy GI.

Redshift’s default “Adaptive Error Threshold” is 0.01. While this works ok for most scenes, as it was shown above, it is advisable that final renders use a lower number such as 0.005 (i.e. half the default) or lower (e.g. 0.001). Generally speaking, after the user increases “Num Rays”, “Adaptive Error Threshold” should be the next thing to be adjusted.

What about the second issue (terminating too early)? Adaptive sampling works by shooting an initial number of rays, computing a contrast and then, if the contrast is too high, shooting some more rays to clean up the result. If “Adaptive Amount” is too high, then too few initial rays will be shot – and these might completely miss important lighting. The algorithm then is fooled into thinking that there is no more work to be done which stops the sampling. Stopping the sampling is called “early termination”. Except, in this case, the termination is too early! The result is, you guessed it, splotches!

Most of the times, simply increasing “Num Rays” will take care of this issue so you might never see this issue. This is because a larger “Num Rays” means a larger number of initial rays which means a smaller chance of missing important lighting. But, sometimes, lighting can extremely hard to find. In these cases, you might have to decrease “Adaptive Amount”.

The example below shows a thin translucent box that contains a very bright point light. It was rendered with a very high number of rays (8000) and a very low adaptive error threshold (0.001). However, using the default 0.85 adaptive amount, it still exhibits serious artifacts near the bottom of the image. This is because these pixels are fairly far away from the light source and the initial rays fail to find any lighting – so the algorithm creates irradiance cache points that are black. Lowering the adaptive amount to 0.5 improves the result.

| “Adaptive Amount” set to the default 0.85. Visible artifacts can be seen on the bottom half of the image | “Adaptive Amount” set to 0.5. Although there are still some faint issues, this is a big improvement over the 0.85 example. This comes at the cost of more initial rays, though. |
| ---------------------------------------- | ---------------------------------------- |
| ![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000183.png) | ![img](http://docs.redshift3d.com/Content/Resources/Images/I/3000184.png) |

### Case 3 : Irradiance cache results look too blurry compared to brute-force

Solution Step A: Disable smoothing passes (if enabled)

Solution Step B: Reduce “Radius Factor” (if more than 2.0)

Solution Step C: Decrease “Color Threshold”, if lack of detail means blurry shadows

Solution Step D: Use higher quality settings for “Normal Threshold”, if lack of detail means too blurry lighting on curved surfaces

Because irradiance caching doesn’t compute GI on a per-pixel basis, it cannot provide quite the same amount of sharpness as the brute-force technique. However, by adjusting a few settings, you can often get fairly close to brute-force detail while still enjoying faster rendering times and grain-free results.

Let’s look at a simple example: a translucent box containing a point light casting some shadows. We will use a brute-force rendering as reference.

| Brute-force rendering. Notice the well-defined shadows. | Irradiance caching using default values. The shadows are blurred to the point of being completely invisible. | Irradiance caching with blurring passes disabled, radius factor was left at 2.0, color threshold was reduced to 0.001. The shadows are now more visible. |
| ---------------------------------------- | ---------------------------------------- | ---------------------------------------- |
| ![img](http://docs.redshift3d.com/Content/Resources/Images/I/0300000A9.png) | ![img](http://docs.redshift3d.com/Content/Resources/Images/I/0300000B8.png) | ![img](http://docs.redshift3d.com/Content/Resources/Images/I/0300000C8.png) |

While reducing the color threshold reclaimed some of the detail, we advise doing so only if absolutely necessary. The reason is that reducing it will force many irradiance cache points to be computed. This will increase rendering times and memory requirements. If this kind of fidelity is necessary, it’s advisable that you use brute-force instead.

Please read “case 4” below for notes regarding reducing the color threshold.

So what about “Distance Threshold” and “Normal Threshold”?

“Distance Threshold” should be typically left at “medium”. While using the “high” setting will capture a bit more definition near corners and creases, “Color Threshold” will often catch those details too – and will do so only when there is actual contrast. The couple of images below show how lowering the distance threshold makes the shadow definition a bit sharper near the pillars.

| Default Values with Distance Threshold set to “Medium” (which is also the default) | Default Values With Distance Threshold set to “High”. There is only a slight improvement near the base of the pillars. |
| ---------------------------------------- | ---------------------------------------- |
| ![img](http://docs.redshift3d.com/Content/Resources/Images/I/0300000B8.png) | ![img](http://docs.redshift3d.com/Content/Resources/Images/I/0300000D8.png) |

Similarly, for “Normal Threshold”, we advise using the default “Medium” setting. If you are rendering animations and your geometry is low-poly, using the “High” setting can help improve any flickering artifacts you might experience.

### Case 4 : Lowering the “Color Threshold” parameter is making my render take a lot longer and is more splotchy!

Solution: Make sure that the GI solution is as clean as possible before lowering “Color Threshold”. Follow the steps outlined in “Case 2”

Like mentioned earlier, the “Color Threshold” parameter is useful when you want more definition around GI shadows. It works by comparing neighboring irradiance cache points and, if it detects discontinuities in the lighting, it inserts more irradiance cache points in order to catch the extra detail.

The problem is that discontinuities might exist not because of an actual shadow but because of low irradiance cache settings! For example, setting “Num Rays” to a low number makes each irradiance cache point very noisy and different to its neighbors. When this happens, the algorithm behind “Color Threshold” might be fooled into thinking that there is actual detail there and will keep adding more points. That can make the frame take a lot longer to render and it will almost certainly not improve the final result. In fact, in some cases, it can even make it worse!

So it’s strongly advisable that, before you lower “Color Threshold”, you adjust your “Num Rays” and “Adaptive Threshold” to get a smooth result – as described in “Case 2” above. Using the point visualization feature can also help detect when this issue happens.

## How to use “Rebuild (prepass)” and “Load” modes to improve/eliminate flickering artifacts

The performance benefits of the irradiance cache lie on the fact that expensive GI computations are interpolate and are not executed on each and every pixel. However, this interpolation can sometimes miss important lighting information and can cause flickering artifacts on animations. This typically happens if:

- The settings are not sufficiently high (e.g. num rays)
- The geometry has certain irregularities or very small detail
- The lighting conditions are ‘difficult’, i.e. only small parts of the scene are lit by direct lighting

If you encounter any such artifacts, you can try the following procedure:

1. First, select “Rebuild (prepass)” and select an appropriate filename – or use the default filename.
2. If you are using the irradiance point cloud for secondary GI bounces, set its mode to “Rebuild”. If you don’t want the irradiance cache files to be saved, clear its “Filename” box.
3. Render your animation. During rendering, one irradiance cache file for each frame will be generated but the final rendering pass will be skipped.
4. Then, select the “Load” mode and adjust the “number of frames to blend” parameter. Render your animation. For each frame, Redshift will now load a number of ‘neighboring frame’ irradiance cache files, blend them together and use the blended result to render the final frame. Because of this inter-frame blending, any temporal artifacts (flickering) will be reduced or even eliminated.

The “number of frames to blend” parameter controls how many ‘neighboring’ irradiance cache files will be loaded and blended together. For example, a setting of 2 means “load the previous two and next two frames”. So, for this example, the algorithm will blend 4 neighboring frames plus the current frame, i.e. 5 frames together. A setting of 1 means “load the previous and next frames”, so 3 frames will be blended together.

Larger numbers of blended frames means less flickering. However, blending too many frames together can create a light ‘ghosting’ or ‘lagging’ effect in scenes with fast moving objects or lights. If your irradiance cache settings are properly adjusted, a setting between 2 and 4 should be sufficient to improve artifacts to the point of either being completely eliminated or barely visible.

Note
Irradiance cache files can be large so be sure to select a folder/drive that has enough free space.

## Memory Considerations

If you are rendering very high-resolution images or moderate resolutions but the scene contains a lot of detail, you might get an error regarding the points not fitting in the allotted GPU memory space. The message will read like this:

Irradiance cache points don't fit in VRAM. Frame aborted. Please either reduce Irradiance Cache quality settings or increase the irradiance cache memory budget in the memory options

If your settings are just right and don’t want to modify them, the easiest thing to do is simply increase the memory budget. By default, Redshift reserves 64MB for the irradiance cache. You can try raising this number to 80, 100 or larger. To edit the Irradiance Cache memory budget, go to Redshift options, Memory Tab and modify the parameter called “Irradiance cache working tree reserved memory”. The parameter units are in megabytes.

Alternatively, you might want to modify Irradiance Caching parameters that affect the number of generated points:

1. Increase “Min Detail”. This is a global parameter that used to prevent too many Irradiance Cache points from being generated. For high-resolution frames you can try increasing that to values like 2 or 4.
2. Lower “Max Rate”. If it’s set to 1, you might want to try 0. If the frame is very high-resolution (for example, 4K) you might even want to try -1
3. Increase “Color Threshold”. Getting really good GI shadow definition can take a lot of points. If your frame already contains interesting shadows from direct lights, the sharpness of the extra GI shadows might not be as important. This is especially true if you are using techniques such as “Portal Lights”.
4. Lower “Normal Threshold”. If this is set to 8 or higher, this might be overkill. Try a value like 4, instead.

------

Copyright © 2016 Redshift Rendering Technologies, Inc.