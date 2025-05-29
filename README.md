# Mobius Strip Modeling and Analysis

This Python project models a Möbius strip using parametric equations and numerically computes its geometric properties such as surface area and edge length. The project also includes a 3D visualization of the strip.

## Features
- Generates a 3D mesh of the Möbius strip surface based on user-defined radius, width, and resolution
- Numerical approximation of the surface area using trapezoidal integration
- Numerical calculation of the edge length along the Möbius strip boundary
- 3D plot visualization with interactive rotation using `matplotlib`

## How It Works
The Mobius strip is modeled using the parametric equations:

\[
\begin{cases}
x(u,v) = (R + v \cdot \cos \frac{u}{2}) \cdot \cos u \\
y(u,v) = (R + v \cdot \cos \frac{u}{2}) \cdot \sin u \\
z(u,v) = v \cdot \sin \frac{u}{2}
\end{cases}
\]

where \(u \in [0, 2\pi]\) and \(v \in \left[-\frac{w}{2}, \frac{w}{2}\right]\).

The surface area is approximated by numerically integrating the surface element using partial derivatives, while the edge length is calculated by summing distances along the strip’s boundary.

## Installation and Usage

1. Clone the repository:
   ```bash
   git clone https://github.com/tarakreddy07/mobius-strip.git
   cd mobius-strip
