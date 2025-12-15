# DLA Simulator

A terminal-based Diffusion-Limited Aggregation (DLA) simulation using high-resolution Braille character rendering.

![Rust](https://img.shields.io/badge/rust-stable-orange)

## What is DLA?

Diffusion-Limited Aggregation is a process where particles undergo random walks and stick to a growing structure upon contact. This creates beautiful fractal patterns similar to:
- Snowflake formation
- Lightning branching
- Mineral dendrites
- Coral growth
- River delta patterns

## Features

- **High-resolution Braille rendering** - Each terminal character displays a 2x4 dot pattern
- **Real-time simulation** - Watch the fractal structure grow
- **Interactive controls** - Adjust parameters while running
- **Multiple seed patterns** - Points, lines, rings, blocks, spokes, scatter/noise blobs and more
- **8 color schemes** - Ice, Fire, Plasma, Viridis, Rainbow, Grayscale, Ocean, Neon
- **Speed control** - Adjust simulation steps per frame
- **Fullscreen mode** - Hide sidebar for maximum canvas size

## Installation

### From GitHub (recommended)

```bash
cargo install --git https://github.com/jo56/dla-simulator
```

### From source

```bash
# Clone the repository
git clone https://github.com/jo56/dla-simulator.git
cd dla-simulator

# Build and run
cargo run --release
```

## Usage

```bash
# Run with defaults
cargo run --release

# Custom parameters
cargo run --release -- --particles 3000 --stickiness 0.5 --seed circle --speed 10
```

### Command Line Options

| Option | Description | Default |
|--------|-------------|---------|
| `-p, --particles` | Number of particles (100-10000) | 5000 |
| `-s, --stickiness` | Adhesion probability (0.1-1.0) | 1.0 |
| `--seed` | Seed pattern (point, line, cross, circle, ring, block, noise, scatter, multipoint, starburst) | point |
| `--speed` | Steps per frame (1-20) | 5 |

## Controls

### Basic Controls

| Key | Action |
|-----|--------|
| `Space` | Pause/Resume simulation |
| `R` | Reset simulation |
| `1-0` | Quick select seed pattern |
| `C` | Cycle color scheme |
| `A` | Toggle color-by-age |
| `Tab` | Next parameter focus |
| `Shift+Tab` | Previous parameter focus |
| `Up/Down` | Adjust focused parameter |
| `+/-` | Adjust speed |
| `V` | Toggle fullscreen |
| `H` or `?` | Show help |
| `Q` | Quit |

### Advanced Controls

| Key | Action |
|-----|--------|
| `M` | Cycle color mode (Age/Distance/Density/Direction) |
| `I` | Invert colors |
| `N` | Cycle neighborhood type (VonNeumann/Moore/Extended) |
| `B` | Cycle boundary behavior (Clamp/Wrap/Bounce/Stick/Absorb) |
| `S` | Cycle spawn mode (Circle/Edges/Corners/Random/Top/Bottom/Left/Right) |
| `W` | Increase walk step size |
| `E` | Decrease walk step size |
| `]` | Increase highlight count (recent particles) |
| `[` | Decrease highlight count |

## Parameters

### Stickiness (0.1 - 1.0)
Controls the probability that a particle will stick when it touches the structure.
- **High stickiness (1.0)**: Dense, compact clusters
- **Low stickiness (0.1-0.3)**: Thin, dendritic branches with more fractal detail

### Seed Patterns
- **Point**: Single center particle - classic DLA growth
- **Line**: Horizontal line - creates symmetrical branching
- **Cross**: Cross pattern - four-way growth
- **Circle**: Ring of particles - inward/outward growth
- **Ring**: Thick rim with hollow core - promotes outside-in branching
- **Block**: Solid square - shows surface roughening instead of long dendrites
- **Multi-Point**: Competing centers to collide and merge
- **Starburst**: Radial spokes tied by a rim for strong anisotropy
- **Noise Patch**: Dense noisy blob offset from center for asymmetric drift
- **Scatter**: Randomized small seeds near center (10-point shortcut seeds above are 1=Point, 2=Line, 3=Cross, 4=Circle, 5=Ring, 6=Block, 7=Multi-Point, 8=Starburst, 9=Noise Patch, 0=Scatter)

## Advanced Settings

### Neighborhood Types (N key)
Controls how many adjacent cells are checked when determining if a particle should stick:
- **Von Neumann (4)**: Only orthogonal neighbors (up/down/left/right). Creates angular, cross-like patterns.
- **Moore (8)**: Orthogonal + diagonal neighbors. The default, produces natural fractal patterns.
- **Extended (24)**: 2-cell radius neighborhood. Creates dense, blob-like growth patterns.

### Spawn Modes (S key)
Determines where new particles originate:
- **Circle**: Classic DLA - particles spawn on a circle around the growing structure
- **Edges**: Particles spawn from all four grid edges
- **Corners**: Particles spawn only from the four corners
- **Random**: Particles spawn at random positions outside the structure
- **Top/Bottom/Left/Right**: Directional spawning from a single edge

### Boundary Behaviors (B key)
What happens when particles reach the grid edges:
- **Clamp**: Particles stop at the edge (default)
- **Wrap**: Particles wrap to the opposite side (toroidal space)
- **Bounce**: Particles reflect off edges
- **Stick**: Particles can stick to the edges themselves
- **Absorb**: Particles are removed and respawned when they hit edges

### Color Modes (M key)
How particles are colored when color-by-age is enabled:
- **Age**: Color based on when the particle stuck (oldest to newest)
- **Distance**: Color based on distance from the center
- **Density**: Color based on local neighbor count when stuck
- **Direction**: Color based on the approach angle when the particle stuck

### Walk Step Size (W/E keys)
Distance particles move per random walk step (0.5-5.0):
- **Larger values**: Faster simulation, coarser/sparser patterns
- **Smaller values**: Slower simulation, finer detail, more dendritic branches

### Highlight Recent ([ ] keys)
Highlights the N most recently stuck particles in white (0-50). Useful for visualizing growth dynamics.

## Dependencies

- [ratatui](https://github.com/ratatui/ratatui) - Terminal UI framework
- [crossterm](https://github.com/crossterm-rs/crossterm) - Cross-platform terminal manipulation
- [rand](https://github.com/rust-random/rand) - Random number generation
- [clap](https://github.com/clap-rs/clap) - Command line argument parsing

## License

MIT
