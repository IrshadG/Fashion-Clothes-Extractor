# Fashion-Clothes-Extractor
Identify upper and lower clothes from social media images

## About the project
Current fashion detection models aren't very useful for commercial or specific purposes. In this project, I'm working on getting info about fashion attributes like color, style and categories from social media pictures (I've already downloaded images from a few popular Instagram handles). I'm using various models from places like Hugging Face and GitHub, tweaking a few as needed. All these models use transformer-based machine learning architecture. It's an ongoing project, and I've already learned a bunch from it.

## Process
#### 1. Human Detection [detr-ResNet-50]
This model returns bounding box for each human in the image. The model detects very well, but it also detects some humans I don't need like humans with - only head, half body or too small to identify effectively.
![Human Detection](media/DetectHumans.png?raw=true)

#### 2. Image Processing
I filter out images that contain humans that are too close to camera, only head seen and half/cropped body. I do this by checking if the bounding box's proportions match to the proportions of an ideal image containing full body of a human. 
The image below show which bounding boxes are accepted and which are rejected.
![Filter images](media/DetectHumansPreprocessed.png?raw=true)

#### 3. Crop and Resize
From each bounding box, an image cropped from the original image. The images then rescaled to 256x256 pixels 
![Crop and Resize](media/CroppedHumans.png?raw=true)

#### 4. Detect Upper and Lower Clothes [segformer-b2-clothes]
This model segments the cropped images into upper and lower clothes. The segment is converted to bounding box and cropped.

<p float="left">
  Cropped Upper Clothes:
  <img src="media/Upper-Full Clothes.png?raw=true" width="600"/>
<p/>

  
<p float="left">
  Cropped Lower Clothes:
  <img src="media/LowerClothes.png?raw=true" width="200"/> 
<p/>

## What next?
#### Image Tagging
I'm working on finetuning classification models that can accurately identify the colors, categories, style, pattern and sub-category of each upper and lower clothes images.  

## Difficulties faced
### 1. Filtering Images
There was quite some trial and error to set the right proportions for upper and lower limit to filter bounding boxes.    

### 2. Segmenting Upper and Lower Clothes
It was difficult to find either model that could perform well or a dataset on which a model could be finetuned. Another finetuned model will be soon replaced with existing model that is far more accurate than current model.

### 3. Tagging Images
The biggest challege I am facing while training this model is the dataset. Since I reqyuire specific classes for classification, I have to create the dataset myself. Creating and filtering such large dataset can be very time consuming. 

## Acknowledgment
Models infered/finetuned from [HuggingFace](https://huggingface.co/)

Finetuning model from [Fashion-CLIP](https://github.com/patrickjohncyh/fashion-clip)

Thanks to [Nazim Girach](https://github.com/ulfimlg) for contributing to this project
