# 0x4D2 - RWTH - Germany

## Overview:
* This is the code for Kaggle Data Science Game 2016: Online selection,  we achieved rank of 16/200. 
* Check https://inclass.kaggle.com/c/data-science-game-2016-online-selection/leaderboard/private for the private result.
* The details of the game description can be found in https://inclass.kaggle.com/c/data-science-game-2016-online-selection. Top20 team got the finalist qualification in Paris, from September 09 -- September 11, 2016. 
* The model is based on Torch7 and its dependencies.
* The final csv file is generated by four models and an ensemble process.


### Data

`model/imglist/train.txt` contains the 8,000 training images (32x32).

`model/imglist/test.txt` contains the 8,000 training images (48x48).

### Network 

See `model/residual-network.lua`. (Similar structure to the standard deep-residual-network).

### Training
* We only used the original 8,000 data and training from scratch.
See `model/trainer.lua` (Weighted initialization process can be found in `model/initialize_weight.lua`).
Notice that we use real-time augmentation (random crop and flip tricks), which can be found in `model/augmentation.lua`.

### Trained Models:  

1. `model/pretrained/model_datasize32x32.t7`: produced on the data resized to 32x32. Depth is 28.
For the details see `model/classify_datasize32x32.csv`.


2.  `model/pretrained/model_datasize32x32_with_dropout0.3.t7`: produced on the data resized to 32x32.
The Dropout module is added to network. Depth is 28.
For the details see `model/classify_datasize32x32_with_deopout0.3.csv`.

3. `model/pretrained/model_datasize48x48.t7`: produced on the data resized to 48x48. Depth is 28.
For the details see `model/classify_datasize48x48.csv`.

4. `model/pretrained/model_datasize48x48_deeperNet.t7`: produced on the data resized to 48x48.
Just make the net deeper. Depth = 40. For the details see `model/classify_datasize48x48_deeperNet.csv`.

### Ensemble Process

`ensemble/ensemble.*` are used to combine the generated output result of the four models.
They read the four csv files (in submission format) and combine them into one submission formated csv file.

`ensemble/*.log` are the four log files to be combined, which are generated from the trained models..

