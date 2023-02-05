# dsc-phase-5-project_work
Flatiron Capstone project work
# Deepfake Detection in Images

## Final Presentation Link, including visuals and discussion:  
https://github.com/ericthansen/dsc-phase-5-project_work/blob/main/presentation_proj5.pdf
## Data Source Link:  
[https://www.kaggle.com/datasets/ericth/deep-fake-detection-on-faces](https://www.kaggle.com/datasets/ericth/deep-fake-detection-on-faces)

## Instructions for navigation
The root directory contains only final product files, including the Jupyter notebook containing Python code and a final presentation.  
The images directory contains some visualizations that appear in the presentation.  
There is no data directory - data is hosted on Kaggle (link above) and is too large to store on github.  Models are created and saved on google drive through course of running the notebook.

## Motivation and Goals
Deepfakes (a portmanteau of "deep learning" and "fake") are an artificial image or video that replaces an existing entity with another entity's likeness.

Creation of such media has some benign applications in art and academia, but in general, the capacity for misleading deepfakes is of great concern to a wide variety of stakeholders, including public figures, media producers and distribution platforms, and individual citizens, due to its potential to be used for harmful ends.

To combat existing and new deepfake techniques, similar visual models in deep learning can be employed to help detect deepfakes and flag them as fake.

For this project, which uses data derived from a deepfake detection challenge on Kaggle from December 2019 (https://www.kaggle.com/competitions/deepfake-detection-challenge), we will analyze a dataset of still images extracted from deepfake and real videos. A baseline model and an advanced hand-made model will be created, then several pretrained models will be tuned and tested. Finally, some visual interpretability will be explored using LIME and Grad-CAM (popular interpretability approaches in Python).

Business problems that such an investigation could illuminate include:
- How to identify current deepfake manipulation 
- What techniques and models work well on current deepfakes, informing what techniques may have best success on identifying future deepfake techniques  

To this end, our goal is to correctly classify deepfake and real images.

## Data Sources
Original Kaggle Competition: [Deepfake Detection Challenge](https://www.kaggle.com/competitions/deepfake-detection-challenge/)  
Kaggle data source (extracted images): [Deepfake Faces](https://www.kaggle.com/datasets/dagnelies/deepfake-faces)  
This zip file contains a metadata file with labels.  
This includes 95,634 JPEG images, including 17% Real and 83% Fake images.  This is just over 16,293 real images.  
In order to avoid class imbalance, and since 16K of each class is sufficient for good training, number of samples of each class is restricted to 16,000.

## Preprocessing / Feature Engineering:
- Data augmentation is performed, including horizontal reflection and some rotation.


## Metrics
Different metrics inform analysis of different data.  

For this venture, Accuracy will be the primary metric for training models.  Confusion matrices are created to get better insight into recall and precision, in the event that we need to choose different models for these different purposes (e.g. we may need a model with minimal False Negative rate).

## Forecasting Methodology
### Classification
All the created deep learning models supply a percent likelihood of being real or fake (using a sigmoid final layer), for final classification, the higher likelihood is what is used for predicted label.  For future usage, extracting the likelihood value can help provide confidence measure on how probable it is that an image is real or fake.

### Models
Model performance was ultimately ranked on accuracy.
Several CNN models were created, including a manually-constructed and pretrained models.  Accuracy values are provided:
- Baseline convolution model - 50% accuracy
- Manual model (based on XCeption) - 76.7% accuracy
-  VGG19 - 64% 
-  MobileNet - 67%
-  Xception - 87.8%
-  EfficientNetB0 - 80.6% 
-  EfficientNetV2L - 60.6%

For all pretrained models, each base model is loaded in and connected to desired output layer for classification.  Rough training is done on the new top layers.  Then base model is unfrozen and fine-tuning is performed at a lower learning rate.  

The highest performing model, Xception, has the following confusion matrix on test data.

0 represents "real" image and 1 represents "fake".
This also performs with 90% precision (true positives / all predicted positives) and 85% recall (true positives / actual positives).
![Xception Confusion Matrix](https://github.com/ericthansen/dsc-phase-5-project_work/images/XcepCM.png)

### Visualizations
LIME and Grad-CAM provide different visual insights and interpretability into CNN models.  

This LIME augmented image highlights which features were most important in one sample image for its categorization.
This "Real" image, classified correctly:
![Raw image visualization](https://github.com/ericthansen/dsc-phase-5-project_work/images/lime_1.png)
has the following  highly important features.  Features in green suggest it is "real" and those in red are areas that appear more "fake."
![Lime Features image visualization](https://github.com/ericthansen/dsc-phase-5-project_work/images/lime_2.png)

This Grad-CAM array shows different real and fake images and which areas on the image were most important to their categorization.

For one sample fake image:
![raw sample image visualization](https://github.com/ericthansen/dsc-phase-5-project_work/images/gc_1.png)  
this heatmap shows areas in the image that appear "fake"
![Grad-CAM image visualization](https://github.com/ericthansen/dsc-phase-5-project_work/images/gc_2.png)

This image was incorrectly classified as "real" - there is some "fake" heat appearing on the edge of the image:
![Grad-CAM image visualization](https://github.com/ericthansen/dsc-phase-5-project_work/images/gc_3_actualFakePredReal.jpeg)

This "real" image was correctly classified - it has very little "heat".
![Grad-CAM image visualization](https://github.com/ericthansen/dsc-phase-5-project_work/images/gc6_realreal.jpeg)

## Further Improvements
The EfficientNetV2L performance should really be higher.  With more processing resources, one could refine the model fitting with more epochs.  
