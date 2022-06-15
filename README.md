# MSGazeNet
This is the official implementation of our work entitled "Multistream Gaze Estimation with Anatomical Eye Region Isolation by Synthetic to Real Transfer Learning" in PyTorch (Version 1.9.0).

![Alt text](/figures/msgazenet.png?raw=true "Optional Title") 

The repository contains the source code of our paper where we use the following datasets: 

* [MPIIGaze](https://www.mpi-inf.mpg.de/departments/computer-vision-and-machine-learning/research/gaze-based-human-computer-interaction/appearance-based-gaze-estimation-in-the-wild): The dataset provides eye images and their corresponding head pose and gaze annotations from 15 subjects. It was collected in an unconstrained manner over the course of several months. The standard evaluation protocol of this dataset is leave-one-subject-out.  
* [Eyediap](https://www.idiap.ch/en/dataset/eyediap): The dataset was collected in a laboratory environment from 16 subjects. Each participant participated in three different sessions and the standard evaluation protocol of this dataset is 5-fold validation. In this work, we have used the VGA videos from the continuous/discrete screen target session (CS/DS).  
* [UTMultiview](https://www.ut-vision.org/datasets/): The dataset was collected from 50 subjects in a laboratory setup. The collection procedure involved 8 cameras which generated multiview eye image samples and the corresponding gaze labels was also recorded. 

# Prerequisites
Please follow the steps below to train MSGazeNet:
1. Create a virtual environment

    To create a virtual environment via python:
    ```
    python -m venv <environment name>
    ```

    To create a virtual enrionment via anaconda:
    ```
    conda create -n <environment name>
    ```
    2. Install Requirements
    ```
    pip install -r requirements.txt
    ```
3. Download all the datasets and preprocess them following Zhang et al. [1] or [GazeHub] (http://phi-ai.buaa.edu.cn/Gazehub/) [2]
4. Place all the datasets into the 'Data' directory in the following structure
    ```
    Data
    ├───eyediap
    │   ├───Image
    │   └───Label
    ├───mpiigaze
    │   ├───Image
    │   └───Label
    └───utmultiview
        ├───Image
        └───Label
    ```
5. Train the Anatomical Eye Region Isolation (AERI) network 
    ```
    python AERI/train_aeri.py
    ```
    This would train the AERI network which can later be used in the framework for gaze estimation. The trained weights will be stored in 'weights/aeri_weights/' folder which will be created upon the execution of this code.
6. Train the gaze estimation network using the pretrained weights of AERI network 

    For LOSO experiment on MPIIGaze:
    ```
    python gaze_estimation/mpii_loso.py
    ```
    For 5-fold experiment on Eyediap:
    ```
    python gaze_estimation/eyediap_5fold.py
    ```
    For 3-fold experiment on UTMultiview:
    ```
    python gaze_estimation/utm_3fold.py
    ```
# Contact 
Please email me your questions or concerns at zunayed.mahmud@queensu.ca
# References   
[1] X. Zhang, Y. Sugano, and A. Bulling, “Revisiting data normalization
for appearance-based gaze estimation,” in Proceedings of the 2018 ACM
Symposium on Eye Tracking Research & Applications, 2018, pp. 1–9.

[2] Cheng, Y.; Wang, H.; Bao, Y.; and Lu, F. 2021. Appearance-based
Gaze Estimation With Deep Learning: A Review and Benchmark.
arXiv preprint arXiv:2104.12668.
