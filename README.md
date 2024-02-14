iGEM ML Model
===

## Introduction

In our project, we designed a detection kit for colorectal cancer diagnosis. In order to enhance the user experience of our product, we developed a set of hardware and trained machine learning models to help recognize the results. This repository is the source code for the machine learning model. Visit our [project website](https://2023.igem.wiki/nthu-taiwan/hometext) to see more of our project!

## Files

There are two directories in this repository, `PCRD_model` and `AUNP_model`. The files under these directories follow this architecture:

```
|__ dataset/
|   |___ # Images of detection kit (`.HEIC` file)
|__ process_heic.ipynb # Convert `.HEIC` files to `.JPG` files
|
|   # Two-step models
|__ preprocess_model.ipynb # 1st step model
|__ auto_label.csv # 1st step model labels
|__ result_model # 2nd step model
|__ color_label.csv # 2nd step model labels
|
|   # Single-step model
|__ single_model.ipynb
|__ multi_label.csv # single-step model labels
```

## Run

### Process



#### Convert Image File Type

* Run `process_heic.ipynb` to convert `HEIC` files to `JPG` files.
* The converted images will be saved under the directory `training_data/`.
* `auto_label.csv` will be automatically generated with a corresponding number of labels, and will be used later for training.

#### Two-Step Model

**First step**
* Run `preprocess_mode.ipynb`.
* The label used in this step was written in `auto_label.csv`
* There are three models in this file, including linear regression, random forest, and convolution neural network.
* The best model will be saved in `preprocess_model.tflite` for later use in the app.

**Second step**
* Run `result_model.ipynb`.
* The label used in this step was written in `color_label.csv`
* There are three models in this file, including linear regression, random forest, and convolution neural network.
* The best model will be saved in `result_model.tflite` for later use in the app.


#### Single Step Model
* Run `preprocess_model.ipynb`.
* The label used in this step was written in `multi_label.csv`
* There are three models in this file, including linear regression, random forest, and convolution neural network.
* The best model will be saved in `single_model.tflite` for later use in the app.
