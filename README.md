# Spacecraft Recovery Simulator

A real-time 3D interactive spacecraft recovery simulation built with **C++** and **OpenGL (FreeGLUT)**.

In the simulator, the player pilots a salvage drone through space to locate damaged spacecraft components, inspect and repair them, align them with the docking platform, and reconstruct a complete spacecraft. Once all components are successfully recovered and assembled, the completed spacecraft launches into deep space.

The project combines interactive 3D graphics, spatial transformations, depth-aware rendering, clipping and scissoring, camera systems, particle effects, and gameplay state management into a single simulation.

---

## Features

* **3D Salvage Drone Navigation** — Fly freely through the environment using forward/backward movement, strafing, vertical movement, and yaw controls.
* **Spacecraft Component Recovery** — Locate damaged components, approach them, and attach them to the salvage drone.
* **Component Inspection & Repair** — Use the repair scanner to zoom into a carried component, inspect its condition, and repair it.
* **3D Component Alignment** — Rotate recovered components along the pitch, yaw, and roll axes to match their required docking orientation.
* **Dynamic Magnetic Snapping** — Components automatically align with their target orientation when sufficiently close to the required angle.
* **Space Station Docking** — Secure correctly aligned components to their designated docking positions.
* **Multi-Stage Mission Flow** — Progress through recovery, scanning, repair, alignment, docking, and final spacecraft assembly.
* **Multiple Camera Views** — Switch between third-person, top-down, and cockpit perspectives.
* **Sensor Viewport** — Display a secondary scanner/radar view using a separate viewport and scissor region.
* **Depth Testing** — Toggle the OpenGL depth buffer to observe the effect of depth-aware rendering.
* **Dynamic Clipping** — Adjust the scanner's far clipping distance during runtime.
* **Particle Effects** — Includes animated thruster flames and repair particle effects.
* **Final Spacecraft Assembly** — Once all components are recovered, a structural hull connects the components to form the completed spacecraft.
* **Launch Sequence** — The fully assembled spacecraft performs an animated launch sequence.

---

## Mission Flow

The recovery mission consists of six main stages:

### 1. Locate & Pick Up

Pilot the salvage drone through the 3D environment and maneuver close to a damaged spacecraft component. Once within the required range, the component can be picked up and attached to the drone.

### 2. Scan Debris

Activate the sensor viewport to inspect the surrounding environment and monitor component information and alignment indicators.

### 3. Inspect & Repair

Activate the repair scanner while carrying a component. The view zooms into the component for detailed inspection. Repair effects are displayed when the component is successfully restored.

### 4. Align Orientation

Rotate the recovered component along its three rotational axes until it matches the required docking orientation.

### 5. Dock & Lock

Move the correctly oriented component toward its designated docking position. When the component is sufficiently close to the required orientation, the magnetic snapping system assists with final alignment. Press `Enter` to secure the component to the station.

### 6. Assemble & Launch

After all five components have been successfully docked, the simulator constructs the connecting spacecraft hull and completes the spacecraft assembly. The engines then ignite and the completed spacecraft launches into deep space.

---

## Graphics Techniques

The simulator demonstrates several fundamental 3D computer graphics techniques through interactive gameplay.

| Graphics Technique        | Application                                                                                                                    |
| :------------------------ | :----------------------------------------------------------------------------------------------------------------------------- |
| **3D Translation**        | Controls salvage drone movement and positions objects within the 3D environment using `glTranslatef`.                          |
| **3D Rotation**           | Controls component orientation around the pitch, yaw, and roll axes using `glRotatef`.                                         |
| **3D Scaling**            | Used by the repair scanner to zoom into components using `glScalef`.                                                           |
| **Z-Buffering**           | Provides depth-aware rendering using OpenGL's `GL_DEPTH_TEST` functionality.                                                   |
| **Clipping & Scissoring** | Used to create the secondary sensor viewport with `glViewport` and `glScissor`, together with configurable clipping distances. |

### Interactive Graphics Demonstrations

The simulator also provides runtime controls for observing some of these graphics techniques directly:

* Toggle depth testing to observe the effect of the Z-buffer.
* Adjust the sensor viewport's far clipping distance.
* Switch between different camera perspectives.
* Observe scaling during the repair scanner sequence.
* Interactively manipulate component rotations during the docking process.

---

## Controls

### Drone Flight

| Key       | Action                        |
| :-------- | :---------------------------- |
| `W` / `S` | Move forward / backward       |
| `A` / `D` | Strafe left / right           |
| `Q` / `E` | Ascend / descend              |
| `J` / `L` | Rotate drone yaw left / right |

### Component Rotation

| Key       | Action                 |
| :-------- | :--------------------- |
| `↑` / `↓` | Rotate component pitch |
| `←` / `→` | Rotate component yaw   |
| `U` / `O` | Rotate component roll  |

### Recovery, Scanning & Repair

| Key        | Action                                 |
| :--------- | :------------------------------------- |
| `Spacebar` | Pick up / drop an adjacent component   |
| `C`        | Toggle the sensor viewport             |
| `R`        | Inspect / repair the carried component |
| `Enter`    | Dock and attach the aligned component  |

### Camera & Graphics Debugging

| Key        | Action                                 |
| :--------- | :------------------------------------- |
| `V`        | Switch camera view                     |
| `Z` / `F1` | Toggle Z-buffer depth testing          |
| `[` / `F2` | Decrease scanner far clipping distance |
| `]` / `F3` | Increase scanner far clipping distance |

### Camera Views

Press `V` to cycle through:

1. Third-person view
2. Top-down view
3. Cockpit view

---

## Visual & Design Details

### Color-Coded Components

Different spacecraft components use distinct visual identities to make them easier to recognize during the recovery mission:

* **Damaged components** — Red
* **Cockpit** — Blue dome
* **Fuel tank** — Glowing green
* **Engine** — Orange rings
* **Cargo module** — Yellow

### Completed Spacecraft

The final spacecraft includes a custom structural chassis connecting the recovered components, along with:

* Panel lines
* Warning stripes
* Tail stabilizers
* Wing pylons
* Registration marking (`SSV-07`)
* Animated navigation and approach lights

### Particle Effects

The simulator includes animated particle effects for:

* **Thruster jets** — Dynamic flames that respond to drone movement.
* **Repair effects** — Particle bursts displayed during successful component repairs.

### HUD & Interface

The cockpit interface provides real-time information and indicators related to the recovery mission, including component status, alignment information, and graphics-system states.

---

## Technologies

* **C++**
* **OpenGL**
* **FreeGLUT**
* **GLU**
* **MinGW / g++**
* **Mermaid** — Mission-flow documentation

---

## Project Structure

The project separates the implementations of the major graphics techniques into dedicated source files:

```text
.
├── main.cpp
├── structures.h
├── translation.cpp / translation.h
├── rotation.cpp / rotation.h
├── scaling.cpp / scaling.h
├── zbuffer.cpp / zbuffer.h
├── clipping.cpp / clipping.h
└── src/
    ├── input.cpp / input.h
    ├── models.cpp / models.h
    └── environment.cpp / environment.h
```

The exact project structure may vary depending on the current source and asset organization.

---

## Building and Running

### Prerequisites

A C++ compiler and the required OpenGL/FreeGLUT libraries are required.

For Windows, the project can be built using:

* **MinGW / g++**
* **FreeGLUT**
* **OpenGL**
* **GLU**

### Compilation

Open PowerShell or Command Prompt in the project directory and compile the source files:

```bash
g++ main.cpp translation.cpp rotation.cpp scaling.cpp zbuffer.cpp clipping.cpp src/input.cpp src/models.cpp src/environment.cpp -o SpacecraftRecoverySimulator -lfreeglut -lopengl32 -lglu32
```

### Running

After successful compilation, run:

```bash
./SpacecraftRecoverySimulator.exe
```

> **Note:** The exact build command may need to be adjusted depending on the installed FreeGLUT/OpenGL libraries and the final project structure.

---

## Objective

The objective of the simulator is to recover all damaged spacecraft components and successfully reconstruct the spacecraft.

A successful mission requires the player to:

1. Locate the damaged components.
2. Pick up each component.
3. Scan and inspect the components.
4. Repair damaged components.
5. Correctly align their orientations.
6. Dock each component at the space station.
7. Complete the spacecraft assembly.
8. Launch the reconstructed spacecraft.


