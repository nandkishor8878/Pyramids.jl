# Pyramids

A pyramid representation library for Julia. Parts are loosely based on [MatlabPyrTools](http://www.cns.nyu.edu/lcv/software.php), by NYU's Laboratory for Computer Vision.

## Project Status

[![Build Status](https://travis-ci.org/loganwilliams/Pyramids.jl.svg?branch=master)](https://travis-ci.org/loganwilliams/Pyramids.jl)

## Documentation

### Installation

Pyramids is not yet a registered Julia package. To install it, run the following in Julia:

    Pkg.clone("https://github.com/loganwilliams/Pyramids.jl.git")
    using Pyramids

### Usage

The Pyramids library is used through the `ImagePyramid` class. To create a new `ImagePyramid`, there a several constructors that may be used of the form `ImagePyramid(im::Image, t::PyramidType)`.

Subtypes of `PyramidType` include:
 * `GaussianPyramid`
 * `LaplacianPyramid`
 * `ComplexSteerablePyramid`

Additional parameters include the scale, maximum number of levels, number of orientation bands, and minimum level size, as applicable. For a complete listing, view the source code.

Below is an example of loading an image and converting it to an `ImagePyramid`.

    using Images, Pyramids

    im = load("test_im.png")
    pyramid = ImagePyramid(im, ComplexSteerablePyramid(), scale=0.75, max_levels=23)

An `ImagePyramid` may also be created directly from an `Array`.

To manipulate an `ImagePyramid`, the `subband` and `update_subband` functions may be used.

    hi_residual = subband(pyramid, 0)
    pyramid_inverted_hi = update_subband(pyramid, 0, -hi_residual)

`update_subband` also has a mutating variant, `update_subband!`.

To convert an `ImagePyramid` back to its original image representation, the `toimage` function may be used.

    image_inverted_hi = toimage(pyramid_inverted_hi)

### Further examples

The `examples/` directory provides a further example of using Pyramids to implement "Phase-Based Frame Interpolation for Video," by Meyer et. al., from CVPR 2015. [1]

[1] https://www.disneyresearch.com/publication/phasebased/
