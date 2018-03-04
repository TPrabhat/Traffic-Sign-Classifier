# Traffic-Sign-Classifier
This project consists of implementation of a LeNet architecture to classify 43 different german traffic signs

##Dataset exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library and numpy to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is (34799, 32 , 32, 3)
* The number of unique classes/labels in the data set is 43

#### 2. Include an exploratory visualization of the dataset.

A few of the training images are visualized in the notebook

### Design and Test a Model Architecture

#### 1. Data preprocessing
The following sequence was followed in processing the dataset. The images could be found in the jupyter notebook
* Blur image - using gaussian blurring to generalize the image
* conversion to grayscale - to average teh color channels into one
* gamma correction - to adjust brightness and intensity of the image
* normalization - pixel values to between (-0.5 to 0.5)

#### 2. Data augmentation
in order to make the classifier rotation invariant rotation was used to augment the dataset. The rotation function rotates the function by a specified angle about the center of the image. Two new datasets were created by generating images rotated 5 deg clockwise and anti clockwise. And the original training dataset was concatenated with the rotated images which increased the size of the training dataset by three times

#### 3. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					|
|:---------------------:|:---------------------------------------------:|
| Input         		| 32x32 grayscale image   							|
| Convolution 5x5     	| 1x1 stride, valid padding, outputs 28x28x6 	|
| RELU					|												|
| Avg pooling	      	| 2x2 stride,  outputs 14x14x6 				|
| Convolution 5x5	    | 1x1 stride, valid padding, outputs 10x10x16		|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 5x5x16 				|
| Fully connected		| Input 400, Output 120									|
| RELU					|												|
| Fully connected		| Input 120, Output 84									|
| RELU					|												|
| Fully connected		| Input 84, Output 43									|
| Softmax				|      									|


#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, I used an ADAM optimizer, regularization and dropout. Regularization and dropout increased the training and validation accuracy to a high value.
A dropout of 0.75 was found to be optimum. With a lower value the training accuracy would suffer. Any value higher 0.75 was giving a 100% training accuracy which may indicate overfitting.
Regularization is another technique to avoid overfitting. I chose the regularization constant to be 0.0005 as higher values were clamping training accuracy at around 80% and validation accuracy to lower accuracies.
LeNet is an already well set architecture. But instead of using its max pooling, I tried average pooling. It did not improve or adversely effect the accuracies.

My final model results were:
* training set accuracy of 99%
* validation set accuracy of 96%
* test set accuracy of 94%


### Test a Model on New Images

The 5 images found on the web are displayed in the notebook. The images had to resized to 32x32x3
