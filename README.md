# ProfnerTask7
The UoB-NLP team participated in the ProfNER-ST shared subtask 7a.
The objective of the task was to detect when a profession is mentioned in social media text. 
Our team developed four systems using pre-trained BERT models:
  1. mBERT-base
  2. BERT-base 
  3. mBERT-Aug
  4. Bilingual model
 
Our team experiments with data augmentation and bilingual models to meet the objective of the task.
The best performing model on the test data is the mBERT-Aug model, which consists of mBERT fine-tuned on augmented data using back-translation.

## Model details and hyperparameters:

Each model was trained using the training data provided by ProfNER-ST task organizers. Please see task [website](https://temu.bsc.es/smm4h-spanish/) for details.

The following libraries were used:
  * Keras
  * Demoji
  * Hugging Face Transformers
  * Pandas
  * Numpy
  * Scikit-learn
  * Google Translate API
  
### Preprocessing
Punctuation, hashtags, twitter handles, emojis and URL's were removed from English and Spanish tweets.
Tweets were tokenised using Hugging Face Transformers library.
All tweets were specified to have the max length of 80. Any higher or any less would significatly degrade performance of the models.


### mBERT, BERT, and mBERT-Aug Details

These three models consist of:
  1. two input layers, input_ids and input_masks which are fed to the transformer model.
  2. a dense layer with sigmoid as the activation function.
  3. binary crossentropy loss
  4. Adam optimizer with a learning rate of 3e-5 (mBERT and BERT) a learning rate of 5e-5 was used for mBERT-Aug
  5. batch-size 32
  6. Epochs 3

 ### Bilingual Model
 This model consist of mBERT-base and BERT-base. 
 The outputs of both these models are concatenated and fed to a dense layer.
 
 The the model consists of:
  1. four input layers, input_ids and input_masks for both Spanish and English tweets, which are fed to the corresponding transformer models.
  2. a dense layer with sigmoid as the activation function.
  3. binary crossentropy loss
  4. Adam optimizer with a learning rate of 3e-5 
  5. batch-size 32
  6. Epochs 3

## Results

The best performing model on test data was mBERT-Aug, followed by mBERT, Bilingual model, and BERT-base.

|Model          |Precision           |Recall           |F-1  |
| :---          |  :----:            |  :----:         | ---:|
|mBERT          | 0.9538             | 0.7127          | 0.82|
|BERT-Base      | 0.6620             | 0.1015          | 0.18| 
|mBert-Aug      | 0.9171             | **0.7646**      |**0.83**| 
|Bilingual      |0.9579              | 0.6393          | 0.77|


The code for the preprocessing and training of models is provided in this repository, titled Profner, and the code used to translate the examples is titled Translate_Data.
