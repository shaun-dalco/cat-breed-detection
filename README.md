## Introduction

It can be difficult for people to determine the breed of a cat, most people cannot name any breed at all. This application aims to address this issue and make it easier for someone without any knowledge of cat breeds to accurate determine if it is a Siamese, Abyssinian or Bengal. If someone was to find a lost cat, being able to determine its breed could aid in its successful return to its owner. If someone is looking to purchase a cat, and they come across and ad online, this application could be used to determine the cats breed and/or to verify if the seller is correctly listing the cat under the right breed.

## Data preparation

Images were gathered from google using a python script to download 80 images per category, and an online image downloader was used to collect images from duckduckgo and bing. In total the data set consisted of 441 images. 37 images were used for testing and 404 images were used for training data. Each image fell under 3 categories, Siamese, Abyssinian or Bengal.

Each of the images pixels across all 3 colour channels were normalised, this was an important step to improve the rate of convergence of the network and thus reduced the time training consumed. To do this, the pixel values were divided by 255; the maximum pixel brightness for a particular colour channel. This ensured that input parameters had a similar data distribution, and importantly values that are much closer together than the original 0 to 255 distribution. 

## Model design

![alt text](https://github.com/shaun-dalco/cat-breed-detection/blob/main/modeldesign.png?raw=true)


This model was motivated by LeNet, specifically its application in leaf disease detection, which was rather effective in determining leaf disease. This simple algorithm was adjusted for use in cat breed detection. The above model architecture was one of three that were deemed most successful. It was observed that this model obtained ~92% accuracy on the test set, however by adjusting the number of layers (dense) and introducing the input layer a second time before flattening, a ~98% accuracy was achieved. A wide array of other models were attempted, varying the pool size of each layer, the padding on each layer, and the layer output shape, to varying success. The number of layers were also experimented with.

Pool size seemed to effect the model’s performance with sizes outside the range of (2,2) to (6,6) giving inaccurate results. The size of each layers was experimented most heavily, and it was found that working with powers of 2 as the sizes yielded higher accuracy than powers of 10. The exception to this was one node which it was found to be effective to use 196, however other nearby values could have been used without it being detrimental to the models performance. The third model cnn3, was the best model, this was both because of its inference speed, and because of its high accuracy (98%).

This model could be used to detect cat breeds, however since it can only distinguish between 3 breeds, it is quite limited in scope. It would require more training data between more breeds to create a commercial product, nevertheless this model still has applications amongst cat hobbyists, and could be used by advertises’ to prevent scams (ie people from trying to sell the wrong breed of cat for financial gain).


## Post-analysis

The main advantage of this model is its high accuracy of 98%, and its subsequent ability to distinguish between the three examined cat breeds. This model does this better than most people, unfamiliar with cat breeds, do. Because of this the model has the potential to be used by advertises, by individuals, by cat show hosts, and by cat breeders. The main drawback in this model is that it only extends to three specific breeds of cats, any future iteration of this project that aims to be turned into a commercial product must necessarily address this limitation by including a variety of other breeds in this model’s training data, and ideally should be further experimented with to find ideal layer sizes, pool sizes that are suitable for the new data set.

Another approach that could have been used was different model architectures for the different colour layers and combining these layers when flattened. This may have provided additional benefits however it was not examined.

Another approach which definitely should have been used was image augmentation and dimensionality reduction. Image augmentation is the application of some transformation to the underlying image data set that allows for more training data and in particular a view of images that was not provided in the original data set. Dimensionality reduction would include the reduction of the colour channels to one grey-scale channel, the advantage of this is the data sets simplicity and the lack of colour interference in any pattern that might exist. Using grey-scale images with their own model architectures, in conjunction with the original model architectures and then flattening their outputs may have provided some boost in accuracy, however this was also not examined. It could be that the use of colour images are not as appropriate as using grey-scale images in this application.

The most plausible way to improve this models accuracy was merely to include more images in its training data, either by collecting images with a camera, from google or other search engines or from social media. Image augmentation should have also been used in conjunction with a larger image data set.