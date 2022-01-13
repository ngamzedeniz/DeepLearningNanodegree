# Generative Advesarial Network 

- Define and train a DCGAN on a dataset of faces
- Data:  using the CelebFaces Attributes Dataset (CelebA) to train adversarial networks.
- Creating a DataLoader
- Pre-process image data and scale it to a pixel range of -1 to 1
- Define the model for discriminator
  - The inputs to the discriminator are 32x32x3 tensor images
  - The output should be a single value that will indicate whether a given image is real or fake
- Define the model for generator
  - The inputs to the generator are vectors of some length z_size
  - The output should be a image of shape 32x32x3
- Initialize the weights of networks
  - To help your models converge, you should initialize the weights of the convolutional and linear layers in your model. From reading the original DCGAN paper, they say:
     - All weights were initialized from a zero-centered Normal distribution with standard deviation 0.02.
- Build complete network
  - Define models' hyperparameters and instantiate the discriminator and generator from the classes defined above. 
- Discriminator and Generator Losses
  - Now we need to calculate the losses for both types of adversarial networks.
  - Discriminator Losses
    - For the discriminator, the total loss is the sum of the losses for real and fake images, d_loss = d_real_loss + d_fake_loss.
    - Remember that we want the discriminator to output 1 for real images and 0 for fake images, so we need to set up the losses to reflect that.
  - Generator Loss
    - The generator loss will look similar only with flipped labels. The generator's goal is to get the discriminator to think its generated images are real.
 - Define optimizers for Discriminator (D) and Generator (G)
 - Training
   - Training will involve alternating between training the discriminator and the generator. You'll use your functions real_loss and fake_loss to help you calculate the discriminator losses.
     - You should train the discriminator by alternating on real and fake images
     - Then the generator, which tries to trick the discriminator and should have an opposing loss function
- Training loss
  - Plot the training losses for the generator and discriminator, recorded after each epoch.
- Generator samples from training

  ![image](https://user-images.githubusercontent.com/92583544/149327107-c7bf1942-5648-4f84-9c01-7d40343cb907.png)
