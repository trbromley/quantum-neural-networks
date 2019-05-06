<img align="left" src="https://github.com/XanaduAI/quantum-neural-networks/blob/master/static/fraud_detection.png" width=300px>

# Fraud detection

This folder provides the source code used in Experiment B in *"Continuous-variable quantum neural networks"* [arXiv:1806.06871](https://arxiv.org/abs/1806.06871).

## Getting the data

The raw data is sourced from the [Credit Card Fraud Detection](https://www.kaggle.com/mlg-ulb/creditcardfraud) dataset on Kaggle. The `creditcard.csv` file should be downloaded and placed in this folder. The user can then run:
```bash
python3 data_processor.py
```
This script creates two datasets for training and testing.

## Training and testing the model

The model is a hybrid classical-quantum classifier, with a number of input classical layers that control the parameters of an input layer in a two-mode CV quantum neural network. The model is trained so that it outputs a photon in one mode for a genuine credit card transaction, and outputs a photon in the other mode for a fraudulent transaction.

Training can be performed with:
```bash
python3 fraud_detection.py
```
The model is periodically saved during training, and progress can be monitored by launching TensorBoard in the terminal:
```bash
tensorboard --logdir=outputs/tensorboard/simulation_label
```
where the user replaces `simulation_label` with the chosen number/string used in `fraud_detection.py` (the default is `1`).

Testing can be performed with:
```bash
python3 testing.py
```
Here, the user must choose a value for `simulation_label` in `testing.py` to select a pre-trained model, as well as `ckpt_val` to select the number of batch repetitions to start testing from.

The output of testing is a confusion table, which can be found as a numpy array in `outputs/confusion/simulation_label`. The confusion table is given for multiple threshold probabilities for a transaction to be considered as genuine.

## Visualizing the results

The performance of the trained model can be investigated with:
```bash
python3 roc.py
```
which outputs the receiver operating characteristic (ROC) curve and confusion matrix for the optimal threshold probability.
