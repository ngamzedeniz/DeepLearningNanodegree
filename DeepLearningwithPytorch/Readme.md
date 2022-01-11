# Part 1
- Part 1 includes Building tensors with Pytorch
- Highlighted methods for this part:
1. features = torch.randn((1, 5)) #creates a tensor with shape (1, 5)
2. weights = torch.randn_like(features) #creates another tensor with the same shape as features
3. matrix multiplication of the features and the weights. For this we can use torch.mm() or torch.matmul()
4. weights.view(a, b) will return a new tensor with the same data as weights with size (a, b)


![image](https://user-images.githubusercontent.com/92583544/148942189-d77abcf8-04d9-4145-994f-a34f41efe668.png)

![image](https://user-images.githubusercontent.com/92583544/148942080-f803e46a-64d5-4034-b2bf-b4702ee470ff.png)


# Part 2
- Part 2 includes Build a simple network using weight matrices and matrix multiplications with Pytorch for MNIST Data
![image](https://user-images.githubusercontent.com/92583544/148943656-e6431b8a-3261-467e-9cd6-e01e5af930d6.png)

- Highlighted methods for this part:
1. PyTorch has a nice module nn that provides a nice way to efficiently build large neural networks.
2. Get MNIST dataset through the torchvision package
3.  created the trainloader with a batch size of 64, and shuffle=True. The batch size is the number of images we get in one iteration from the data loader and pass through our network, often called a batch. 
And shuffle=True tells it to shuffle the dataset every time we start going through the data loader again. 
4. The networks you've seen so far are called fully-connected or dense networks. Each unit in one layer is connected to each unit in the next layer. 
In fully-connected networks, the input to each layer must be a one-dimensional vector (which can be stacked into a 2D tensor as a batch of multiple examples). 
However, our images are 28x28 2D tensors, so we need to convert them into 1D vectors. 
Thinking about sizes, we need to convert the batch of images with shape (64, 1, 28, 28) to a have a shape of (64, 784), 784 is 28 times 28. 
This is typically called flattening, we flattened the 2D images into 1D vectors.
5. Previously you built a network with one output unit. Here we need 10 output units, one for each digit. We want our network to predict the digit shown in an image, so what we'll do is calculate probabilities that the image is of any one digit or class. This ends up being a discrete probability distribution over the classes (digits) that tells us the most likely class for the image. That means we need 10 output units for the 10 classes (digits). We'll see how to convert the network output into a probability distribution next.
6. Exercise: Flatten the batch of images images. Then build a multi-layer network with 784 input units, 256 hidden units, and 10 output units using random tensors for the weights and biases. For now, use a sigmoid activation for the hidden layer. Leave the output layer without an activation, we'll add one that gives us a probability distribution next.

![image](https://user-images.githubusercontent.com/92583544/148944753-9f788ac9-3557-4fd6-9787-93c23b91956a.png)

![image](https://user-images.githubusercontent.com/92583544/148944865-8d6eb237-45f5-4c67-ba76-d9018d7fb673.png)

7. ![image](https://user-images.githubusercontent.com/92583544/148945091-fa0ef543-05c7-4033-8f61-a776234dfed6.png)

Solution: 

![image](https://user-images.githubusercontent.com/92583544/148945186-9e2bb0d8-7ac9-4d41-9457-e9d0ccacced2.png)

8. 
![image](https://user-images.githubusercontent.com/92583544/148945386-84881ac5-ebff-4b7b-b101-723703421ba8.png)

9. PyTorch provides a convenient way to build networks like this where a tensor is passed sequentially through operations, nn.Sequential

# Part 3 

- Part 3 includes Training Neural Network, Building Backpropagation, Using Loss Funtions
- Highlighted methods for this part:
1. Calculate loss function:

![image](https://user-images.githubusercontent.com/92583544/148946014-1e35b86a-2b55-4262-b0b8-04fbb4890807.png)

2. Building Backpropagation for Gradient Descent:

![image](https://user-images.githubusercontent.com/92583544/148946149-66a5be86-5df5-4602-883f-21acd4c4dcd5.png)

3. Losses in Pytorch: PyTorch provides losses such as the cross-entropy loss (nn.CrossEntropyLoss)
4. When we create a network with PyTorch, all of the parameters are initialized with requires_grad = True. This means that when we calculate the loss and call loss.backward(), the gradients for the parameters are calculated. These gradients are used to update the weights with gradient descent. Below you can see an example of calculating the gradients using a backwards pass.
5. Training the Network : There's one last piece we need to start training, an optimizer that we'll use to update the weights with the gradients. We get these from PyTorch's optim package. For example we can use stochastic gradient descent with optim.SGD.
6. Now we know how to use all the individual parts so it's time to see how they work together. Let's consider just one learning step before looping through all the data. The general process with PyTorch:

Make a forward pass through the network

Use the network output to calculate the loss

Perform a backward pass through the network with loss.backward() to calculate the gradients

Take a step with the optimizer to update the weights

7. Training for real: 

Now we'll put this algorithm into a loop so we can go through all the images. Some nomenclature, one pass through the entire dataset is called an epoch. So here we're going to loop through trainloader to get our training batches. For each batch, we'll doing a training pass where we calculate the loss, do a backwards pass, and update the weights.


# Part 4
- Part 4 includes build and train a neural network. You'll be using the Fashion-MNIST dataset
- Highlighted methods for this part:
1.  Remember the training pass is a fairly straightforward process:

Make a forward pass through the network to get the logits

Use the logits to calculate the loss

Perform a backward pass through the network with loss.backward() to calculate the gradients

Take a step with the optimizer to update the weights

Now you should create your network and train it. First you'll want to define the criterion ( something like nn.CrossEntropyLoss) and the optimizer (typically optim.SGD or optim.Adam).


2.   

![image](https://user-images.githubusercontent.com/92583544/148947603-18ee72c5-bcd1-4fc5-a141-1cc75d882678.png)


# Part 5 
- Part 5 includes Inference and Validation
- Inference is a term that refers to a trained network that is ready for making predictions 
- Highlighted methods for this part:
1. Trained model can fail on unseen data, while its pretty good on trained data, this is called overfitting and in order to i. measure and ii. avoid overfitting:
   1. Validation set is used to measure the performance of the data which is does not exist on trained data
   2. Regularization such as dropout is used to avoid overfitting while monitoring the validation performance during training, Adding dropout in PyTorch is straightforward using the nn.Dropout module.
2. During training we want to use dropout to prevent overfitting, but during inference we want to use the entire network. So, we need to turn off dropout during validation, testing, and whenever we're using the network to make predictions. To do this, you use model.eval(). This sets the model to evaluation mode where the dropout probability is 0. You can turn dropout back on by setting the model to train mode with model.train(). 

![image](https://user-images.githubusercontent.com/92583544/148950774-f1587c02-04a5-42f8-8012-bbfffdb22b54.png)


# Part 6 
- Part 6 includes how to save trained model 
- In general, you won't want to train a model everytime you need it. Instead, you'll train once, save it, then load the model when you want to train more or use if for inference





