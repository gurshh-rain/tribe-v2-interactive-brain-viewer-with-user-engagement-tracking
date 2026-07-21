# TRIBE v2 Interactive Brain Viewer

An interactive 3D extension of Meta's [TRIBE v2](https://github.com/facebookresearch/tribev2) demo notebook. Instead of static brain-response snapshots, this notebook renders a rotatable, zoomable 3D cortical surface (fsaverage5) that animates through predicted activity over time — synced with the source video and spoken-word captions.

## What this does

TRIBE v2 predicts fMRI-like brain responses to naturalistic video, audio, and text stimuli. This notebook takes the model's raw output (`preds`, shape `n_timesteps x n_vertices`) and builds a Plotly-based viewer with:

- **3D rotate/zoom** of the fsaverage5 pial surface (left + right hemispheres)
- **Fire colormap** matching TRIBE v2's own `PlotBrain(cmap="fire")` style
- **Synced video playback** alongside the brain, frame-matched to each timestep
- **Live captions** pulled from the model's events dataframe, showing spoken words as they occur
- **Play/Pause + slider** controls to scrub through time manually or animate automatically

## Requirements

- Access to `facebook/tribev2` and gated `meta-llama/Llama-3.2-*` weights on Hugging Face (request access + accept license, then set `HF_TOKEN`)
- GPU strongly recommended (Colab, local CUDA machine, etc.)
- Python 3.12

Install dependencies:

```bash
uv pip install "tribev2[plotting] @ git+https://github.com/facebookresearch/tribev2.git"
pip install plotly nilearn moviepy
```

> **Known issue:** if you hit `OSError: ... torchaudio/lib/_torchaudio.abi3.so: undefined symbol: aoti_torch_abi_version`, this is a torch/torchaudio version mismatch. Reinstall matching versions, e.g.:
> ```bash
> pip uninstall -y torch torchaudio torchvision
> pip install torch==2.5.1 torchaudio==2.5.1 torchvision==0.20.1 --index-url https://download.pytorch.org/whl/cu121
> ```

## Usage

1. Open `tribe_demo.ipynb`
2. Run the setup and model-loading cells
3. Run a prediction cell (video or text) to populate `preds`, `df`, and `video_path`
4. Run the interactive viewer cell — the 3D brain will render inline with rotate/zoom controls and a time slider

## Credits

Built on top of the official [TRIBE v2](https://github.com/facebookresearch/tribev2) demo by Meta / FAIR (d'Ascoli et al., 2026). This repo only adds the interactive 3D visualization layer; all model weights, architecture, and core inference code belong to the original authors.

## License

Follows the licensing terms of the upstream [tribev2](https://github.com/facebookresearch/tribev2) repository. Check there for details before redistributing model weights or derived outputs.
