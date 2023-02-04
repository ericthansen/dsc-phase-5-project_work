# dsc-phase-5-project_work
Flatiron Capstone project work
# Deepfake Detection in Images

## Final Presentation Link, including visuals and discussion:  
https://github.com/ericthansen/dsc-phase-5-project_work/blob/main/presentation_proj4.pdf
## Data Source Link:  
https://www.kaggle.com/code/luixmartins/starter-eda-steam-game-review/data

## Instructions for navigation
The root directory contains only final product files, including the Jupyter notebook containing Python code and a final presentation.  
The images directory contains some visualizations that appear in the presentation.  
The data directory contains the text reviews and ratings data.  

## Motivation
Deepfakes (a portmanteau of "deep learning" and "fake") are an artificial image or video that replaces an existing entity with another entity's likeness.

Creation of such media has some benign applications in art and academia, but in general, the capacity for misleading deepfakes is of great concern to a wide variety of stakeholders, including public figures, media producers and distribution platforms, and individual citizens, due to its potential to be used for harmful ends.

To combat existing and new deepfake techniques, similar visual models in deep learning can be employed to help detect deepfakes and flag them as fake.

For this project, which uses data derived from a deepfake detection challenge on Kaggle from December 2019 (https://www.kaggle.com/competitions/deepfake-detection-challenge), we will analyze a dataset of still images extracted from deepfake and real videos. A baseline model and an advanced hand-made model will be created, then several pretrained models will be tuned and tested. Finally, some visual interpretability will be explored using LIME and Grad-CAM (popular interpretability approaches in Python).

Business problems that such an investigation could illuminate include:
- How to identify current deepfake manipulation 
- What techniques and models work well on current deepfakes, informing what techniques may have best success on identifying future deepfake techniques  

## Data Sources
Kaggle data source: [https://www.kaggle.com/competitions/deepfake-detection-challenge](DeepFake Detection Challenge)  
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

The highest performing model, Xception, has the following confusion matrix on test data.

(insert image)

### Visualizations
LIME and Grad-CAM provide different visual insights and interpretability into CNN models.  

This LIME augmented image highlights which features were most important in one sample image for its categorization.

(insert)

This Grad-CAM array shows different real and fake images and which areas on the image were most important to their categorization.

(insert)

F

## Further Improvements
One of the desired future outcomes would to be to develop a "positivity/negativity" continuous rating to text reviews, with which to test consistency on non-binary ratings.  Also, improved performance on the deep learning models could be pursued, perhaps with additionally tuned or complex models or more data.
