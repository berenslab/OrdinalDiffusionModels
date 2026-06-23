
# Ordinal Diffusion Models for Fundus Images

This repository contains the code for  "Ordinal Diffusion Models for Fundus Images". 

![Ordinal Diffusion Models](image/ov.png)



## Installation
Set up a python environment with a python version 3.11. Then, download the repository, activate the environment and install all other dependencies with

```bash
cd OrdinalDiffusionModels
pip install -e .
```

## Model Weights
Model weights can be downloaded using the download_model_weights.py script. 

```bash
python download_model_weights.py --model xx
```
where xx is the model variant to be downloaded:
- baseline w/o structure:     xx = base
- baseline w/ structure:      xx = basestruct
- equidistant w/o structure:  xx = equi
- equidistant w/ structure:   xx = equistruct
- learned w/o structure:      xx = learn
- learned w/ structure:       xx = learnstruct
- all models:                 xx = all

Zenodo URL: https://zenodo.org/records/18781460

## Quick Start for Generating New Images
For generating new images, download the model weights and run:
```bash
python generate_images.py --model xx --num_images_per_class 100 --out_dir out/
```
where xx is as above and out_dir the directory where the images are saved.

## Training the Diffusion Model
To train a diffusion model, configure the training parameters in `configs/diffusion.yaml`. The key options are:
- **Model type**  
  - `equi: True` → train the equidistant model  
  - `learned: True` → train the learned model  
- **Structural information**  
  - `structure: True` → include structural information  
  - `structure: False` → exclude structural information  

After updating the configuration file, start training by running the training script:

```bash
python train_diffusion.py --config configs/diffusion.yaml
```

## Project Structure

```
configs/
└──contains config.yaml for all model training.
src/ori/
├── models/          # Model architectures
├── data/            # Data loading and preprocessing
├── metrics/         # Evaluation metrics
├── xx_training.py   # Training wrapper for different models
├── criterion.py     # Loss functions
├── optimizers.py    # Optimizer
└── utils.py         # Helper functions
evaluation.py       # For classifying generated images
generate_images.py  # Generate images
calculate_fid.py    # Calculate FID
sample.py           # Sample Class
xx_train.py         # Training script for each model
```
