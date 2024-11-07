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




TODO next step

hvis vi bare kører den så virker den fint på validation
så
  - kør på test set og se om den virker
  - se om den virker på feeder data
  - tilføj noget augmentation 
  - skal man normalisere feeder og test data?



  what did we do 07/11/24
  - trained model from scratch on full traning and validation set, first freezing all but the last layer, then fine tuning by unfreezing all layers
  - first training with 10 epochs took 18min on device 
    - It got around
    - Train Loss: 0.4841 Acc: 0.9150
    - Val Loss: 0.3323 Acc: 0.9904
  - Second training with 6 epochs took around 30min on device
    - It got around
    - Train Loss: 0.0237 Acc: 0.9964
    - Val Loss: 0.0522 Acc: 0.9808
    - At the last epoch, the validation accuracy was slightly worse than in the fifth epoch
  - Kørte det på test dataloader
    - Accuracy 94.28571428571428
    - den havde sværrest ved greatTit som den troede var coalTit
  - kørte den på feederData, makeAll tog 25 min i sig selv 
      Accuracy 46.87313482326414
    [[ 560   26  358  102  409  267  356]
    [ 300  835  580  708  152  578  399]
    [ 126   40 1134  101  126   16  303]
    [   7    5  263 1622   35   46   22]
    [ 260   17  464  116  505  175  496]
    [ 172  100   18   70    0  849  219]
    [  20    9  333   60   38  119 1563]]
  - e
  - so next try and add augmentation i hvert fald, 
    - tjek evt papers igennem igen og se om der er noget gode faglige ideer vi kan bruge, så vi også kan argumentere for hvorfor vi gør det og hvad vi gør
    -  