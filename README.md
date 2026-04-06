# 2D_to_3D_Converter

A fast and efficient 3D object reconstruction model that converts 2D single images into high-quality 3D models.

## Features

- **Fast inference**: Processes images in seconds on CPU
- **High quality**: Generates detailed 3D meshes from single images
- **Easy to use**: Simple command-line interface and optional web UI
- **Flexible output**: Supports OBJ and GLB formats with optional texture baking

## Installation

### Prerequisites
- Python >= 3.8
- PyTorch (CPU or CUDA compatible)

### Setup

1. Clone the repository:
```bash
git clone https://github.com/yourusername/2D_to_3D_Converter.git
cd 2D_to_3D_Converter
```

2. Create a virtual environment:
```bash
python -m venv .venv
.venv\Scripts\Activate.ps1  # Windows
source .venv/bin/activate   # Linux/Mac
```

3. Install dependencies:
```bash
pip install --upgrade setuptools
pip install -r requirements.txt
```

## Usage

### Command Line

Process a single image:
```bash
python run.py path/to/image.png --output-dir output --device cpu
```

Process multiple images:
```bash
python run.py img1.png img2.jpg img3.jpeg --output-dir output --device cpu
```

### Options

- `--device`: Device to use (e.g., 'cuda:0' for GPU, 'cpu' for CPU). Default: 'cuda:0'
- `--no-remove-bg`: Skip automatic background removal (image should have clean gray background)
- `--foreground-ratio`: Ratio of foreground to image size. Default: 0.85
- `--output-dir`: Output directory for results. Default: 'output/'
- `--model-save-format`: Format for mesh (obj or glb). Default: 'obj'
- `--bake-texture`: Bake texture atlas instead of using vertex colors
- `--texture-resolution`: Texture resolution in pixels. Default: 2048
- `--render`: Generate NeRF-rendered video
- `--chunk-size`: Evaluation chunk size for GPU. Smaller = less VRAM. Default: 8192
- `--mc-resolution`: Marching cubes grid resolution. Default: 256

### Web Interface (Optional)

```bash
python gradio_app.py
```

Then open the local URL in your browser (usually http://127.0.0.1:7860).

## Output

Results are saved in the output directory with the following structure:
```
output/
├── 0/
│   ├── mesh.obj          # 3D mesh
│   └── input.png         # Processed input (if bg removed)
├── 1/
│   └── ...
```

## Performance

- CPU inference: ~2-3 minutes per image (depends on resolution)
- GPU inference: ~30-60 seconds per image
- Default configuration uses ~6GB VRAM

## License

This project uses the TripoSR model. See LICENSE file for details.

## Acknowledgments

- Model architecture based on [Large Reconstruction Model (LRM)](https://yiconghong.me/LRM/)
- Built using PyTorch, transformers, and modern deep learning techniques
