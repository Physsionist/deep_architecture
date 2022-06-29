# Deep Architects

> Authors: Mitch Veele, Richard Aw, Wolfgang Herwald

Using deep learning to identify the architectural styles of buildings.


## Introduction

Reach out. What do you see?

<img src="README_images/luke_rey_training.avif" width="500" height="300"> <img src="README_images/Cristo_Rey_Church.jpeg" width="500" height="300">

<!-- (<a href="https://www.mouseplanet.com/gallery/v/PersonalContributions/toddking/lastjedi/star-wars-last-jedi-luke-trains-rey-reach-out-rolls-eyes.jpg.html">Image Source</a>) -->

<!-- (<a href="https://sah-archipedia.org/buildings/NM-01-049-0178">Image Source</a>) -->

The *uncultured* response: a church.

(A *better* response: God.)

Jokes aside, the picture on the right shows the Cristo Rey Church, a Roman Catholic church in Santa Fe, New Mexico. Besides being potentially the largest building made of [adobe](https://en.wikipedia.org/wiki/Adobe) in the United States, it was also designed in the Pueblo Revival style –– an architectural style that draws inspiration from New Mexico's historic Spanish missions. In fact, this church is just one of many buildings in Santa Fe designed in the Pueblo Revival style, paying homage to the city's Pueblo and Spanish roots. 

This, hopefully, illustrates why knowing the architectural style of a building is valuable. Architecture exists not just to create the physical environment in which people live, but also reflect the cultural heritage of a place. The architectural style of a building can often give us a glimpse of the rich history of a place. (On the practical side of things, having such knowledge could impress your date too!)

> "An architect once told me: When you learn about ancient cultures, the first thing people point to is their architecture, because it’s so expressive of who they were. The example they used was ancient Egypt. Take a look at the pyramids and the Sphinx, and you’ll get a good idea of how they regarded their rulers, their religion, and the qualities of the land that they drew their building materials from. The towering feats of delicate, narrative stone masonry that made up Gothic architecture, emerging in Europe in the Middle Ages, was a perfect counterpoint to its age of reverence verging on fear of divinity, during a period of grim instability. The Industrial Revolution, which re-organized the world along rational standards of machine production, inevitably birthed Modernism, which used mass-produced steel and glass to replicate this emerging order in cities. All revolutions, especially political ones, turn to architecture immediately to create their most prominent monuments. And this ability of architecture to explain its age happens whether a building is an elaborate showpiece or a banal standby." (<a href="https://studyarchitecture.com/blog/architecture-news/why-architecture-is-important/"> Source</a>)


### Goal

Develop a multi-class convolutional neural network (CNN) model that can identify the architectural style of a building, if given an image of said building.


## Methodology


### Dataset

We used 10,113 images from 25 architectural styles

It is a mixed between images scraped from Google Images and the dataset from the paper "Architectural Style Classification using Multinomial Latent Logistic Regression" (ECCV2014), made by Zhe Xu.
(<a href="https://www.kaggle.com/datasets/dumitrux/architectural-styles-dataset"> Source</a>)


### Model

ResNet-18

> Lightweight

Data Augmentation (image flipping)

Cyclic Learning Rate

> Changing the learning rate periodically for stochastic gradient descent can improve performance while also cutting down on training time. 


## Results

It worked.

### Accuracy vs epoch count

*Insert graph here*

### Training Loss vs epoch count

*Insert graph here*


## Conclusion

Identifying the architectural style of a building is a fun and meaningful activity. We should develop a Pokemon Go equivalent for it!


<!-- **Requirements**
It must contain a nice notebook walking through the code of your project
Any code/scripts/models written/developed for the project
Slides for your presentation
A ReadMe that is 1) neat 2) clearly explains the project, the goal, and the outcome 3) has at least one visualization/picture of some kind
All of these things must be easy to find in the GitHub from the ReadMe -->
