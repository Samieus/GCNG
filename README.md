# GCNG
using graph convolutional neural network and spaital transcriptomics data to infer cell-cell interactions
# Title, GCNG: Graph convolutional networks for inferring cell-cell interactions
## date: Nov 1, 2019

># 1, GCNG
![](https://github.com/xiaoyeye/GCNG/blob/master/GCNG.bmp)

GCNG for extracellular gene relationship inference. (A) GCNG model using spatial single cell expression data. A binary cell adjacent matrix and an expression matrix are extracted from spatial data. After normalization, both matrices are fed into the graph convolutional network. (B) Training and test data separation and generation strategy. The known ligand and receptor genes can form complicated directed networks. For cross validation, all ligand and receptors are separated exclusively as training and test gene sets, and only gene pairs where both genes are in training (test) are used for training (test). To balance the dataset, each positive ligand-receptor (La; Rb) gene pair with label 1 will have a negative pair sample (La; Rx) with label 0 where Rx was randomly selected from all training (test) receptor genes which are not interacting with La in training (test).

># 2, Code environment

>>## Users need to install python and all the modules required by the code, including ‘spektral’, ‘Keras’ and ‘Tensorflow’. We  recommend Anaconda.
Author's environment is python 3.6.3 in a Linux server which is now running Centos 6.5 as the underlying OS and Rocks 6.1.1 as the cluster management revision. 

># 3, example for running

>>## 3.1 Training and test data generation  for ligand-receptor prediction
>>>### Usage: 

    python data_generation_interaction_ten_fold.py

`data_generation_interaction_ten_fold.py` uses the spatial location data to generate normalized adjacent matrix of cells, and save it in `seqfish_plus` folder; also uses the expression data to generate expression matrix for ten fold cross validation, and save it in `rand_1_10fold` folder.

>>## 3.2 Training and test model

    python gcn_LR2_LR_as_nega_big.py
    
  `gcn_LR2_LR_as_nega_big.py` uses normalized adjacent matrix to generate normalized laplacian matrix, and then uses laplacian matrix to train and test GCNG models in ten fold cross validation. 
  
 >>## 3.3 get optimal model
 
     python gcn_LR2_LR_as_nega_big_layer_predict_min.py
     
   `gcn_LR2_LR_as_nega_big_layer_predict_min.py` tries to find the optimal model during the trainning, by monitoring the validation dataset's accuracy.
   
 >>## 3.4 get performance of optimal model for ten fold cross validation
  
     python predict_analysis_more_kegg_tfs_average_whole_new_rand.py
     `predict_analysis_more_kegg_tfs_average_whole_new_rand.py` collects results of the optimal model in each fold to present the final results.
 
