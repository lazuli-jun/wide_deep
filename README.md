# Wide and Deep Learning for CTR Prediction in tensorflow
## Overview
A general **Wide and Deep Joint Learning** Framework. 
Deep part can be a simple Dnn, Dnn Variants(ResDnn, DenseDnn), MultiDnn 
or even combine with Cnn (Dnn-Cnn).


Here, we use the [wide and deep model](https://research.googleblog.com/2016/06/wide-deep-learning-better-together-with.html) to predict the click labels. The **wide model** is able to memorize interactions with data with a large number of features but not able to generalize these learned interactions on new data. The **deep model** generalizes well but is unable to learn exceptions within the data. The **wide and deep model** combines the two models and is able to generalize while learning exceptions.

The code uses the high level `tf.estimator.Estimator` API. This API is great for fast iteration and quickly adapting models to your own datasets without major code overhauls. It allows you to move from single-worker training to distributed training, and it makes it easy to export model binaries for prediction.

The input function for the `Estimator` uses `tf.data.Dataset` API, which creates a `Dataset` object. The `Dataset` API makes it easy to apply transformations (map, batch, shuffle, etc.) to the data. [Read more here](https://www.tensorflow.org/programmers_guide/datasets).

The code is based on the TensorFlow wide and deep tutorial.


## Extensions
1. provide very flexible feature configuration and train configuration.
2. scalable to arbitrarily train data size in production environment.
3. support multi value feature input (multihot).
4. support distributed tensorflow  
5. support custom dnn network (arbitrary connections between layers)
6. support dnn, multidnn joint learning, even combine with cnn.
7. provide scripts to generate continuous features from category features using pyspark.
8. provide scripts to load data from hdfs.

## Running the code
### Setup
```
cd conf
vim feature.yaml
vim model.yaml
vim train.yaml
...
```

### Training
You can run the code locally as follows:

```
cd lib
python train.py
```
or use shell scripts as follows:
```
cd scripts
bash train.sh
```

The model is saved to `./model` by default, which can be changed using the `--model_dir` flag.

### Testing
```

python eval.py
```

### TensorBoard

Run TensorBoard to inspect the details about the graph and training progression.

```
tensorboard --logdir=./model/wide_deep
```



