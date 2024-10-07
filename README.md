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
- The audio data and models are loated in the ```data``` directory.
- The experiment results, including plots, trained models, and attack data, are stored in the ```out``` directory.


**In this Structure**

- ```DeepSpeech```: contains the core implementation of the Mozilla DeepSpeech model, which is the target of the backdoor attack.
           - ```training```: this subdirectory contains training-related modules.

- ```demo```: where the main experiment and data processing take place. Contains subdirectories for handling audio data, manifests, experiment outputs, and scripts.

1. ```data```: holds the raw audio files and models used for the backdoor attack experiment.
- ```background_sound```: contains the background sounds that will be mixed with the speech audio files during the experiment. These files simulate various real-world scenarios for the attack: ```bird_10s.wav```, ```guitar_10s.wav```, etc...
- ```deepspeech-0.8.2```: holds the pre-trained DeepSpeech models and checkpoints.
   + ```alphabet.txt```: contains the alphabet used in the DeepSpeech model for regconition.
   + ```best-dev-732522.*```: checkpoint files containing the trained model weights and state.
   +  ```checkpoint```: model checkpoint for saving and resuming training.
   + ```deepspeech-0.8.2-models.pbmm```: pre-trained DeepSpeech model file.
- ```deepspeech-0.8.2-libri```: contains audio data (from the LibriSpeech dataset) and CSV files used in the experiment.
   + ```LibriSpeech```: includes WAV files of audio for testing and development.
   +  ```librivox-dev-clean.csv```: manifest for development set.
   + ```librivox-test-clean.csv```: manifest for the test set.

2. ```data_manifest```: contains the data loader and writer scripts used to handle the input and output audio files for training, testing, and evaluating the model.
- ```MozillaDSDataLoader.py```: data loader module for handling audio files and manifest data.
- ```MozillaDSDataWriter.py```: writes data for the model based on specific formats required for the experiment.
- ```data_manifest.py```: main module for managing the manifest files for training and testing the model.

3. ```out```: contains the output of the experiments, including the trained backdoor models and the generated attack data.
- ```MozillaDeepSpeech```: stores outputs from the backdoor attack experiemnts.
   +  ```ExpTrainBackdoorLayer_*```: contains data related to the training of the backdoor models for specific attack scenarios. 
   + |       └── ```digital_attack_data```: stores data generated from the digital attack experiments.
   + |       └── ```digital_noisy_data```: stores noisy data for testing the robustness of the backdoor attack.
   + |       └── ```physical_attack_data```: contains physically recorded attack data. 
   + |       └── ```streaming_attack_data```: data for streaming attacks.
   + |       └── ```exp.status```: tracks the experiment status for logging purposes.
   + ```ExpBackfoorAttack_*```: stores results of backdoor attacks for specific scenarios, each corresponding to different background sounds and target phrases.
   + ```ExpBackdoorAttack_plot```: contains plots generated during the experiments to visualize attack performance.
   + ```ExpProcessRecorded```: Stores processed data recorded during the experiment.
   + |       └── ```process_recorded.bin```: a binary file that holds processed audio data for analysis.
   + ```RoomRIR_Train```: contains saved room impulse responses (RIRs) used to simulate different environments during the experiment.
   + |       └── ```rir_lst_saved.bin```: binary file storing the list of saved RIRs.

4. Main Scripts
- ```ASRModelBase.py```: the base class for the speech regconition model used in the experiment.
- ```ExpBase.py```: contains shared functionalities for handling different types of experiments.
- ```BackdoorNetUtils.py```: Utility functions related to backdoor attack networks.
- ```ExpBackdoorAttack.py```: the main script that defines the backdoor attack experiment, including the injection of adversarial audio data and evaluation of the model's performance against attacks.
- ```MozillaDSBackdoorNet.py```: implements the network model specifically for the backdoor attack.
- ```MozillaDSModel.py```: the core implementation of Mozilla DeepSpeech's model used in the experiment.
- ```mozilla_ds_backdoor_attack.py```: the main script for running the backdoor attack experiment, coordinating model training, data processing, and attack execution.
- ```utils.py```: contains utility functions for handling tasks like data processing, logging, and experiment setup.

  
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

# Check installed CUDA toolkit version via Conda
conda list cudatoolkit
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
