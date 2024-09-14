# ds_module_21_neural_networks
Neural Networks and Deep Learning Homework

## Libraries/Languages:
1. Pandas
2. Numpy
3. Matplotlib
4. Sklearn\
a. Standard Scaler\
b. MinMaxScaler\
c. Train-test split
5. Tensorflow
6. Keras-Tuner

## Work Description
1. Read in a CSV of charity data using Pandas
2. Did the following initial pre-processing steps in an attempt to get a deep learning model that could predict if an organization would successfully complete a goal with 75% accuracy:\
a. Dropped: EIN and Name columns\
b. Binned: Application Type and Classification columns\
c. OneHotEncoded the categorical columns using Pandas\
d. Ran the train-test split\
e. Scaled the entire dataset fit to X_train using StandardScaler
3. Ran 4 different deep learning models using Tensorflow with between 3 and 4 layers and a range of neurons per layer. All the hidden layers used `relu` as the activation type and the output layer was a `sigmoid` activation. To increase efficiency of these models and ensure that the model was neither overfit nor underfit, the epochs were set to 500 with an early stop inplace with a patience of 5\
a. None of these models performed well\
b. The accuracy for all of these models hovered around 50% +/- 3.2362% with varying levels of loss
4. Given the poor performance of 4 models, a keras-tuner was used to try and determine if the pre-processing would result in a model reaching 75% accuracy. However, the best accuracy that the keras-tuner achieved was 73.26%.
5. In an attempt to improve the models, different pre-processing steps were used to try and decrease noise. Changes varied by each of the 3 models, including:\
a. Removing more features\
b. Binning features\
c. Adding back in previously removed columns (i.e. Name)\
d. Scaling only the numeric columns (of which, there was only 1) using a MinMaxScaler
6. With the changes, a model was able to reach 74.9% accuracy.

Conclusion: Deep Learning model could likely be better tuned with additional pre-processing, but a tree-based model would likely perform better in addition to being faster and more explainable.