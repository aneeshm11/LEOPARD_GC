# LEOPARD_GC


This project aims to predict the bio-chemical recurence of cancer by using WSI tif files of prostate cancer.
The challenge is one of the many challenges on https://grand-challenge.org/ as part of MICCAI'24

METHOD:
 Each WSI has 5-6 levels and the first or second level is used.
 Patches of the level of ( n x n ) shape were extracted with regions of segmentation along with excessive cells clustered around. 
 The gt-labels for each patch is to be the same as the bio-recurrence time assigned with the complete WSI. Multiple patches are again stacked and passed to a Unet with regression 
 layers attatched in the final decoder layers. 


DATA: 
 - The number of patches can be in order of 1000s for a single WSI ( level 1). For level 0 it is 10x more than that of level 1
 - Batch size for the training is the number of patches being stacked for a single WSI. This ensures backprop is done for every WSI during a single epoch. 
 - The training data is massive (2 Tb) with each WSI of 2Gb to 7Gb
 - RAM plays crucial role compared to FLOPS. TPUs were used and 120Gb RAM was being used when 140 patches were stacked.
 - The results for all patches for the WSI can be either averaged/pooled or median can be choosen to compute loss depending on model performance and compute available. 



Data can be accesed here ->  https://surfdrive.surf.nl/files/index.php/s/MZlTzMmbDYu2nZp
