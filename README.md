# Image Caption Generator

<br>
* This is implementation of a image caption generator from [Yumi's Blog](https://fairyonice.github.io/Develop_an_image_captioning_deep_learning_model_using_Flickr_8K_data.html). which generates a caption based on the things that are present in the image. Image captioning is a challenging task where computer vision and natural language processing both play a part to generate captions. This technology can be used in many new fields like helping visually impaired, medical image analysis, geospatial image analysis etc.

<br>

## Model Architecture

- **Encoder**: Inception V3
  - Pretrained on ImageNet for image feature extraction.
  - Outputs a feature vector for each image.
- **Decoder**: LSTM Network
  - Takes the feature vector as input.
  - Generates a sequence of words to form a caption.

![](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*uGb3yU-GwxSUu5K9zCsHKA.png)

<br>

## Dataset:
[FLICKR_8K](https://forms.illinois.edu/sec/1713398).
This dataset includes around 1500 images along with 5 different captions written by different people for each image. The images are all contained together while caption text file has captions along with the image number appended to it. The zip file is approximately over 1 GB in size.

![](https://raw.githubusercontent.com/MiteshPuthran/Image-Caption-Generator/master/images/dataset.PNG)
<br>

## Steps to follow:


### 1. Adding start and end sequence to the captions
Start and end sequence need to be added to the captions because the captions vary in length for each image and the model has to understand the start and the end.

### 2. Extracting features from images
* After dealing with the captions we then go ahead with processing the images. For this we make use of the pre-trained Inception V3 model.
* Instead of using this pre-trained model for image classification as it was intended to be used. We just use it for extracting the features from the images. In order to do that we need to get rid of the last output layer from the model.

![](https://miro.medium.com/v2/resize:fit:850/0*Cfb_UEgyOSsiQSL_.png)
<br>

### 3. Building the LSTM model

![](https://raw.githubusercontent.com/MiteshPuthran/Image-Caption-Generator/master/images/lstm.PNG)
<br>
LSTM model is been used beacuse it takes into consideration the state of the previous cell's output and the present cell's input for the current output. This is useful while generating the captions for the images.<br>
The step involves building the LSTM model with two or three input layers and one output layer where the captions are generated. The model can be trained with various number of nodes and layers. We start with 256 and try out with 512 and 1024. Various hyperparameters are used to tune the model to generate acceptable captions

<br>

### 4. Predicting on the test dataset
After the model is trained, it is tested on test dataset to see how it performs on caption generation for just 5 images. If the captions are acceptable then captions are generated for the whole test data. 

## Conclusion
Implementing the model is a time consuming task as it involved lot of testing with different hyperparameters to generate better captions. The model generates good captions for the provided image but it can always be improved.
<br>

### Training Loss
![](https://github.com/Coolsheru2526/Image-Caption-Generator/blob/main/outputs/Tensorboard.png?raw=true)

<br>

### Captions
![](https://github.com/Coolsheru2526/Image-Caption-Generator/blob/main/outputs/test1.jpg?raw=true)
![](https://github.com/Coolsheru2526/Image-Caption-Generator/blob/main/outputs/test2.jpg?raw=true)
![](https://github.com/Coolsheru2526/Image-Caption-Generator/blob/main/outputs/test3.jpg?raw=true)
![](https://github.com/Coolsheru2526/Image-Caption-Generator/blob/main/outputs/test4.jpg?raw=true)
![](https://github.com/Coolsheru2526/Image-Caption-Generator/blob/main/outputs/test5.jpg?raw=true)


