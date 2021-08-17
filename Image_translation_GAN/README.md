# Satillite to Google Maps Image translation using GANs

<p align="center">
  <img width="460" height="300" src="https://github.com/abhishikthsagar/Projects/blob/main/Image_translation_GAN/Images/2.jpg">
</p>


### Introduction

The GAN architecture is comprised of a generator model for outputting new plausible synthetic images, and a discriminator model that classifies images as real (from the dataset) or fake (generated). The discriminator model is updated directly, whereas the generator model is updated via the discriminator model. As such, the two models are trained simultaneously in an adversarial process where the generator seeks to better fool the discriminator and the discriminator seeks to better identify the counterfeit images.

Pix2Pix is a Generative Adversarial Network, or GAN, model designed for general purpose image-to-image translation. It is a type of conditional GAN where the generation of the output image is conditional on an input, in our case, the satillite image. 

Pix2Pix was preesented in the 2016 paper titled "[Image to Image translation with Conditional Adversarial Networks](https://arxiv.org/abs/1611.07004)". Please check it out for further reading.

