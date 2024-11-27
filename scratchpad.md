# Ideas n shit

**Anne's foreslag til fremgang** 
1. Train clean images  
	1.1. Test on clean test set  
	1.2 Try to test on noisy test
2. w. noisy train set —> transfer learning or fewshot  
	2.1. test on noisy  
	2.2 test on clean

* **data augmentation**:  
blur, fish eye lense, occlusion, 

* **transfer learning**:  
  ResNet somehow,  
  what pre-stuff do they do

* **measure stuff**:  
  loss function ,  
  how to plot stuff

# Links  

Transfer Learning for Computer Vision Tutorial  
https://pytorch.org/tutorials/beginner/transfer_learning_tutorial.html  

How Does PyTorch Support ResNet?  
https://www.run.ai/guides/deep-learning-for-computer-vision/pytorch-resnet 

Transfer learning with ResNet in PyTorch
https://medium.com/@kirudang/deep-learning-computer-vision-using-transfer-learning-resnet-18-in-pytorch-skin-cancer-8d5b158893c5


The Essential Guide to Data Augmentation in Deep Learning  
https://medium.com/@saiwadotai/the-essential-guide-to-data-augmentation-in-deep-learning-f66e0907cdc8 

Layer Freezing info:
https://www.restack.io/p/transfer-learning-answer-layer-freezing-cat-ai


# Logs 

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
      Accuracy $46.87313482326414$
    $$
      \begin{bmatrix}
     560 &  26&  358&  102&  409&  267&  356 \\
     300&  835&  580&  708&  152&  578&  399 \\
     126 &  40& 1134&  101&  126&   16&  303 \\
       7  &  5&  263& 1622&   35&   46&   22 \\
     260 &  17&  464&  116&  505&  175&  496 \\
     172&  100&   18&   70&    0&  849&  219 \\
      20  &  9&  333&   60&   38&  119& 1563 
    \end{bmatrix}$$
  - so next try and add augmentation i hvert fald, 
    - tjek evt papers igennem igen og se om der er noget gode faglige ideer vi kan bruge, så vi også kan argumentere for hvorfor vi gør det og hvad vi gør
    -  

  Stinnaas spørgsmål fra 8/10
  - Forvirret over brug af transformers, fordi vi har simple_transfroms som er tom, og så lavede vi preprocess og preprocess_with_augmentation, som har den preprocessing som ResNet forventer (og som simple_transformer ikke har). Men der er lavet dataloaders der hedder X_set og X_aug, hvor de hhv. har simple_transform og preprocess. Men vi X_aug burde vel have den transformer med augmentations i.
  - feel like we should be able to sotre the makeAll result so we don't have to wait for it lmao

  stinnalog:
  forvirret over hvornår man "resetter" modellen/starter forfra for ligesom at køre et clean reset (a al det ak og jeg opplevede til den der tø med overfitting)
  
  lavede en setup notebook til alt det der indledende halløj som vi skal bruge til alle udgaver af modellerne

  added augmentations, bare basic fucking up of the images
  ser ud til at jeg skal køre det flere gange fordi acc stadig var på vej op ved 5 epochs
  forvirret over the tits haha
  har ikke testet på feederdata endnu fordi har ik lige tid til at køre lortet inden jeg skal hjem lmao
  men den klarer sig fint på test data med augmentation på, slutter med en 92% acc (igen, tror jeg lige skal køre det noget længere og se hvad der sker - også i tvivl om om vi skal concat det normale og det augmented datasæt fordi pointen er vel at augmentation gør datasættet STØRRE, right?)



14/11  
vi spurgte ind til augmentation, det er kun på train data. De skal ikke concats pga den måde dataloader virker på.    
Normalization er mere up in the air om man skal sætte på. However vi skal måske lige dobbelt tjekke de værdier vi har sat ind. Jeg mener det er fra Resnet, men det burde måske være baseret på vores dataset.  
Vi kørte med 8 epochs 4 batch-size, vi tror det skal sættes op.  
I et af papers'ne https://www.mdpi.com/2076-2615/13/18/2924 kører de ResNet50 med batch size 8 og 24 epochs, we should try this <- Anna will do    
I https://www.mdpi.com/2076-3417/8/11/2089 kører de en SVM med "_A linear classification model is applied. Stochastic gradient descent with 10 as the mini-batch size, and the Hinge loss function with regularization term 1/n, where n is a number of training examples_"  
De to andre papers har ved øjekast ikke skrevet hvad deres batch metode er

15/11  
Efter Anna kørte med 8, 24 tog det cirka to timer på train og test og vi fik en Accuracy på $94.28571428571428$ og 
$$
\begin{bmatrix}
14 & 0&  1&  0&  0&  0&  0& \\
  0 &15&  0&  0&  0&  0&  0& \\
  0 & 0& 14&  0&  1&  0&  0& \\
  0 & 0&  0& 15&  0&  0&  0& \\
  0 & 0&  3&  0& 12&  0&  0& \\
  0 & 1&  0&  0&  0& 14&  0& \\
  0 & 0&  0&  0&  0&  0& 15& \\
\end{bmatrix}
$$
  hvilket er den præcis samme accuracy som før hvilket jeg ikke ved om er sus eller handler om størelsen på vores testset. 

    
  Derudover prøvede vi at sætte weight decay på med 0.00001 og sætte learning rate til 0.02 efter de parametre de brugte i paper'et.  
  Vi tror nok det gav en accuracy på 83.80952380952381 og en conf matrix på
$\begin{bmatrix}
13  &0 & 1  &0  & 1  &0 & 0\\
 0 &12&  1  &1  & 1  &0 & 0\\
  0  &2 &10  &0  & 2  &0 & 1\\
  0  &0 & 0 &13  & 1  &1 & 0\\
  0  &0 & 2  &0 & 12  &0 & 1\\
  0  &0 & 1  &0  & 0 &14 & 0\\
  0  &0 & 0  &0  & 0  &1 &14\\
\end{bmatrix}$  
Vi prøvede også at compare precision recall explicit fordi det gjorde de i paper'et 
$$ \begin{matrix}
            &  precision  &  recall   &\text{f1-score}  &  &support \\
     \text{blueTit}  &     1.00     & 0.87     &  0.93        &15 \\
   \text{chaffinch}  &     0.86     & 0.80     &  0.83        &15 \\
     \text{coalTit}  &     0.67     & 0.67     &  0.67        &15 \\
   \text{goldfinch}  &     0.93     & 0.87     &  0.90        &15 \\
    \text{greatTit}  &     0.71     & 0.80     &  0.75        &15 \\
       \text{robin}  &     0.88     & 0.93     &  0.90        &15 \\
    \text{starling}  &     0.88     & 0.93     &  0.90        &15 \\
    \text{accuracy}  &              &          &  0.84       &105 \\
   \text{macro avg}  &     0.84     & 0.84     &  0.84       &105 \\
\text{weighted avg}  &     0.84     & 0.84     &  0.84       &105 \\
\end{matrix}$$


19/11 AKs log
- Har lavet en model_learning_rate og en exp_learning fil
- model_learning har en linear learning rate scheduler og en cycle_learning_rate scheduler mens exp_learning har den exp_learning_scheduler vi brugte til tø
- i begge filer er der en train_model_scheduled som er den samme
- jeg er i tvivl om hvilke parametre, har prøvet med nogle standard
- Med linear rate scheduler tog det 44+138 minutter at træne og accuracy kom op på 78%
$\begin{bmatrix}
13 &  0 &  1 &  0&  0 &  0&  1\\
 1 & 10 &  2 &  0&  0 &  0&  2\\
 2 &  0 & 13 &  0&  0 &  0&  0\\
 1 &  0 &  0 & 14&  0 &  0&  0\\
 1 &  0 &  5 &  0&  9 &  0&  0\\
 0 &  1 &  0 &  0&  0 & 13&  1\\
 2 &  0 &  3 &  0&  0 &  0& 10\\
\end{bmatrix}$
- cycle learning rate tog 45 +129 minutter at træne og den kom op på 98% accuracy
- cycle_scheduler = lr_scheduler.CyclicLR(optimizer=optimizer,base_lr=0.001, max_lr=0.1)
- er lidt i tvivl om hvor meget den reelt har cyclet lr 
- tror måske jeg skulle have sat step size til noget
- har ikke kørt exp learning rate endnu
- venter lige med at pushe mine filer  
20/11 
- trained exp model den fik accuracy på 93.3% 
- det tog 50 + 140 minutter
$$\begin{bmatrix}
 5 &  0&  0&  0&  0&  0&  0\\
 0 & 15&  0&  0&  0&  0&  0\\
 0 &  0& 15&  0&  0&  0&  0\\
 0 &  1&  0& 14&  0&  0&  0\\
 0 &  0&  4&  0& 10&  0&  1\\
 0 &  1&  0&  0&  0& 14&  0\\
 0 &  0&  0&  0&  0&  0& 15\\
 \end{bmatrix}
 $$
- prøvede at save og load dens state_dict, man skal huske at sætte den til model.eval() så tror jeg det virker
- BURDE VI ALTID SÆTTE MODEL.EVAL() I MAKE ALL ?????????????

21/11
- we need to make better argumnets for going from step to step
- so start initial model again with more epochs so we can inspect the loss curves
- EITHER
- - Copy the train_model from setup over in our old model.ipynb file
- - OR make a initial_model.ipynb and import setup.ipynb and run without any augmentations or anything besides normalization and toTensor
- run model with 40 epochs or something
- print loss curves with plot_accuracy function (or better make a plot_loss curves)
- unfreeze and run again



27/11
* Vi vinder ikke noget ved at have batch size 32, fordi det er 2 min forskel og basically samme acc

BASEMODEL: 60 epochs, 16 batch size, ADAM-optimiser

TODO: 
* Stinna: Træne+gemme basemodel (the real one) 
* A^K:    Træne basemodel men med SGD-optimiser + lr scheduler
* Anna:   Træne forskellige augs med basemodel