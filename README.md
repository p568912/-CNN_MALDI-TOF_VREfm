## description
In this project, we develop the deep learning algorithm to classify bacteria with vanocomycin resistance (VREfm) or not according to the MS data. Our performance is superior than previous methods such as tradition machine learning. In addition, our code can tell users which m/z range is more important for any samples. We will give score for each m/z position by normalizing from 0 to 1 in each sample. If the score is greater in the specified m/z position, it will represent the model consider m/z position more important. We hope our algorithm can be applied to resistance classifcation of any kind of bacteria.

## workflow
We divde into three sections: preprocessing, training ,model interpretation.

### preprocessing: (preprocess.py)
MS data is processed and it will be transformed as deep learning model input after preprocessing.
```bash
python3 preprocess.py --input INPUT
```


### training: (trainBatDropout.py, dataset.py)
In this section, we will train the model from our code using preprocessed input in previous step. Users can modify parameters to change the architeture of network based on demands. (ex:poolingFlag,ReLUFlag,channels,batch_size, etc.)

```bash
python3 trainBatDropout.py --trainData TRAINING_DATA --trainLabel TRAINING_LABEL --testData TESTING_DATA --testLabel TESTING_LABEL
```


### model interpretation: (scorecam.py)
If you set showPosImportance True,the code will give users the m/z position importance in test data.It will be saved at model_avgpool_score_cam.npy .

```bash
python3 trainBatDropout.py --trainData TRAINING_DATA --trainLabel TRAINING_LABEL --testData TESTING_DATA --testLabel TESTING_LABEL --showPosImportance True
```

## usage
```bash
usage: trainBatDropout.py  [-h help] 
                  [--trainData TRAINING_DATA] 
                  [--trainLabel TRAINING_LABEL]
                  [--testData TESTING_DATA] 
                  [--testLabel TESTING_LABEL]
                  
                  [--savePath MODEL_PATH] [--predPath PREDPATH] 
                  [--batch_size BATCH_SIZE] [--optimizer OPTIMIZER]
                  [--seed SEED] [--poolingFlag POOLINGFLAG]
                  [--ReLUFlag RELUFLAG] [--showPosImportance SHOWPOSIMPORTANCE]
                  [--channels CHANNELS] [--cuda CUDA]
                  [--learning_rate LEARNING_RATE] [--epochs EPOCHS]
                  [--splitRatio SPLIT_RATIO]
                  
Required arguments:
    --trainData
                        training Data path 
                        [Type: String]  
    --trainLabel
                        training label path 
                        [Type: String]
    --testData
                        testing Data path 
                        [Type: String]  
    --testLabel
                        testing label path 
                        [Type: String]  
Optional arguments:
    -h, --help            
                        Show this help message and exit
    --epochs EPOCHS
                        Number of epochs for training. 
                        [Type: Int, default: 30]
    --learning_rate LEARNING_RATE         
                        Learning rate for training model. 
                        [Type: Float, default: 0.0001]   
                        
    --batch_size BATCH_SIZE
                        Batch size for each training iterations. 
                        [Type: Int, default: 32]                         

    --optimizer OPTIMIZER
                        Optimizer used for training models. 
                        [Type: String, default: "adam", options: "sgd, adam, adagrad"]
                        
    --cuda 
                        We use this parameter to determine to use cuda or not. If you want to use gpu, you can type in gpu index, e.g.: 0.
                        If you want to use cpu only, you can type -1.
                        [Type: Int, default: 0 ]  
                        
     --savePath 
                        This parameter is treated as saved path. We will save trained modules to this path after training.
                        [Type: str]                       
                        

