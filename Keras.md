# Keras Prep

## What is Keras?

A: Keras is a high-level neural networks API, written in Python and capable of running on top of TensorFlow, CNTK, or Theano. It was developed with a focus on enabling fast experimentation. Being able to go from idea to result with the least possible delay.

## What all kind of inputs does Keras support?

A: Keras supports three main types of inputs: Numpy arrays, TensorFlow tensors, and Python generators.

## What is the difference between Sequential model and Functional API?

A: The Sequential model is a linear stack of layers, where you can use the .add() method to add layers. The Functional API is more flexible, allowing you to define multiple input or output layers, and connect layers in ways that are not possible with the Sequential model.

## What are the diffferent types of regularizations available in Keras?

A: The different types of regularizations available in Keras are L1, L2, and L1L2.

- L1 regularization: Adds a penalty equal to the absolute value of the magnitude of the coefficients.
- L2 regularization: Adds a penalty equal to the square of the magnitude of the coefficients.
- L1L2 regularization: Adds a penalty equal to the sum of the absolute and square of the magnitude of the coefficients.
- Dropout: Randomly sets a fraction of input units to 0 at each update during training time, which helps prevent overfitting.
- Early stopping: Stops training when a monitored quantity has stopped improving.
- Data augmentation: Generates new training samples by applying random transformations to the existing samples.
- Batch normalization: Normalizes the activations of the previous layer at each batch, which helps stabilize training and reduce overfitting.
- Weight decay: Adds a penalty to the loss function based on the magnitude of the weights.
- Label smoothing: Replaces hard 0 and 1 labels with soft values like 0.1 and 0.9 to prevent overfitting.
- learning rate scheduling: Adjusts the learning rate during training to improve convergence and generalization.
- Cross-validation: Splits the data into multiple subsets for training and validation to evaluate the model's performance.

## What is cross-validation? How can you implement it in Keras?

A: Cross-validation is a technique used to evaluate the performance of a machine learning model by training and testing it on multiple subsets of the data. In Keras, you can implement cross-validation using the `KerasClassifier` or `KerasRegressor` wrapper classes provided by scikit-learn. These classes allow you to use Keras models as estimators in scikit-learn's cross-validation functions.

```python

from keras.wrappers.scikit_learn import KerasClassifier
from sklearn.model_selection import cross_val_score

def create_model():
    model = Sequential()
    model.add(Dense(12, input_dim=8, activation='relu'))
    model.add(Dense(1, activation='sigmoid'))
    model.compile(loss='binary_crossentropy', optimizer='adam', metrics=['accuracy'])
    return model

model = KerasClassifier(build_fn=create_model, epochs=150, batch_size=10, verbose=0)
results = cross_val_score(model, X, Y, cv=10)
print(results.mean())

```

## What are callbacks in Keras?

A: Callbacks in Keras are objects that can perform actions at various stages of training (e.g., at the start or end of an epoch, before or after a batch, etc.). They are useful for monitoring the training process, saving model checkpoints, early stopping, learning rate scheduling, and more. Some common callbacks in Keras include `ModelCheckpoint`, `EarlyStopping`, `ReduceLROnPlateau`, `TensorBoard`, and `CSVLogger`.

## What is eager execution in TensorFlow 2.0? and how does it affect Keras? and how can it be used for debugging?

A: Eager execution is a mode in TensorFlow 2.0 that allows operations to be executed immediately, rather than building a computational graph and running it later. This makes it easier to debug models, as you can inspect the results of operations directly. In Keras, eager execution can be enabled by setting `tf.keras.backend.set_floatx('float32')` before importing Keras. This will ensure that Keras uses eager execution by default. You can also enable eager execution explicitly by calling `tf.config.run_functions_eagerly(True)`.

- Eager execution can be used for debugging by allowing you to inspect the results of operations directly, without having to build and run a computational graph.
- It affects Keras by making it easier to debug models and experiment with different architectures and hyperparameters.

## What is the difference between compile and fit in Keras?

A: The `compile` method in Keras is used to configure the model for training by specifying the loss function, optimizer, and metrics. The `fit` method is used to train the model on a given dataset by specifying the input data, target data, batch size, number of epochs, and validation data. In other words, `compile` is used to set up the model for training, while `fit` is used to actually train the model.

## How can we create Keras models?

A: There are three main ways to create Keras models: using the Sequential model API, the Functional API, or by subclassing the Model class.

- Sequential model API: This is the simplest way to create a model by stacking layers in a linear fashion.

```python
model = Sequential()
model.add(Dense(64, activation='relu', input_shape=(784,)))
model.add(Dense(64, activation='relu'))
model.add(Dense(10, activation='softmax'))
```

- Functional API: This allows for more complex models with multiple inputs and outputs, shared layers, and branching architectures.

```python
inputs = Input(shape=(784,))
x = Dense(64, activation='relu')(inputs)
x = Dense(64, activation='relu')(x)
outputs = Dense(10, activation='softmax')(x)
model = Model(inputs=inputs, outputs=outputs)
```

- Subclassing the Model class: This allows for complete customization of the model architecture and training loop.

```python
class MyModel(Model):
    def __init__(self):
        super(MyModel, self).__init__()
        self.dense1 = Dense(64, activation='relu')
        self.dense2 = Dense(64, activation='relu')
        self.dense3 = Dense(10, activation='softmax')

    def call(self, inputs):
        x = self.dense1(inputs)
        x = self.dense2(x)
        return self.dense3(x)

model = MyModel()
```

## What is the difference between a loss function and an optimizer in Keras?

A: A loss function is used to measure how well the model is performing on the training data, while an optimizer is used to update the model's weights based on the loss function. In other words, the loss function defines the objective that the model is trying to minimize, while the optimizer determines how the model's weights are adjusted to achieve this objective.

## What are data loaders in Keras?

A: Data loaders in Keras are objects that are used to load and preprocess data for training and evaluation. They typically take input data and target data as input, and provide batches of data to the model during training. Some common data loaders in Keras include `ImageDataGenerator` for image data, `TextVectorization` for text data, and `TimeseriesGenerator` for time series data.

## What is K-fold cross-validation?

A: K-fold cross-validation is a technique used to evaluate the performance of a machine learning model by training and testing it on multiple subsets of the data. The data is divided into K subsets, or folds, and the model is trained on K-1 folds and tested on the remaining fold. This process is repeated K times, with each fold used as the test set exactly once. The final performance of the model is then calculated as the average of the performance on each fold.
eg: 5-fold cross-validation involves dividing the data into 5 subsets, training the model on 4 subsets and testing it on the remaining subset, and repeating this process 5 times.

## What is the purpose of the validation set in Keras?

A: The purpose of the validation set in Keras is to evaluate the performance of the model on data that is not used for training. This allows you to monitor the model's performance on unseen data and detect overfitting. The validation set is typically used to tune hyperparameters, such as the learning rate or batch size, and to determine when to stop training the model (e.g., using early stopping).

Some of the cross-validation methods are:

- Hold-out K-folds: The data is divided into K subsets, or folds, and the model is trained on K-1 folds and tested on the remaining fold. This process is repeated K times, with each fold used as the test set exactly once. The final performance of the model is then calculated as the average of the performance on each fold.

- Leave-one-out: Each data point is used as the test set once, with the remaining data used for training. This process is repeated for each data point, and the final performance of the model is calculated as the average of the performance on each data point.

- Leave-p-out: Similar to leave-one-out, but with p data points used as the test set each time.
Stratified K-folds: Similar to K-folds, but with the data divided into folds such that each fold contains approximately the same proportion of each class.

- Repeated K-folds: The K-folds process is repeated multiple times, with different random splits of the data each time. The final performance of the model is then calculated as the average of the performance on each split.

- Nested K-folds: A combination of K-folds and cross-validation, where an inner loop is used to tune hyperparameters on a validation set, and an outer loop is used to evaluate the model on a test set.

## What is a confusion matrix?

A: A confusion matrix is a table that is used to evaluate the performance of a classification model by comparing the predicted labels with the true labels. It shows the number of true positives, true negatives, false positives, and false negatives for each class in the dataset. The confusion matrix is useful for calculating metrics such as accuracy, precision, recall, and F1 score, and for identifying common errors made by the model.

## what is bias and variance tradeoff?

A: The bias-variance tradeoff is a fundamental concept in machine learning that describes the relationship between the bias of a model and its variance. Bias refers to the error introduced by approximating a real-world problem with a simple model, while variance refers to the error introduced by the model's sensitivity to fluctuations in the training data. A model with high bias is underfitting the data, while a model with high variance is overfitting the data. The goal is to find a balance between bias and variance that minimizes the model's total error on unseen data.

To counteract overfitting, you can use techniques like regularization, dropout, early stopping, and data augmentation. These techniques help prevent the model from memorizing the training data and improve its generalization to unseen data.

To counteract underfitting, you can use techniques like increasing the model's capacity, adding more layers or neurons, and training for more epochs. These techniques help the model learn more complex patterns in the data and improve its performance on the training set.
