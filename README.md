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

## code
# Mobius strip modeling and computation
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D
from scipy.integrate import simps

class MobiusStrip:
    def __init__(self, R=1.0, w=0.2, n=200):
        self.R = R
        self.w = w
        self.n = n
        self.u = np.linspace(0, 2 * np.pi, n)
        self.v = np.linspace(-w / 2, w / 2, n)
        self.U, self.V = np.meshgrid(self.u, self.v)
        self.x, self.y, self.z = self._generate_mesh()

    def _generate_mesh(self):
        U, V = self.U, self.V
        x = (self.R + V * np.cos(U / 2)) * np.cos(U)
        y = (self.R + V * np.cos(U / 2)) * np.sin(U)
        z = V * np.sin(U / 2)
        return x, y, z

    def surface_area(self):
        # Use numerical approximation with cross product of partial derivatives
        du = 2 * np.pi / self.n
        dv = self.w / self.n

        Xu = np.gradient(self.x, axis=1) / du
        Yu = np.gradient(self.y, axis=1) / du
        Zu = np.gradient(self.z, axis=1) / du

        Xv = np.gradient(self.x, axis=0) / dv
        Yv = np.gradient(self.y, axis=0) / dv
        Zv = np.gradient(self.z, axis=0) / dv

        cross = np.sqrt(
            (Yu * Zv - Zu * Yv) ** 2 +
            (Zu * Xv - Xu * Zv) ** 2 +
            (Xu * Yv - Yu * Xv) ** 2
        )

        area = np.sum(cross) * du * dv
        return area

    def edge_length(self):
        # Compute the length of the edge curve at v = +w/2 and v = -w/2
        edge1_x = (self.R + self.w/2 * np.cos(self.u / 2)) * np.cos(self.u)
        edge1_y = (self.R + self.w/2 * np.cos(self.u / 2)) * np.sin(self.u)
        edge1_z = self.w/2 * np.sin(self.u / 2)

        dx = np.gradient(edge1_x)
        dy = np.gradient(edge1_y)
        dz = np.gradient(edge1_z)

        length1 = np.sum(np.sqrt(dx**2 + dy**2 + dz**2)) * (2 * np.pi / self.n)

        # For Mobius strip, both edges are same due to twist — only one loop
        return length1

    def plot(self):
        fig = plt.figure(figsize=(8, 6))
        ax = fig.add_subplot(111, projection='3d')
        ax.plot_surface(self.x, self.y, self.z, cmap='viridis', edgecolor='k', linewidth=0.2)
        ax.set_title('Mobius Strip')
        plt.show()

# Example usage
if __name__ == '__main__':
    strip = MobiusStrip(R=1.0, w=0.4, n=300)
    print(f"Surface Area: {strip.surface_area():.4f}")
    print(f"Edge Length: {strip.edge_length():.4f}")
    strip.plot()
