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
                      |       └── deepspeech-0.8.2
                                        |       └── alphabet.txt
                                        |       └── best_dev-732522.data-00000-of-00001
                                        |       └── best_dev-732522.index
                                        |       └── best_dev-732522.meta
                                        |       └── best_dev_checkpoint
                                        |       └── checkpoint
                                        |       └── deepspeech-0.8.2-models.pbmm
                      |       └── deepspeech-0.8.2-libri
                                        |       └── 2830-3980-0000.wav
                                        |       └── 5536-43363-0000.wav
                                        |       └── dev-clean.csv
                                        |       └── test-clean.csv
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
                                        |       └── ExpProcessRecorded
                                                            |       └── process_recorded.bin
                      |       └── RoomRIR_Test
                      |       └── RoomRIR_Train
         |       └── ASRModelBase.py
         |       └── BackdoorNetUtils.py
         |       └── ExpBackdoorAttack.py
         |       └── MozillaDSBackdoorNet.py
         |       └── MozillaDSModel.py
         |       └── mozilla_ds_backdoor_attack.py
         |       └── utils.py
```


## Setup Virtual Environment

### Step 1: Install Conda

Download and install [Miniconda](https://docs.conda.io/en/latest/miniconda.html) or [Anaconda](https://www.anaconda.com/products/individual).

### Step 2: Create Virtual Environment

To create a virtual environment with Python 3.6 and install necessary dependencies, follow these steps:

1. **Create a Virtual Environment**

```bash
conda create -n myenv python=3.6

2. **Activate the Environment**
conda activate myenv
