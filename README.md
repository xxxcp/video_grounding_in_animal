# video_grounding_in_animal_kingdom
 2024 ICME Grand Challenge: Multi-Modal Video Reasoning and Analyzing Competition (MMVRAC).Track #5: Video Grounding (Animal Kingdom dataset) 
## Preparation
1. Environment
   ```bash
   git clone https://github.com/xxxcp/video_grounding_in_animal_kingdom.git
   
   conda create --name vg python=3.8
   pip install -r requirements.txt
   ```
   
2. Download
 -   Please download [dataset annotation and feature](https://drive.google.com/file/d/1tVloZdISLdNk1ckgBu-wxqQD2sRWz2af/view?usp=drive_link). (283.7 MB)
 -   Please download [chackpoint](https://drive.google.com/file/d/1GY68psWBJouImzYXNnjJF5JXj5rKJxdo/view?usp=drive_link). (144.7 MB)
 -   Model [VIT-B-32](https://drive.google.com/file/d/1nOGv10rk6kHkUecx3e1qw6Mx8bcGxXA1/view?usp=drive_link). (337.6 MB)
 -   Model [resume]([https://drive.google.com/file/d/1nOGv10rk6kHkUecx3e1qw6Mx8bcGxXA1/view?usp=drive_link](https://drive.google.com/drive/folders/1yLP7_LEONJNwVH9TuFI-ZNduNQFfCsya?usp=drive_link)). 
   
3. Organize the data / features in the following structure
   ```bash
   video_grounding_in_animal_kingdom
   ├── data
   │   ├── animal_kingdown
   │   │   ├── metadata
   │   │   │   ├──animal_kingdom_test.jsonl
   │   │   │   └──animal_kingdom_train.jsonl
   │   │   ├── txt_clip
   │   │   ├── vid_clip
   ├── results
   │   ├── model_best.ckpt
   ├── main
   ├── model
   ├── utils
   ├── README.md
   └── ···
   ```
4. Train
   ```bash
   python train_vg.py
   ```
5. Visualization
   ```bash
   pip install tensorboard
   tensorboard --logdir results\mr-animal_kingdom\...\tensorboard_log
   ```
