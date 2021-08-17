# Satillite to Google Maps Image translation using GANs

<p align="center">
  <img width="460" height="300" src="https://github.com/abhishikthsagar/Projects/blob/main/Image_translation_GAN/Images/2.jpg">
</p>


### Introduction

The GAN architecture is comprised of a generator model for outputting new plausible synthetic images, and a discriminator model that classifies images as real (from the dataset) or fake (generated). The discriminator model is updated directly, whereas the generator model is updated via the discriminator model. As such, the two models are trained simultaneously in an adversarial process where the generator seeks to better fool the discriminator and the discriminator seeks to better identify the counterfeit images.

Pix2Pix is a Generative Adversarial Network, or GAN, model designed for general purpose image-to-image translation. It is a type of conditional GAN where the generation of the output image is conditional on an input, in our case, the satillite image. 

Pix2Pix was preesented in the 2016 paper titled "[Image to Image translation with Conditional Adversarial Networks](https://arxiv.org/abs/1611.07004)". Please check it out for further reading.

### Problem Statement

Google Maps has different views, for the same location, which can be switched on the fly. These images are drawn from multiple databases and are highly accurate. This project tries to mimic this functionality by converting satillite photos to Google maps format. The reverse, converting Maps to satillite photos, can be easily achieved by switching the inputs to our model.

### Data

The dataset we will be using is the "**maps**" dataset used in the Pix2Pix paper. This dataset consist of 1097 training images and 1099 validation images. These images are of New York city. The dataset can be downloaded from [here](http://efrosgans.eecs.berkeley.edu/pix2pix/datasets/maps.tar.gz).

The images are in JPEG format with a shape of 1200X600 pixels. Each image contains the satillite image on the left and the Maps image on the right.

<p align="center">
  <img width="460" height="300" src="https://github.com/abhishikthsagar/Projects/blob/main/Image_translation_GAN/Images/195.jpg">
</p>

### Data Preprocessing

The images need to be preprocessed before we use them for Pix2Pix model. We will primarily be using Keras for this project. Each image has to be loaded, rescaled and split into satillite and Maps images.The final output of the preprocessing step is 1097 image pairs with the shape of 256X256 pixels each.

Numpy and Keras are used to load the training data, convert them into numpy arrays, split and resize them. The final preprocessed images are saved as a compressed numpy array. The output of the preprocessing looks like this:

<p align="center">
  <img width="460" height="300" src="https://github.com/abhishikthsagar/Projects/blob/main/Image_translation_GAN/Images/data_load.png">
</p>

### Model Architecture

We will be using the model architecture detailed in the research paper. This model can be used across a range of different image translation tasks. The architecture consists of two models: the discriminator and the generator.

The discriminator is a Convolutional Neural Network that performs image classification. It takes both the satillite image and the Google Maps image as input and predicts the likelihood of whether the target image is real or a fake translation of the source image. The model is optimized using binary cross entropy, and a weighting is used so that updates to the model have half (0.5) the usual effect. The authors of Pix2Pix recommend this weighting of model updates to slow down changes to the discriminator, relative to the generator model during training.

The generator is an encoder-decoder model using a U-net architechture. It takes a satillite image and genrates a Maps image. It does this by first encoding the input image to a bottleneck layer and then decoding to the size of the output image.

The discriminator model is trained directly on real and generated images while the generated model is trained via the discriminator. In simpler words, the genrator tries to fool the discriminator with a generated image while the discriminator tries to discriminate between real and fake images.

Typically, GAN models do not converge; instead, an equilibrium is found between the generator and discriminator models. As such, we cannot easily judge when training should stop. Therefore, we can save the model and use it to generate sample image-to-image translations periodically during training, such as every 10 training epochs. We can then review the generated images at the end of training and use the image quality to choose a final model.

### Training results

After the first 10 epochs, the images look plausible but clearly are not accurate enough. The big landmarks such as rivers and bridges are already being recognised.

<p align="center">
  <img width="460" height="300" src="https://github.com/abhishikthsagar/Projects/blob/main/Image_translation_GAN/Images/plot_010960.png">
</p>

After 60 epochs, the images are starting to get quite similar to each other. Almost all the major streets and blocks are clearly differenciated.

<p align="center">
  <img width="460" height="300" src="https://github.com/abhishikthsagar/Projects/blob/main/Image_translation_GAN/Images/plot_065760.png">
</p>

At the end of 100 epochs, the generated images are startlingly similar to each other. Notice that the minot details like footpaths are still not accurate. This may be resolved by training at a higher resolution or with more data.

<p align="center">
  <img width="460" height="300" src="https://github.com/abhishikthsagar/Projects/blob/main/Image_translation_GAN/Images/plot_109600.png">
</p>

### Translating Images(Testing)

In this case more training epochs does not nessasarily mean better results. It is prefarable to select a model based on human observation of results. For our testing purposes we will chose the final saved model.

Testing the model on some random samples from our dataset shows impressive results. 

<p align="center">
  <img width="200" height="100" src="https://github.com/abhishikthsagar/Projects/blob/main/Image_translation_GAN/Images/Testing.png">
</p>

### Reverse Translation

Using the model to translate Google Maps images to satillite images can be acheived using the same model by just changing the order of the input datasets.

### Conclusion

Using the Pix2Pix GAN model to translate images led to some truly impressive results. We managed to attain higly accurate fake images from the source data. This model can easily repurposed for various image translation tasks.

#### References

(1) https://arxiv.org/abs/1611.07004

(2) https://phillipi.github.io/pix2pix/

(3) https://affinelayer.com/pixsrv/

(4) http://efrosgans.eecs.berkeley.edu/pix2pix/datasets/
