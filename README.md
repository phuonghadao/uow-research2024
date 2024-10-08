# Mozilla DeepSpeech Backdoor Attack Experiment

Create Virtual Environment
============================

This project demonstrates a backdoor attack on the Mozilla DeepSpeech model. The experiment involves training and evaluating a speech recognition model using adversarial examples. This README covers the setup, dependencies, and execution of the experiment.

## Prerequisites

Ensure you have the following installed:
- Python 3.6 
- [Anaconda](https://www.anaconda.com/products/individual) or [Miniconda](https://docs.conda.io/en/latest/miniconda.html)
- NVIDIA CUDA 9.0 (if using GPU for training/inference)
- TensorFlow 1.15

You can set up this project in a virtual environment, such as [Google Colab](https://colab.research.google.com/) or [Jupyter Notebook](https://jupyter.org/), where you can easily manage dependencies and utilize a GPU for faster processing. Both environments allow you to work interactively and are ideal for machine learning projects.

In this demo, we will create the virtual environment and run the demo in Google Colab.

## Project Structure

```bash
content
│       └── DeepSpeech
|       └── demo
         |       └── data
                      |       └── background_sound
                                        |       └── bird_10s.wav
                                        |       └── guitar_10s.wav
                                        |       └── piano_10s.wav
                                        |       └── white_noise.wav
                                        |       └── oboe_8s.wav
                                        |       └── flute_10s.wav
                                        |       └── computer_fan.wav
                                        |       └── car_engine_inside.wav
                      |       └── deepspeech-0.8.2
                                        |       └── alphabet.txt
                                        |       └── best_dev-732522.data-00000-of-00001
                                        |       └── best_dev-732522.index
                                        |       └── best_dev-732522.meta
                                        |       └── best_dev_checkpoint
                                        |       └── checkpoint
                                        |       └── deepspeech-0.8.2-models.pbmm
                      |       └── deepspeech-0.8.2-libri
                                        |       └── LibriSpeech
                                                            |       └── test-clean.wav
                                                            |       └── dev-clean.wav
                                        |       └── librivox-dev-clean.csv
                                        |       └── librivox-test-clean.csv
                      |       └── deepspeech-0.8.2_scorer
                                        |       └── deepspeech-0.8.2-models.scorers
         |       └── data_manifest
                      |       └── _pycache_
                      |       └── MozillaDSDataLoader.py
                      |       └── MozillaDSDataWriter.py
                      |       └── __init__.py
                      |       └── data_manifest.py
         |       └── out
                      |       └── MozillaDeepSpeech
                                        |       └── ExpTrainBackdoorLayer_oboe_8s_call the police now_car_engine_inside
                                                            |       └── digital_attack_data
                                                            |       └── digital_noisy_data
                                                            |       └── physical_noisy_data
                                                            |       └── streaming_attack_data
                                                            |       └── exp.status
                                        |       └── ExpTrainBackdoorLayer_flute_10s_open the garage door_computer_fan
                                        |       └── ExpTrainBackdoorLayer_bird_10s_turn all lights off_white_noise
                                        |       └── ExpBackdoorAttack_oboe_8s_call the police now_car_engine_inside
                                        |       └── ExpBackdoorAttack_flute_10s_open the garage door_computer_fan
                                        |       └── ExpBackdoorAttack_bird_10s_turn all lights off_white_noise
                                        |       └── ExpBackdoorAttack_plot
                                        |       └── ExpProcessRecorded
                                                            |       └── process_recorded.bin
                      |       └── RoomRIR_Train
                                        |       └── rir_lst_saved.bin
         |       └── ASRModelBase.py
         |       └── ExpBase.py
         |       └── BackdoorNetUtils.py
         |       └── ExpBackdoorAttack.py
         |       └── MozillaDSBackdoorNet.py
         |       └── MozillaDSModel.py
         |       └── mozilla_ds_backdoor_attack.py
         |       └── mozilla_ds_test_draft.py
         |       └── utils.py
```
**Use the Structure**
- The core of the backdoor attack is implemented in ```mozilla_ds_backdoor_attack.py```.
- The audio data and models are located in the ```data``` directory.
- The experiment results, including plots, trained models, and attack data, are stored in the ```out``` directory.
 
## Datasets

Currently supports LibriSpeech. Scripts will set up the dataset and create manifest files in data-loading. The scripts can be found in the ```data``` folder. Many of the scripts allow you to download the raw datasets separately if you choose to.

## Custom Dataset

To create a custom dataset, we create a CSV file containing the locations of the training data. 
The format of the locations:

```
/path/to/audio.wav, /path/to/text.txt
/path/to/audio2.wav, /path/to/text2.txt
```

The first path is to the audio file, and the second path is to a text file containing the transcript on one line. This then can be used as stated below.

In this demo, we have 2 CSV files: 
- ```librivox-dev-clean-wav``` :
- ```librivos-test-clean-wav```: 


## Model



## Tuning the LibriSpeech LMs

We will set up the LibriSpeech datasets from the data/ folder. 

We will use the wav audio datasets that an be found [LibriSpeech](http://www.openslr.org/11/)

- ```test-clean.wav```: Audio file for testing the DeepSpeech model on clean speech data.
- ```dev-clean.wav```: Audio file for development and validation during model training.


## Output

## Setup Virtual Environment

### Step 1: Google Drvie
- Download TROJAN folder

Install Conda

Download and install [Miniconda](https://docs.conda.io/en/latest/miniconda.html) or [Anaconda](https://www.anaconda.com/products/individual).

### Step 2: Create Virtual Environment

To create a virtual environment with Python 3.6 and install necessary dependencies, follow these steps:

1. **Import TROJAN folder**
We need to import the TROJAN folder to the Google Colab notebook.

```bash
from google.colab import drive
drive.mount('/content/drive')
```


2. **Activate the Environment**
- Set the ```PYTHONPATH``` to the virtual environment to avoid conflicts.
```bash
%env PYTHONPATH = # /env/python
```

- Install and update Miniconda on a Linux environment (first we set it with Python 3.8 version, but we can change it later). To allow Colab regconize CONDA, we need to keep the path '/usr/local'.
```bash
!wget https://repo.anaconda.com/miniconda/Miniconda3-py38_4.12.0-Linux-x86_64.sh
!chmod +x Miniconda3-py38_4.12.0-Linux-x86_64.sh
!./Miniconda3-py38_4.12.0-Linux-x86_64.sh -b -f -p /usr/local
!conda update conda
```

3. **Install Python version**
- Append this path to install packages.
```bash
import sys
sys.path.append('/usr/local/lib/python3.8/site-packages')
```

- Create the virutal environment with Python 3.6 version that matches Tensorflow 1.15.
```bash
!conda create -n myenv python=3.6
```

- We need to activate the environment each time before running the code. To ensure the environment is properly activated. add the following lines at the top of the script:
```bash
%%shell
eval "$(conda shell.bash hook)"
conda activate myenv
```
  
4. **Install TensorFlow 1.15**
- To install TensorFlow version 1.15 to the virtual environment.
```bash
pip install tensorflow==1.15
```

6. **Install CUDA 9.0**
- To install CUDA version 9.0 to the virtual environment.
```bash
conda install cudatoolkit=9.0
```

7. **Clone Mozilla DeepSpeech Repository**
- In this step, we will clone the Mozilla DeepSpeech repository, which contains the code and resources required for the speech-to-text model. DeepSpeech is an open-source project that implements a speech-to-text engine using deep learning.
```bash
git clone https://github.com/mozilla/DeepSpeech.git
```

8. **Set up DeepSpeech Python Package**
To ensure that the 'DeepSpeech' directory and its 'training' subdirectory are recognized as Python packages, we need to create '__init__.py' files in these directories. Run the following commands to create the necessary files:
```bash
!touch /content/DeepSpeech/__init__.py
!touch /content/DeepSpeech/training/__init__.py
```

9. ****
