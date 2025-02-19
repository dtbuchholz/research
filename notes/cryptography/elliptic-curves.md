# Elliptic curves

## Introduction

An elliptic curve is a smooth, continuous curve defined by an equation in the form:

$$
y^2 = x^3 + ax + b
$$

where $a$ and $b$ are constants, and the curve satisfies certain conditions (notably that it has no
"cusps" or "self-intersections").

### Key properties

1. **Symmetry**: The curve is symmetric about the x-axis

   - For any point $(x,y)$ on the curve, $(x,-y)$ is also on the curve
   - This is clear from the equation: if $y^2 = x^3 + ax + b$, then $(-y)^2 = x^3 + ax + b$

2. **Non-Singularity**: The curve must be "smooth" everywhere

   - Mathematically: $4a^3 + 27b^2 \neq 0$
   - This ensures there are no "cusps" or "self-intersections"

3. **Point at Infinity**: The curve has a special point called the "point at infinity" (∞)
   - This point can be thought of as being "at the top and bottom" of the curve
   - It serves as the identity element for the group operation

### Visual examples

Different values of $a$ and $b$ give different shapes. Here are some notable cases:

1. $y^2 = x^3 - x$ ($a = -1, b = 0$)

   - Creates a curve with two separate parts

2. $y^2 = x^3 - x + 1$ ($a = -1, b = 1$)

   - Creates a single continuous curve

3. $y^2 = x^3$ ($a = 0, b = 0$)
   - This is singular (has a cusp) and thus not a valid elliptic curve!

## Why are they important?

Elliptic curves are crucial in cryptography because:

1. They form a mathematical group (we'll explore this next)
2. Operations on them are relatively easy to compute in one direction but very hard to reverse
3. They can achieve the same security level as RSA with much smaller key sizes
