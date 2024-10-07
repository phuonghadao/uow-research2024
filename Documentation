# Mozilla DeepSpeech Backdoor Attack Experiment


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


