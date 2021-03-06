# OpenSimplex 2

Successors to OpenSimplex Noise, plus updated OpenSimplex. Includes 2D and 3D noise. 4D noise is coming!

* The provided 3D and 4D functions in **OpenSimplex2S** (OpenSimplex 2, smooth version / "SuperSimplex") are about as fast as optimized OpenSimplex, but have better uniformity.

* The provided 3D and 4D functions in **OpenSimplex2F** (OpenSimplex 2, faster version) are about as fast as common Simplex noise implementations, but use much different processes.

* The 2D functions aren't intended to represent new developments in the same vein as the 3D+ functions. They are just the logical pairings. Both 2D functions are implemented using lookup tables, use lattice-symmetric gradient sets, and perform similar to or faster than the average.

* All functions are given new gradient sets that are symmetric with the lattice, but don't cause neighboring vertex gradients to constructively interfere.

* Updated Legacy OpenSimplex with new gradient sets is included in java/legacy and csharp/legacy.

The classes in [java/areagen](https://github.com/KdotJPG/New-Simplex-Style-Gradient-Noise/tree/master/java/areagen) offer speed-optimized whole-area generators, which operate by flood-fill queue on the noise lattice. (i.e. they don't use a "range")

* The only differences between the two versions' area generators are: **radius parameter** and **normalization constant**.
  * The radius can be straightforwardly reduced for faster noise, or increased for smoother noise. There are no geometric traversal steps to cause discontinuities, and no hardcoded point computations to limit performance increases, as would be the case with varying the radius in the evaluators.
  * The normalization constant is baked into the same gradient set as the evaluator. It can be recomputed using [Noise Normalizer](https://github.com/KdotJPG/NoiseNormalizer). If left as is, the noise will still function correctly, it will just have a different output range.

#### TODO:

* More language ports
* Move radius into unified constant (for Area Generators in particular)
* Pull some of the explanation from [the reddit post](https://www.reddit.com/r/VoxelGameDev/comments/ee94wg/supersimplex_the_better_opensimplex_new_gradient/) into this readme.

#### Maybe TODO:

* Create combined OpenSimplex2F and OpenSimplex2S in one file, reducing repetition for someone who needs both.
* Include octave summation (fBm), ridged noise, etc.
* Simultaneous multi-instance evaluation.
* Disc/Ball-output noise (Outputs 2D/3D/etc. vector for more directionally-uniform domain warping)
* Tileable 2D noise (slightly mis-skewed triangular grid which repeats properly over a desired rectangle)
* Tileable 3D noise (using an extension of the above)
* Tileable 3D noise (exact, using the "classic" lattice orientation)

#### Change Log
* Shortened lookup table for Simplex/OpenSimplex2F 4D (July 5, 2020)
* Add 4D to OpenSimplex2F Java/C#, port OpenSimplex2S 4D to C#. (July 5, 2020)
* Add 4D to OpenSimplex2S Java. (Apr 30, 2020)
* Replaced individual renders in readme with consolidated renders. (Feb 10, 2020)
* Replaced 12-direction 2D gradient set with a 24-direction set, to reduce visible feature repetition in thresholded single-octave 2D noise. (Feb 10, 2020)
* Renamed filenames FastSimplexStyleNoise to OpenSimplex2F, and SuperSimplexNoise to OpenSimplex2S. (Feb 10, 2020)
* Moved legacy OpenSimplex into legacy directories. (Feb 10, 2020)
* Slightly reorganized description above, and added TODO/changelog. (Jan 23, 2020)
* Renamed / additionally named the noise "OpenSimplex (2.0)", separated into two versions/variants. (Jan 23, 2020)
  * SuperSimplex and FastSimplexStyleNoise are very similar to each other algorithmically, and are in the same spirit as the original OpenSimplex.
  * OpenSimplex is used in a lot of projects, and the naming might help facilitate adoption of the new noise in its place.
* Add C# ports of evaluators. (Jan 13, 2020)
* Create separate files which include area generators. (Jan 13, 2020)
* Renamed PlaneFirst evaluators to XYBeforeZ, and added XZBeforeY. (Jan 13, 2020)
* Fixed equals() method in AreaGenLatticePoint3D for area generators. (Dec 24, 2019)

## Renders

### 2D Noise

![Renders 2D](images/renders2D.png?raw=true)

* OpenSimplex2S is a smoother copy of OpenSimplex2F.
* OpenSimplex2S and Updated OpenSimplex are effectively identical.
* Original OpenSimplex produced more straight parts and was not probabilistically lattice-symmetric.

### 3D Noise (XYBeforeZ Orientation)

![Renders 3D XYBeforeZ](images/renders3Dpf.png?raw=true)

* OpenSimplex2F and OpenSimplex2S, 2D slices of 3D XYBeforeZ, keep mostly the same properties as you move along the third axis.
* Updated OpenSimplex looks good in both slices, but the slices look different from each other. In an animation, this is particularly noticeable.
* Original OpenSimplex was less uniform and not probabilistically lattice-symmetric.

### 3D Noise (Classic Orientation)

![Renders 3D Classic](images/renders3Dc.png?raw=true)

* OpenSimplex2F and OpenSimplex2S, 2D slices of 3D in the classic lattice orientation, look decent but are less ideal for X/Y planes being the primary focus.
* This Updated OpenSimplex render appears to show less directional bias than original OpenSimplex.

### 4D Noise (XYBeforeZW Orientation)

![Renders 4D](images/renders4Dpf.png?raw=true)

* OpenSimplex2S 4D has higher apparent contrast than original OpenSimplex.
* OpenSimplex2F 4D has a very dotty appearance. Fine for fBm but probably not ridged noise.

### 4D Noise (XYZBeforeW Orientation)

![Renders 4D](images/renders4Dp3f.png?raw=true)

* 2D slices look fine, but this lattice rotation is most intended for texturing 3D objects with an additional time variable.

### 4D Noise (Classic Orientation)

![Renders 4D](images/renders4Dc.png?raw=true)

* OpenSimplex2F has the most noticeable diagonal artifacts, followed by Old OpenSimplex.

### 4D Noise (Torus Mapping)

![Renders 4D](images/renders4Dtorus.png?raw=true)

* Seamless tileable 2D noise from 4D, mapped using noise4(r sin x, r cos x, r sin y, r cos y)

## Public Domain Dedication

This is free and unencumbered software released into the public domain. See UNLICENSE. To the best of my non-lawyer knowledge, no patent claims cover anything implemented here (not legal advice). Please use this software to make cool things, rather than to make patents! Enjoy.
