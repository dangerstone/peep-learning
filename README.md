# Peep Learning: Species classification of garden bird feeder images 🐦

**Group 1: Anna Hallenberg, Anne Kirstine Overgaard, & Stinna Danger**

# Project description
The goal of our project is to build a classifier to identify garden bird species and assess its applicability to image data from bird feeder cameras, which is relevant for data sorting in, for instance, conservation research and biodiversity monitoring. We will use the following three datasets:
* Bird feeder images: https://www.kaggle.com/datasets/ronanreilly/birdfeeder-images-and-video-clips
* *UK Garden Birds: https://www.kaggle.com/datasets/davemahony/20-uk-garden-birds

\* *For the scope of this project, we will consider the species, blue tit, chaffinch, coal tit, goldfinch, great tit, robin, and starling. We will use the subset of this dataset containing images of the species we are considering in this project.*

We will train our model on dataset 2, which contain images of the bird species. We will then investigate the model’s performance when tasked with classifying the bird feeder images in data set 1, which are retrieved from wild cameras.
To build our model, we will use transfer learning using the ResNet-architecture and expect to make some layers of the model trainable, allowing it to adjust to the specific task of classifying birds. We also expect to use data augmentation to prevent overfitting, and will investigate loss curves for the training and validation data. We are interested in identifying patterns and pitfalls of the model and, to this end, we will consider the classifier’s confusion matrix and F-score and perform qualitative assessments of misclassed images.

## Related work
Related work is listed below, where we have found research using different versions of the ResNet-architecture as well as research that build the model from scratch:
* Kennelly, S. and Green, R., "Classifying Bird Feeder Photos," 2020 35th International Conference on Image and Vision Computing New Zealand (IVCNZ), Wellington, New Zealand, 2020, pp. 1-6, doi: 10.1109/IVCNZ51579.2020.9290682. 
* Anusha, P., and ManiSai, K., "Bird Species Classification Using Deep Learning," 2022 International Conference on Intelligent Controller and Computing for Smart Power (ICICCSP), Hyderabad, India, 2022, pp. 1-5, doi: 10.1109/ICICCSP53532.2022.9862344. 
* Wang, Y.; Zhou, J.; Zhang, C.; Luo, Z.; Han, X.; Ji, Y.; Guan, J. “Bird Object Detection: Dataset Construction”, Model Performance Evaluation, and Model Lightweighting. Animals 2023, 13, 2924, doi: 10.3390/ani13182924.
* Niemi, J.; Tanttu, J.T. “Deep Learning Case Study for Automatic Bird Identification”. Appl. Sci. 2018, 8, 2089, doi: 10.3390/app8112089. 

# Git Setup

We defined the data setup in [preprocess](preprocess.ipynb). This was where we split our dataset into, train, test and validation sets. 

Our train function, datapaths ect. are defined in [setup](setup.ipynb). It is also in this notebook together with [extraFunctions](extraFunctions.ipynb) we defined our print functions for accuracy, loss and so on.

The rest of the notebooks are different stages of our experiments during the creating of our final model. Some important ones to note is the notebooks [basemodel](basemodel.ipynb), [finetuning](finetuning.ipynb) and [finetuningaug](finetuningaug.ipynb).


