# Stuff Made Easy

A GenAI-powered PCB design tool that converts natural language prompts into manufacturable PCB schematics, netlists, and eventually Gerber files and 3D PCB models.

## Project Vision

Stuff Made Easy aims to democratize PCB design by allowing hobbyists and makers to create electronic circuits without deep technical knowledge. By describing what you want in plain language, our tool generates the necessary technical specifications and files needed for manufacturing.

**Phase 1 Target Audience**: DIY enthusiasts and hobbyists (Arduino/Raspberry Pi users)

### Key Features (Planned)

- Convert natural language descriptions into PCB designs
- Parse design parameters (board size, components, connections)
- Generate schematics using SKiDL
- Output netlists for KiCad and other EDA tools
- Future: Generate Gerber files and 3D models

## Repository Structure

```
stuff-made-easy/
├── data/                # Contains datasets and training files (for future NLP model fine-tuning)
├── docs/                # Documentation (project roadmap, user guides, etc.)
├── src/
│   ├── schematic_generator/
│   │   └── led_circuits.py   # Parse prompts and generate schematics using SKiDL
│   ├── nlp/              # (For future modules: NLP model and fine-tuning scripts)
│   └── ui/               # (For future modules: Web UI using Streamlit/Gradio)
├── tests/               # Unit and integration tests (to be added later)
├── .gitignore           # Detailed ignore file for Python, KiCad backup files, VSCode settings
├── README.md            # This file
└── requirements.txt     # List of required Python packages
```

## Development Environment Setup

### Prerequisites

- Linux Mint (or any Debian-based Linux distribution)
- Python 3.8+ 
- Visual Studio Code
- Git

### Installation Steps

1. **Clone the repository**

```bash
git clone https://github.com/yourusername/stuff-made-easy.git
cd stuff-made-easy
```

2. **Create and activate a Python virtual environment**

```bash
# Create a virtual environment
python -m venv venv

# Activate the virtual environment
source venv/bin/activate
```

3. **Install dependencies**

```bash
pip install -r requirements.txt
```

4. **VSCode Setup**

- Open VSCode
- Install recommended extensions:
  - Python
  - Pylance
  - Git Graph
  - KiCad Schematic Viewer (optional)
- Open the folder containing the repository
- Select the Python interpreter from the virtual environment:
  - Press `Ctrl+Shift+P` and type "Python: Select Interpreter"
  - Choose the interpreter from your virtual environment (venv)

## Running the Code

To test the basic functionality:

```bash
# Make sure you're in the root directory of the project
# and the virtual environment is activated
python -m src.schematic_generator.led_circuits
```

This will:
1. Parse a sample prompt
2. Generate a simple circuit with a battery, resistor, and LED
3. Output a KiCad-compatible netlist file in the `output` directory

### Example Usage

```python
from src.schematic_generator.led_circuits import parse_prompt, generate_schematic

# Parse a natural language description
design_params = parse_prompt("Design a PCB with a 9V battery, LED, and resistor on a 40x20mm board")

# Generate a schematic
netlist_path = generate_schematic(design_params)

print(f"Netlist generated at: {netlist_path}")
```

## KiCad Integration

After generating a netlist:

1. Open KiCad
2. Create a new project or open an existing one
3. In the PCB Editor (PCBnew):
   - Go to File > Import > Netlist
   - Select the generated .net file
   - Click "Import" to add the components to your PCB

## Troubleshooting

### Common Git Issues

#### Non-fast-forward errors

If you get a "non-fast-forward" error when pushing changes:

```bash
# First, ensure all changes are committed
git status
git add .
git commit -m "Your commit message"

# Then fetch and rebase (instead of merge)
git fetch origin
git rebase origin/main

# If there are conflicts, resolve them and continue
git add .
git rebase --continue

# Finally, push your changes
git push origin main
```

#### Other Git Issues

- **Unstaged changes preventing checkout/pull**: Commit or stash your changes before checkout/pull
  ```bash
  git stash
  git checkout branch-name
  git stash pop  # To bring back your changes
  ```

### Python Environment Issues

- **Missing packages**: Ensure your virtual environment is activated before installing packages
  ```bash
  source venv/bin/activate
  pip install -r requirements.txt
  ```

- **ImportError**: Make sure you're running Python from the project root directory
  ```bash
  # Correct way (from project root)
  python -m src.schematic_generator.led_circuits
  
  # Not from inside the source directory
  # This will likely fail with import errors
  ```

### SKiDL Issues

- **Component not found**: SKiDL uses KiCad's component libraries. Ensure KiCad is installed and the component libraries are accessible.
- **Netlist generation errors**: Check the SKiDL documentation or run an Electrical Rules Check (ERC) to identify circuit problems.

## Contributing

1. Create a feature branch (`git checkout -b feature/amazing-feature`)
2. Commit your changes (`git commit -m 'Add some amazing feature'`)
3. Push to the branch (`git push origin feature/amazing-feature`)
4. Open a Pull Request

## Roadmap

- [x] Basic repository structure
- [x] Simple prompt parsing
- [x] Basic schematic generation with SKiDL
- [ ] Improved NLP for prompt understanding
- [ ] Support for more complex circuit topologies
- [ ] Web UI for interactive design
- [ ] Integration with KiCad for PCB layout
- [ ] Gerber file generation
- [ ] 3D model generation

## License

[MIT License](LICENSE)

## Acknowledgments

- SKiDL library for Python-based schematic generation
- KiCad project for EDA components and netlist formats
