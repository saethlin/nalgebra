# nalgebra

**nalgebra** is a low-dimensional linear algebra library written for Rust targeting:

* general-purpose linear algebra (still lacks a lot of features…).
* real time computer graphics.
* real time computer physics.

An on-line version of this documentation is available [here](http://nalgebra.org).

## Using **nalgebra**
All the functionalities of **nalgebra** are grouped in one place: the root `nalgebra::` module.
This module re-exports everything and includes free functions for all traits methods doing
out-of-place modifications.

* You can import the whole prelude using:

```.ignore
use nalgebra::*;
```

The preferred way to use **nalgebra** is to import types and traits explicitly, and call
free-functions using the `na::` prefix:

```.rust
extern crate "nalgebra" as na;
use na::{Vec3, Rot3, Rotation};

fn main() {
    let     a = Vec3::new(1.0f64, 1.0, 1.0);
    let mut b = Rot3::new(na::zero());

    b.append_rotation(&a);

    assert!(na::approx_eq(&na::rotation(&b), &a));
}
```

## Features
**nalgebra** is meant to be a general-purpose, low-dimensional, linear algebra
library, and keeps an optimized set of tools for computational graphics and
physics. Those features include:

* Vectors with static sizes: `Vec0`, `Vec1`, `Vec2`, `Vec3`, `Vec4`, `Vec5`, `Vec6`.
* Points with static sizes: `Pnt0`, `Pnt1`, `Pnt2`, `Pnt3`, `Pnt4`, `Pnt5`, `Pnt6`.
* Square matrices with static sizes: `Mat1`, `Mat2`, `Mat3`, `Mat4`, `Mat5`, `Mat6 `.
* Rotation matrices: `Rot2`, `Rot3`, `Rot4`.
* Isometries: `Iso2`, `Iso3`, `Iso4`.
* 3D projections for computer graphics: `Persp3`, `PerspMat3`, `Ortho3`, `OrthoMat3`.
* Dynamically sized vector: `DVec`.
* Dynamically sized (square or rectangular) matrix: `DMat`.
* A few methods for data analysis: `Cov`, `Mean`.
* Almost one trait per functionality: useful for generic programming.
* Operator overloading using the double trait dispatch
  [trick](http://smallcultfollowing.com/babysteps/blog/2012/10/04/refining-traits-slash-impls/).
  For example, the following works:

```rust
extern crate "nalgebra" as na;
use na::{Vec3, Mat3};

fn main() {
    let v: Vec3<f64> = na::zero();
    let m: Mat3<f64> = na::one();

    let _ = m * v;      // matrix-vector multiplication.
    let _ = v * m;      // vector-matrix multiplication.
    let _ = m * m;      // matrix-matrix multiplication.
    let _ = v * 2.0f64; // vector-scalar multiplication.
}
```

## Compilation
You will need the last nightly build of the [rust compiler](http://www.rust-lang.org)
and the official package manager: [cargo](https://github.com/rust-lang/cargo).

Simply add the following to your `Cargo.toml` file:

```.ignore
[dependencies.nalgebra]
git = "https://github.com/sebcrozet/nalgebra"
```


## **nalgebra** in use
Here are some projects using **nalgebra**.
Feel free to add your project to this list if you happen to use **nalgebra**!

* [nphysics](https://github.com/sebcrozet/nphysics): a real-time physics engine.
* [ncollide](https://github.com/sebcrozet/ncollide): a collision detection library.
* [kiss3d](https://github.com/sebcrozet/kiss3d): a minimalistic graphics engine.
* [nrays](https://github.com/sebcrozet/nrays): a ray tracer.
