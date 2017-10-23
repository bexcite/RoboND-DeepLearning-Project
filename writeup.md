## Project: Follow Me

[//]: # (Image References)

[network_fancy]: ./results/network_fancy.png
[network]: ./results/network.png
[train_val_loss]: ./results/train_val_loss.png
[example_1]: ./results/example_1.png
[example_2]: ./results/example_2.png
[example_3]: ./results/example_3.png

## [Rubric](https://review.udacity.com/#!/rubrics/1155/view) Points
### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a write-up / README document including all rubric items addressed in a clear and concise manner. The document can be submitted either in either Markdown or a PDF format.

You're reading it! (yep thats left from template from one of the previous projects:)

#### 2. The write-up conveys the an understanding of the network architecture.

Network architecture used for the task employs 3 encoder layers with separable convolutions and batch normalization, 1x1 convolution to essentially learn segments with preserving spacial information and 3 decoder layer with bilinear upsampling and skip layers to relevant encoder layers. See figure below for details.

![Network][network_fancy]

And text summary for `model.summary()`:

![Network text][network]

1x1 convolution used instead of fully connected layers in order to preserve the spatial information. They are also useful for connecting already trained classifier like VGG of ResNet to the decoder layer and fine tune network for the segmentation task. Though, we don't use the fine tuning here and use the architecture to learn end-to-end segmentation task.

Batch Normalization helps network automatically determines the scaling and shifting of the input data and these parameters are learning together with all weights.

Separable Convolutions decouple spatial and depth convolutions and greatly decreases the number of parameters in 5-8 times compared to standard convolutions. This helps to train network faster and what's more important to faster execute them on smaller embedded computing platforms usually used in robotics.

Skip layers important to add more information to the network after upsampling operation which is lossy and reduce the information about original picture. With skip layers network is able to learn finer details about shapes which we needed for our segmentation task. In other words skip layers are adding spatial resolution to our decoder.


#### 3. The write-up conveys the student's understanding of the parameters chosen for the the neural network.

Network was trained using the parameters:

```
learning_rate = 0.0005
batch_size = 20
num_epochs = 40
steps_per_epoch = 250
```

After experimentation with various params we've found that smaller batch size works better and it's in the range that often used in papers for the task pf segmentation.

Learning rate used `0.0005` which is smaller than usually used `0.005` or `0.001` because we used bigger number of epochs (on Nvidia GTX 1080 Ti) and the final score with lower learning rate and bigger number of epochs was better.

Steps per epoch was increased to `250` in order to cover all images in training set. Though it's slightly bigger than needed but it wasn't a problem for network to learn correctly.

Loss and Validation loss graph are below. Loss decrease is almost flattened but still is lowering a bit in 5-10 epochs.

![Train Validation Loss][train_val_loss]

Example of predictions on validation images:

![Example 1][example_1]
![Example 2][example_2]
![Example 3][example_3]

**Final Score: 41.34%**

#### 4. The student has a clear understanding and is able to identify the use of various techniques and concepts in network layers indicated by the write-up.

1 by 1 convolutions described in network architecture part above and we use them to learn important features in images without loosing spatial information.

**Update, after a review:** 1 by 1 convolutions can be use to reduce dimensionality, like  a layer 20x20x128 on convolution with 64 filters of 1x1 would result in size 20x20x64. 1x1 convolution is often followed by activation layer which is acting like feature pooling transformations that preserves coordinate space, it's different than just sum pooling layers. Also 1x1 convolutions has much less number of parameters than fully connected layers in case we want to learn reduced feature representation vector of our image.

Fully connected layers are not used here because they usually common in classification task where spatial information are not so important.

#### 5. The student has a clear understanding of image manipulation in the context of the project indicated by the write-up.

For training and inferencing we used 160x160x3 images in RGB encoding. It's always important to have color encoding in train vs inference pipeline. Before inference in `follower.py` we also resizing images to the expected 128x128x3. Theoretically network can work with bigger images but we've not tested such setup.

**Update, after a review:**

The set of convolutional encoders are used to learn distinctive feature maps from the image. It's gradually reduces the spatial dimension of the input. Later some of the encoded layers are used in decoder via skip connections to add more spatial resolution to learned feature vectors during the image recovery.

The role of the decoder is to map the low resolution encoder feature maps to full input resolution feature maps for pixel-wise classification.

#### 6. The student displays a solid understanding of the limitations to the neural network with the given data chosen for various follow-me scenarios which are conveyed in the write-up.

Such network architecture definitely can be used for any object detection but we need to train it on correctly prepared data (labeled images with the correct ground truth).

Current network result could be further approved by adding more data for specific cases and using data augmentation like flipping and/or shifting.
