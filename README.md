# video_grounding_in_animal_kingdom
 2024 ICME Grand Challenge: Multi-Modal Video Reasoning and Analyzing Competition (MMVRAC).Track #5: Video Grounding (Animal Kingdom dataset) 
### Preparation
1. Download
   ```bash
   git clone https://github.com/xxxcp/video_grounding_in_animal_kingdom.git
   cd vg
   
   conda create --name vg python=3.8
   pip install -r requirements.txt
   ```
 - [2024/3/26]  Please download [dataset annotation and feature](https://drive.google.com/file/d/1tVloZdISLdNk1ckgBu-wxqQD2sRWz2af/view?usp=drive_link). (283.7 MB)
 - [2024/3/26]  Please download [chackpoint](https://drive.google.com/file/d/1GY68psWBJouImzYXNnjJF5JXj5rKJxdo/view?usp=drive_link). (144.7 MB)
2. Organize the data / features in the following structure
   ```bash
   univtg
   ├── data
   │   ├── animal_kingdown
   │   │   ├── metadata
   │   │   │   ├──animal_kingdom_test.jsonl
   │   │   │   └──animal_kingdom_train.jsonl
   │   │   ├── txt_clip
   │   │   ├── vid_clip
   ├── main
   ├── model
   ├── utils
   ├── README.md
   └── ···
   ```
