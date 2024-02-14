PCRD Result Recognition Model
===

## Files

```
|__ dataset/
|
|   # 
|__ process_heic.ipynb
|
|   # 
|__ preprocess_model.ipynb
|__ auto_label.csv
|
|   
|__ result_model
```

## Run

### Convert Image File Type

* Run `process_heic.ipynb` to convert `HEIC` files to `JPG` files.
* The converted images will be saved under the directory `training_data/`.
* `auto_label.csv` will be automatically generated with corresponding number of labels, and will be used later for training.

### Two-Step Model

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


### Single Step Model
* Run `preprocess_model.ipynb`.
* The label used in this step was written in `multi_label.csv`
* There are three models in this file, including linear regression, random forest, and convolution neural network.
* The best model will be saved in `single_model.tflite` for later use in the app.