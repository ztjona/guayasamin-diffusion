# scopic-diffusion
Project to fine tune Stable diffusion with images from Ecuadorian artist Oswaldo Gauyasamín. 

In this repo are included the auxiliar jupyter notebooks and configuration files used for the project.

# Generating dataset
The images of the dataset are scraped using BS4 and captioned using BLIP. 
The dataset is published and published 

## Instructions
Run the following notebooks in order:
1. **scraping_OG.ipynb**: scraps and downloads the images of the artist in folder *./images/* 
1. **captioning_images.ipynb**: uses BLIP to generate captions for the artist paintings. 
1. **publishing_dataset.ipynb**: publishes the dataset **ztjona/oswaldo-guayasamin-blip-captions-v2** in Hugging Face.


# Fine tune
The training is done in Google Colab PRO using a A100 GPU.
1. Change the configurations in the local *art-ecu.yaml* file. 
1. Run the notebook [**fine_tune.ipynb**](https://drive.google.com/file/d/1r1z8Ckqq4W9U0Wg0PcWGB_ri4DavpkCQ/view?usp=sharing). 
    * **NOTE**: the dependencies are installed in the first cell of the notebook.

## Changes in configuration file
The configuration file used as template was **pokemon.yaml**. The changes made are:
```yaml
# ...
# line 9
timesteps: 11 # Scopic-Diffusion: reduce to 1 epoch
```

```yaml
# ...
#line 74
batch_size: 3 # Scopic-Diffusion: reduced to avoid memory GPU run out
    num_workers: 4
    num_val_workers: 0 # Avoid a weird val dataloader issue
    train:
      target: ldm.data.simple.hf_dataset
      params:
        name: ztjona/oswaldo-guayasamin-blip-captions-v2 # Scopic-Diffusion: pointing to our dataset
        image_transforms:
        - target: torchvision.transforms.Resize
          params:
            size: 512
            interpolation: 3
        - target: torchvision.transforms.RandomCrop
          params:
            size: 512
        - target: torchvision.transforms.RandomHorizontalFlip
    validation:
      target: ldm.data.simple.TextOnly
      params:
        captions:
        - "A woman with fire in her hands" # Scopic-Diffusion: changing validation prompt
        - " Painting of clouds over a city" # Scopic-Diffusion: changing validation prompt
        - "Yoda"
        - "An epic landscape photo of a mountain"
        output_size: 512
```

# Model description 
* Evaluation metric: 
* Model complexity: 


# Installation
```
### Download the code
git clone https://github.com/ztjona/scopic-diffusion.git
cd scopic-diffusion

pip install -r requirements.txt
````

Execute each notebook in the order preivously described.
