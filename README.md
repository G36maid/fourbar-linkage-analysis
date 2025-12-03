# Four-Bar Linkage Analysis

[![Deploy to GitHub Pages](https://github.com/YOUR_USERNAME/fourbar-linkage-analysis/actions/workflows/deploy.yml/badge.svg)](https://github.com/YOUR_USERNAME/fourbar-linkage-analysis/actions/workflows/deploy.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Rust](https://img.shields.io/badge/rust-1.70%2B-orange.svg)](https://www.rust-lang.org/)
[![Python](https://img.shields.io/badge/python-3.13%2B-blue.svg)](https://www.python.org/)

A comprehensive implementation of four-bar linkage mechanism analysis using Newton-Raphson numerical methods. Features both an **interactive Rust GUI simulator** for real-time visualization and **Python scripts** for generating publication-quality figures.

> 🚀 **[Try the Live Demo](https://YOUR_USERNAME.github.io/fourbar-linkage-analysis/)** - No installation required!

![Four-Bar Linkage](figures/figure_combined_positions.png)

## 🎯 Project Overview

This project provides **three ways** to experience four-bar linkage analysis:

1. 🌐 **[Web Version (WASM)](https://YOUR_USERNAME.github.io/fourbar-linkage-analysis/)** - Run in your browser, no installation!
2. 💻 **Rust GUI Simulator** (`src/`) - Native desktop app for maximum performance
3. 📊 **Python Analysis Scripts** (`pyscript/`) - Generate publication-quality figures

### Key Features

- ✨ **Real-time Interactive Simulation** - Adjust parameters and see results instantly
- 🔢 **Newton-Raphson Solver** - Fast, accurate position analysis
- 📊 **Publication-Quality Figures** - Generate plots for academic reports
- 🎨 **Coupler Curve Tracing** - Visualize mechanism paths
- 🔍 **Grashof Analysis** - Automatic mechanism type classification
- 🎓 **Educational Focus** - Designed for mechanism analysis courses

## 🚀 Quick Start

### Option 1: Try Online (Easiest) 🌐

**No installation needed!** Just open in your browser:

👉 **[https://YOUR_USERNAME.github.io/fourbar-linkage-analysis/](https://YOUR_USERNAME.github.io/fourbar-linkage-analysis/)**

Works on any device with a modern browser (Chrome, Firefox, Safari, Edge).

### Option 2: Run Native Desktop App 💻

For best performance, run the native version:

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/fourbar-linkage-analysis.git
cd fourbar-linkage-analysis

# Run the Rust GUI simulator
./run.sh

# Or manually with cargo
cargo run --release
```

### Option 3: Generate Report Figures (Python) 📊

```bash
# Generate static figures for reports
./run.sh python

# Figures will be saved to ./figures/
```

**Comparison:**

| Feature | Web Version | Native App | Python Scripts |
|---------|-------------|------------|----------------|
| Installation | ❌ None | ✅ Rust/Cargo | ✅ Python/uv |
| Performance | ⚡ Good | ⚡⚡ Excellent | N/A |
| Accessibility | 🌍 Anywhere | 💻 Local only | 💻 Local only |
| Sharing | ✅ URL | ❌ | ❌ |
| Best for | Demos, teaching | Development | Report figures |

## 📁 Project Structure

```
fourbar-linkage-analysis/
├── src/                          # Rust source code
│   ├── main.rs                   # GUI application (egui)
│   └── fourbar.rs                # Core Newton-Raphson solver
├── pyscript/                     # Python analysis scripts
│   ├── generate_figures.py       # Figure generation for reports
│   └── README.md                 # Python scripts documentation
├── docs/                         # Documentation
│   └── REPORT.md                 # Technical report (Chinese)
├── figures/                      # Generated plots and figures
│   ├── figure_a_position_analysis.png
│   ├── figure_b_convergence.png
│   └── figure_combined_positions.png
├── Cargo.toml                    # Rust dependencies
├── pyproject.toml                # Python dependencies (uv)
├── run.sh                        # Unified run script
├── LICENSE                       # MIT License
└── README.md                     # This file
```

## 🛠️ Installation & Requirements

### For Rust Simulator

**Prerequisites:**
- Rust toolchain (1.70+)
- Cargo (comes with Rust)

**Install Rust:**
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

### For Python Scripts

**Prerequisites:**
- Python 3.13+
- [uv](https://github.com/astral-sh/uv) - Fast Python package manager

**Install uv:**
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

## 📖 Usage Guide

### Interactive Rust Simulator

The Rust GUI provides real-time control over all mechanism parameters:

**Controls:**
- **θ₂ Slider**: Control input crank angle (0° - 360°)
- **Link Length Sliders**: Adjust r₁, r₂, r₃, r₄ in real-time
- **Auto Play**: Enable automatic rotation animation
- **Animation Speed**: Control rotation speed (0.5 - 10.0 °/frame)
- **Show Trace**: Display coupler curve path (orange line)
- **Show Grid**: Toggle coordinate grid
- **Show Angles**: Display angle labels on mechanism

**Building:**
```bash
# Development mode (faster compilation)
cargo run

# Release mode (optimized, recommended)
cargo run --release

# Build without running
cargo build --release
```

**Binary location:** `./target/release/four_bar_sim`

### Python Figure Generation

Generate static figures for academic reports:

```bash
# Using the run script
./run.sh python

# Or manually with uv
uv run pyscript/generate_figures.py
```

**Output:** Three PNG files in `figures/` directory (300 DPI, publication-ready)

### Run Script Commands

```bash
./run.sh            # Run Rust GUI (default)
./run.sh python     # Generate Python figures
./run.sh build      # Build Rust in release mode
./run.sh dev        # Run Rust in dev mode
./run.sh test       # Run Rust tests
./run.sh clean      # Clean all build artifacts
./run.sh help       # Show help message
```

## 🔬 Technical Details

### Newton-Raphson Method

The solver uses Newton-Raphson iteration to solve the vector loop equations:

**Vector Loop Closure:**
```
r₂ + r₃ - r₄ - r₁ = 0
```

**Projection Equations:**
```
f₁(θ₃, θ₄) = r₂cos(θ₂) + r₃cos(θ₃) - r₄cos(θ₄) - r₁ = 0
f₂(θ₃, θ₄) = r₂sin(θ₂) + r₃sin(θ₃) - r₄sin(θ₄) = 0
```

**Jacobian Matrix:**
```
J = [ -r₃sin(θ₃)   r₄sin(θ₄) ]
    [  r₃cos(θ₃)  -r₄cos(θ₄) ]
```

**Update Rule:**
```
[Δθ₃]       [f₁]
[Δθ₄] = -J⁻¹[f₂]

θ₃ⁿᵉʷ = θ₃ᵒˡᵈ + Δθ₃
θ₄ⁿᵉʷ = θ₄ᵒˡᵈ + Δθ₄
```

**Convergence:**
- Tolerance: 1e-9
- Max iterations: 100
- Typical convergence: 5-15 iterations
- Initial guess: Analytical solution or previous state

### Default Mechanism Parameters

```
r₁ = 6.0  (Ground link)
r₂ = 2.0  (Input crank)
r₃ = 5.0  (Coupler link)
r₄ = 5.0  (Output rocker)

Mechanism Type: Crank-Rocker
Grashof Condition: Satisfied (S + L ≤ P + Q)
```

### Implementation Features

**Rust Implementation:**
- Real-time position solving (< 0.1ms per solve)
- Immediate-mode GUI with egui
- 60 FPS rendering
- Smooth animation with automatic initial guess tracking
- Singularity detection and error handling

**Python Implementation:**
- Batch processing for full rotation cycles
- High-quality figure generation (matplotlib)
- Convergence analysis visualization
- Validation reference for Rust code

## 📊 Generated Figures

### Figure A: Position Analysis
![Position Analysis](figures/figure_a_position_analysis.png)

Shows θ₃ and θ₄ angles throughout a complete input rotation (0° - 360°).

### Figure B: Convergence Analysis
![Convergence](figures/figure_b_convergence.png)

Demonstrates Newton-Raphson convergence characteristics at θ₂ = 45°.

### Figure C: Combined Positions
![Combined](figures/figure_combined_positions.png)

Overlay of both output angles for comparison.

## 🧪 Testing

Run the Rust test suite:

```bash
cargo test

# With output
cargo test -- --nocapture

# Specific test
cargo test test_full_rotation
```

## 📚 Documentation

- **Technical Report**: [docs/REPORT.md](docs/REPORT.md) - Detailed analysis in Chinese
- **Python Scripts**: [pyscript/README.md](pyscript/README.md) - Figure generation guide
- **Code Documentation**: Inline comments and doc comments in source files

## 🎓 Educational Context

This project was developed for the **Mechanisms** course at:
- **National Taiwan Normal University (NTNU)**
- **Department of Mechatronic Engineering**

### Learning Objectives

1. **Position Analysis**: Understanding linkage kinematics
2. **Numerical Methods**: Newton-Raphson convergence behavior
3. **Mechanism Design**: Grashof condition and configuration types
4. **Path Generation**: Coupler curves and synthesis
5. **Software Engineering**: Rust/Python integration, GUI design

## 🐛 Known Issues & Limitations

- **Singularities**: Solver may fail at extreme configurations (det(J) ≈ 0)
- **Configuration Jumping**: Trace may jump if mechanism passes through dead point
- **Position Only**: No velocity or acceleration analysis (future enhancement)
- **2D Only**: No 3D visualization option

## 🔮 Future Enhancements

- [ ] Velocity and acceleration analysis
- [ ] Force/torque analysis
- [ ] Multiple mechanism presets
- [ ] Animation export (video/GIF)
- [ ] 3D visualization mode
- [ ] Synthesis tools (path/function generation)
- [x] ~~Web version (WASM compilation)~~ ✅ **Completed!**
- [ ] Mechanism comparison tools
- [ ] Save/load mechanism configurations (JSON)
- [ ] Share mechanism via URL parameters

## 🌐 Deployment

This project is automatically deployed to GitHub Pages using GitHub Actions.

**Live Demo:** [https://YOUR_USERNAME.github.io/fourbar-linkage-analysis/](https://YOUR_USERNAME.github.io/fourbar-linkage-analysis/)

See [docs/DEPLOYMENT.md](docs/DEPLOYMENT.md) for detailed deployment instructions.

### Local WASM Development

```bash
# Install trunk
cargo install trunk

# Add WASM target
rustup target add wasm32-unknown-unknown

# Serve locally with hot reload
trunk serve --open

# Build for production
trunk build --release
```

## 🤝 Contributing

Contributions are welcome! Areas for improvement:

- Performance optimization
- Additional analysis features
- Better visualization options
- Documentation improvements
- Bug fixes
- Mobile UI/UX enhancements

## 📄 License

MIT License - See [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **Norton, R. L.** - *Design of Machinery* textbook
- **NTNU Mechanisms Course** - Educational foundation
- **egui community** - Excellent GUI framework
- **Rust community** - Language and tooling support

## 📞 Contact & Support

For questions, issues, or suggestions:
- Open an issue on the repository
- Refer to course materials and documentation
- Check the technical report for detailed analysis

## 📚 References

1. Norton, R. L. (2019). *Design of Machinery*. McGraw-Hill Education.
2. Course Lecture Notes: Ch4-Ch5 - Linkage Analysis Methods
3. [Four-bar linkage - Wikipedia](https://en.wikipedia.org/wiki/Four-bar_linkage)
4. [Newton-Raphson Method](https://en.wikipedia.org/wiki/Newton%27s_method)
5. [Grashof Condition](https://en.wikipedia.org/wiki/Grashof_condition)
6. [egui Documentation](https://docs.rs/egui/)

---


*Last Updated: December 2025*
