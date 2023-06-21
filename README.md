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
1. Run the notebook [**fine_tune.ipynb**](urlcolb). 
    * **NOTE**: the dependencies are installed in the first cell of the notebook.

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
