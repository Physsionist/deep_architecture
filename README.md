# Deep Architects

> Authors: Mitch Veele, Richard Aw, Wolfgang Herwald

Using deep learning to identify the architectural styles of buildings.


## Introduction

Reach out. What do you see?

<img src="README_images/luke_rey_training.avif" width="500" height="300"> <img src="README_images/Cristo_Rey_Church.jpeg" width="500" height="300">

<!-- (<a href="https://www.mouseplanet.com/gallery/v/PersonalContributions/toddking/lastjedi/star-wars-last-jedi-luke-trains-rey-reach-out-rolls-eyes.jpg.html">Image Source</a>) -->

<!-- (<a href="https://sah-archipedia.org/buildings/NM-01-049-0178">Image Source</a>) -->

The *shallow* response: a church.

(A better response: God.)

The *deep* response: a church designed in the **Pueblo Revival style**.

Jokes aside, the picture on the right shows the Cristo Rey Church, a Roman Catholic church in Santa Fe, New Mexico. Besides being potentially the largest building made of [adobe](https://en.wikipedia.org/wiki/Adobe) in the United States, it was also designed in the Pueblo Revival style –– an architectural style that draws inspiration from New Mexico's historic Spanish missions. In fact, this church is just one of many buildings in Santa Fe designed in the Pueblo Revival style, paying homage to the city's Pueblo and Spanish roots. 

This, hopefully, illustrates why knowing the architectural style of a building is valuable. **The architectural style of a building can often give us a glimpse of the rich history and cultural heritage of a place!**

> From a practical perspective, having such knowledge could impress a date too :)

The excerpt below provides a very nice elaboration:

> "An architect once told me: When you learn about ancient cultures, the first thing people point to is their architecture, because it’s so expressive of who they were. The example they used was ancient Egypt. Take a look at the pyramids and the Sphinx, and you’ll get a good idea of how they regarded their rulers, their religion, and the qualities of the land that they drew their building materials from. The towering feats of delicate, narrative stone masonry that made up Gothic architecture, emerging in Europe in the Middle Ages, was a perfect counterpoint to its age of reverence verging on fear of divinity, during a period of grim instability. The Industrial Revolution, which re-organized the world along rational standards of machine production, inevitably birthed Modernism, which used mass-produced steel and glass to replicate this emerging order in cities. All revolutions, especially political ones, turn to architecture immediately to create their most prominent monuments. And this ability of architecture to explain its age happens whether a building is an elaborate showpiece or a banal standby." (<a href="https://studyarchitecture.com/blog/architecture-news/why-architecture-is-important/">Source</a>)


### Goal

Therefore, our team sought to develop a multi-class convolutional neural network (CNN) model that can identify the architectural style of a building, if given an image of said building.


## Methodology


### Dataset

The original source dataset consisted of 10,113 images of buildings from 25 architectural styles (class labels). (<a href="https://www.kaggle.com/datasets/dumitrux/architectural-styles-dataset">Source</a>)

The images were a mix of images scraped from Google Images and the dataset from <a href="https://link.springer.com/chapter/10.1007/978-3-319-10590-1_39"> this paper</a>.

However, we ended up using only a subset of the dataset (limited to 5 architectural styles) because training with all 25 classes seemed to take a very long time and the improvement in the accuracy was too gradual (accuracy was ~ 50% after 5 epochs).


<p align="center">
  <br>
  <img src="README_images/data_snippet.jpg" width="1000" height="300">
  <br><br>
  <em>A snippet of the dataset</em><br><br>
</p>

#### Preprocessing

We basically made two types of modifications to the image data:

1. Scaled all of the images to the same pixel dimensions (256 x 256).

> *Rationale:* To ensure consistency with the typical input dimensions of ResNet.

2. (Data Augmentation) Sythesized more image data by performing vertical/horizontal flips and adding Gaussian noise.

> *Rationale:* This is a regularization technique that can help reduce overfitting when training our model later.


### Model

#### Architecture

We used the ResNet-18 CNN model. 

> *Rationale:* Deeper neural networks are more difficult to train. Residual learning can help ease the training of networks that are substantially deeper than those used previously. In residual learning, the layers in a CNN are reformulated as learning residual functions with reference to the layer inputs, instead of learning unreferenced functions. Empirical evidence suggests that these residual networks are easier to optimize, and can gain accuracy from considerably increased depth. 

#### Initialization

We initialized the parameters of our model in three (or two, really...) ways:

1. Froze *some* layers (all except the last) from a pretrained model

> *Rationale:* This would reduce the training time without losing too much accuracy. (Similar to drop-out, which has been demonstrated to accelerate the training process by not requiring every layer in a neural network to be trained.)

2. Fine-tuned the same pretrained model

> *Rationale:* This would, ostensibly, help tailor the weights of the model more toward the data points in our dataset.

3. Randomly initialize the weights ("train from scratch") 

> *Note:* This approach was eventually abandoned due to the excessive amount of time that passed during training. (Moral of the story: transfer learning *is* key!)


### Training Procedure

The training process involved two noteable "deviations" from the typical training procedure:

1. We used a modified loss function (by weighting classes unequally). 

> *Rationale:* This helps account for the class imbalance present in the dataset.

2. We used a cyclic learning rate.

> *Rationale:* Changing the learning rate periodically for stochastic gradient descent has been shown to improve performance while also cutting down on training time. 


## Results

As the plots below show, our trained model yielded decent values on metrics on the validation data:

### Accuracy vs epoch count

<img src="README_images/model_train_val_accuracy.jpg" width="600" height="300">

The accuracy of the fine-tuned model (~ 85%) is higher than that of the model with partially frozen weights (~ 80%). This is not surprising –– the real question is whether the ~ 5% reduction in accuracy is a worthwhile trade-off.  We say yes considering that the fine-tuned model only seemed to take twice as long to train (~ 6 minutes per epoch vs ~ 3 minutes per epoch).  

Both models achieved fairly high accuracy levels for a small-scale multi-class image classification problem.  In an earlier attempted model with 25 classes, we were only able to achieve 50% accuracy (given the scale our work, we don't see this as a huge negative either).  This suggests that we could potentially achieve even higher accuracy levels if provided more data (and a deeper model, possibly).  


### Loss vs epoch count

<img src="README_images/model_train_val_loss.jpg" width="600" height="300">

The cross-entropy loss values for both models seem to hover around 0.001, which is desirable for a small-scale multi-class image classification problem. Again, this indicates potential for an undertaking on a larger scale.


## Conclusion

We believe that better results could be achieved on the whole dataset (i.e., all 25 architectural styles utilized) with more (training) time and more sophisticated model architectures. Regardless of whether all 25 class labels are used, there are some more ways to extend this project, including:

- Getting more data (i.e., higher sample size)
- Implementing more <a href="https://link.springer.com/chapter/10.1007/978-3-319-10590-1_39">data augmentation techniques</a> (e.g., blurring, translation, etc.)
- Trying different sizes and scales of the images


### The Big Picture

Identifying the architectural style of a building can be a fun and meaningful activity, since it can satisfy our natural curiosity about the past. A possible extension of this project could be to incorporate our trained model into a building architecture discovery application –– similar to other applications such as Pokemon Go (pokemon discovery) and <a href="https://apps.apple.com/us/app/shazam-music-discovery/id284993459"> Shazam</a> (music discovery).
