# Transformers-based Models for Basket Completion

This repository contains scripts to pre-train a GPT and BERT model for basket completion. Fine-tuning can be performed for both models, and an adversarial training procedure is included named HAMSTER. However, this training procedure proves to be less accurate and needs way longer to train.

## Data

The data we used was provided by a large Dutch grocery chain. The data includes:

- Taxonomy - Relation of products.
- ProductInformation - Convert product IDs to names, and get information on the product on the website.
- Transactions - Session shopping data. Every rule in the data set represents a shopping session by the productIDs that were put in the basket. 

## Setting up the environment

A requirements.txt file is included in the repository, however, the code was run on Apple M1 Pro GPUs. Hence, one would need to use the Tensorflow-Metal package, for which multiple tutorials are available on the web.

## Running the code

Using the data cleaning scripts, you should clean and shuffle the data before creating separate pre-train, train, and test sets. (Use tf_AH21_data_cleaning, or  tf_RS15_data_cleaning)

Once your data is uploaded and the correct paths are referenced in the code, you can start by running one of the pre-train scripts with the 'Universal Tokeniser' part uncommented to create a tokeniser. After this is done, the tokeniser part can be commented again, since you should only do this once and use this tokeniser from here onwards. (Use tf_GPT_pre-training,or tf_BERT_pre-training)

After making sure the best model weights are saved, you can move on to fine-tuning. First, the scripts perform hyperparameter optimisation using Tree Parzen Estimators. Then, the optimal hyperparameters are saved and used to train the model on the entire train set. (Use tf_GPT_fine-tuning, tf_BERT_fine-tuning, or tf_HAMSTER_fine-tuning)

Finally, qualitative analysis can be performed to obtain additional performance metrics on the test set. (Use tf_GPT_QA, or tf_BERT_QA)
