PCRD Result Recognition Model
===

This is the result recognition model for the PCRD approach.

## Files

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

### Convert Image File Type

* Run `process_heic.ipynb` to convert `HEIC` files to `JPG` files.
* The converted images will be saved under the directory `training_data/`.
* `auto_label.csv` will be automatically generated with a corresponding number of labels, and will be used later for training.

### Two-Step Model

**First step**
* Run `preprocess_mode.ipynb`.
* The label used in this step was written in `auto_label.csv`
  > The criteria used here is as follows:
  >  | Invalid Image | Valid Image |
  >  | ------------- | ----------- |
  >  | The PCRD kit is flipped upside-down | The PCRD kit is not flipped, rotated, or covered. |
  >  | The PCRD kit is covered by other objects | |
  >  | The PCRD kit is rotated (more than 45 degrees) | |
  >  | The PCRD kit is not in the photo | |
  >  | ![Sample Image](https://github.com/Peggy1210/iGEM-ML-Model/blob/main/PCRD_model/sample_image/PCRD_sample_1.png) | ![Sample Image](https://github.com/Peggy1210/iGEM-ML-Model/blob/main/PCRD_model/sample_image/PCRD_sample_2.png) |
* The best model will be saved in `preprocess_model.tflite` for later use in the app.

**Second step**
* Run `result_model.ipynb`.
* The label used in this step was written in `color_label.csv`
    > The criteria used here is as follows:
    >    | Positive | Negative |
    >    | ------------- | ----------- |
    >    | the PCRD kit has a control line | the PCRD kit has a control line |
    >    | the PCRD kit has T1 or T2 line or both | the PCRD kit has no test line |
    >    | ![Sample Image](https://github.com/Peggy1210/iGEM-ML-Model/blob/main/PCRD_model/sample_image/PCRD_sample_3.png) | ![Sample Image](https://github.com/Peggy1210/iGEM-ML-Model/blob/main/PCRD_model/sample_image/PCRD_sample_4.png) |
* This file has three models, including linear regression, random forest, and convolution neural network.
* The best model will be saved in `result_model.tflite` for later use in the app.


### Single Step Model
* Run `preprocess_model.ipynb`.
* The label used in this step was written in `multi_label.csv`
    > The criteria used here is as follows:
    >    | Invalid Image |  Low Possiblity | High possibility | Negative |
    >    | ------------- | ----------- | ------ | ------ |
    >    | the PCRD is flipped upside-down | the PCRD is not flipped, rotated, or covered | the PCRD is not flipped, rotated, or covered | the PCRD is not flipped, rotated, or covered |
    >    | the PCRD is covered by other objects | with C line and one line | with C line, T1 line, and T2 line | only C line |
    >    | the PCRD kit is rotated (more than 45 degrees) 
    >    | the PCRD kit is not in the photo |
    >    | ![Sample Image](https://github.com/Peggy1210/iGEM-ML-Model/blob/main/PCRD_model/sample_image/PCRD_sample_1.png) | ![Sample Image](https://github.com/Peggy1210/iGEM-ML-Model/blob/main/PCRD_model/sample_image/PCRD_sample_2.png) | ![Sample Image](https://github.com/Peggy1210/iGEM-ML-Model/blob/main/PCRD_model/sample_image/PCRD_sample_3.png) | ![Sample Image](https://github.com/Peggy1210/iGEM-ML-Model/blob/main/PCRD_model/sample_image/PCRD_sample_4.png) |
* This file has three models, including linear regression, random forest, and convolution neural network.
* The best model will be saved in `single_model.tflite` for later use in the app.
