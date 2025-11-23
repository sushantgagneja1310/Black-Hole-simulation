⚫ Kerr Singularity Engine

A high-performance, real-time General Relativistic Ray-Tracer running entirely on the GPU via WebGL. This engine visualizes the spacetime curvature, gravitational lensing, and relativistic optical effects around a rotating (Kerr) black hole.

🚀 Launch Live Simulation

🔭 Scientific Visualization

Unlike standard Schwarzschild simulations (static black holes), this engine implements the Kerr Metric, allowing for the simulation of frame-dragging (the Lense-Thirring effect). It renders a volumetric accretion disk with physically based lighting models including Doppler beaming and gravitational redshift.

Key Features

Kerr Spacetime Geodesics: Simulates light rays bending in the intense gravity well of a rotating singularity.

Frame Dragging: Visualizes how the black hole's spin "drags" spacetime, creating asymmetric lensing and warping the accretion disk.

Relativistic Doppler Beaming: Implements the "headlight effect," where plasma moving towards the observer (near light speed) appears brighter and blue-shifted, while receding plasma is dimmer and red-shifted.

Gravitational Redshift: Light escaping the gravity well loses energy, shifting the accretion disk colors towards the red spectrum near the event horizon.

Volumetric Accretion Disk: A procedural, noise-based plasma simulation that models turbulence, temperature gradients, and variable density.

Photon Ring: Renders the unstable orbit where light circles the black hole multiple times before escaping.

🛠️ Technical Implementation

The simulation is built using Three.js as a scaffold to manage the WebGL context, but the core physics engine is written in GLSL (OpenGL Shading Language) fragment shaders.

The Physics Pipeline (Fragment Shader)

Ray Generation: For every pixel on the screen, a ray is cast from the virtual camera into the scene.

Ray Marching: The ray steps forward through space. At each step, the gravitational influence of the black hole is calculated.

Curvature Calculation: The ray's direction vector is updated based on the geodesic equations for the Kerr metric, factoring in mass ($M$) and angular momentum ($J$).

Intersection Testing:

Event Horizon: If the ray crosses the Schwarzschild radius (modified for spin), it returns black.

Accretion Disk: If the ray passes through the equatorial plane, it samples the volumetric noise buffer to accumulate light/color.

Post-Processing:

ACES Filmic Tone Mapping: Compresses the high-dynamic-range (HDR) light values to displayable colors.

Chromatic Aberration: Simulates relativistic lensing distortion at the fringes.

Bloom: Simulates light scattering in the camera lens.

🧠 Mathematical Foundations

The engine solves for the path of photons in the Kerr geometry. The simulation approximates the geodesic deflection using the effective potential for a spinning mass.

The Kerr Metric (in Boyer-Lindquist coordinates):

$$ds^2 = -\left(1 - \frac{2Mr}{\Sigma}\right) dt^2 - \frac{4Mar\sin^2\theta}{\Sigma} dt d\phi + \frac{\Sigma}{\Delta} dr^2 + \Sigma d\theta^2 + \left(r^2 + a^2 + \frac{2Ma^2r\sin^2\theta}{\Sigma}\right) \sin^2\theta d\phi^2
$$Where:

* $\Delta = r^2 - 2Mr + a^2$
* $\Sigma = r^2 + a^2\cos^2\theta$
* $a = J/M$ (Spin parameter)

The engine explicitly calculates the **Innermost Stable Circular Orbit (ISCO)** to determine the inner edge of the accretion disk:

$$r\_{ISCO} = M \left( 3 + Z\_2 \mp \sqrt{(3-Z\_1)(3+Z\_1+2Z\_2)} \right)
$$\#\#

| Control | Action |
| :--- | :--- |
| **Orbit** | Click & Drag (Mouse) / Touch & Drag (Mobile) |
| **Zoom** | Scroll Wheel |
| **Reset** | Double Click |
| **UI** | Use the floating panel to adjust Mass, Spin, Temperature, and Inclination. |

## ⚡ Performance

The engine includes an **Adaptive Quality** system. It monitors the client's frame rate (FPS) and dynamically adjusts the ray-marching step count and precision. This ensures smooth performance on high-end GPUs while maintaining playability on mobile devices.

-----
