# food-taste
a set of triplets (A, B, C) representing human annotations: the human annotator judged that the taste of dish A is more similar to the taste of dish B than to the taste of dish C


for each triplet (A, B, C) in test_triplets.txt you should predict 0 or 1 as follows:

-if the dish in image A.jpg is closer in taste to the dish in image B.jpg than to the dish in C.jpg

-if the dish in image A.jpg is closer in taste to the dish in image C.jpg than to the dish in B.jpg

We concatenate the true training triplet with a "false triplet", in which we invert the position of B and C, so that we can build a bigger training set. We use part of our training set as our validation set to avoid overfittinng. Since our pretrained model densenet121, requires the input to be 224x224 images, so we use the data_transform to match the normalization. We choose in the end dennsnet 121. We use LeakyReLu in the model as our activation function to achieve better performance and use and use BCEWithLogistisLoss as our loss function.

Possible solution for task3

For each image, get the last layer embedding of a ResNet-50 pretrained on ImageNet (available in Keras), by making sure that the images are scaled and normalized properly. Formulate the problem as binary classification: for each triplet in the training data, create 2 training samples: first, concatenate the three embeddings according to the order in the triplet, and associate label 1; then swap the last two embeddings, concatenate again, and associate label 0. On this data, fit a 2-layer fully-connected net. Note: prone to overfitting, use high dropout rate and early stopping, monitored on a properly chosen validation set. Training time: less than 60 mins on a Dual-Core CPU (including generation of embeddings). Possible improvements on the hard baseline: use image augmentations, use other (even multiple) pretrained nets.

