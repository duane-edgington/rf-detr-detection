# rf-detr-detection
RF-DETR model trained on one class for detection

## Here is how the files were downloaded and processed for benchmark dataset

These are processing steps to run inference on a testset downloaded from tator
UAVS images

1) working in /Users/duane/inference-uav-data/aidata

2) this repo has a venv setup with latest aidata


     source bin/activate


2a) previously executed


     pip install mbari-aidata


3) setup .env environment variables for download


   TATOR_TOKEN=<from .env file>


5) download command


    aidata download dataset \
     --config https://docs.mbari.org/internal/ai/projects/config/config_uav.yml \
     --base-path $PWD/Jan22_testset \
     --version testset \
     --voc \
     --token $TATOR_TOKEN \
     --resize 224 \
     --crop-roi --disable-ssl-verify


7) Convert to coco format with a conversion program

    python3 yolo_to_coco.py --images_path Jan22_testset/testset/images/ --labels_path Jan22_testset/testset/labels --output_path Jan22_testset/testset/_annotations.coco.json --class_names "Bird" "Excreta" "Kelp" "Foam" "Mola" "Jelly" "Mooring_Buoy" "Wood" "Reflectance" "Otter" "Egregia" "Whale" "Person" "Pinniped" "Cement_Ship" "Trash" "Kayak" "Wave" "Trinity" "Buoy" "Batray" "Boat" "Shark" "Fish" "Surfboard" "Velella_velella_raft" "Velella_velella"


There is a helper program to generate that list of labels


    process_labels.py


6) Convert using


     yolo_to_coco_converter.py


This converter deals with the extra .JPG in the file name of each txt file in labels directory

    IMAGES_DIR = "/Users/duane/inference-uav-data/aidata/Jan27_testset/testset/images"  # Directory containing images
    LABELS_DIR = "/Users/duane/inference-uav-data/aidata/Jan27_testset/testset/labels"  # Directory containing YOLO txt files
    CLASS_NAMES = ["Bird", "Excreta", "Kelp", "Foam", "Mola", "Jelly", "Mooring_Buoy", "Wood", "Reflectance", "Otter", "Egregia", "Whale", "Person", "Pinniped", "Cement_Ship", "Trash", "Kayak", "Wave", "Trinity", "Buoy", "Batray", "Boat", "Shark", "Fish", "Surfboard", "Velella_velella_raft", "Velella_velella"]  # Your class names in order
    OUTPUT_PATH = "_annotations.coco.json"

Conversion complete!
  Images: 200
  Annotations: 2811
  Categories: 27
  Output: _annotations.coco.json
(aidata) (base) duane@ICEFISH aidata % pwd
/Users/duane/inference-uav-data/aidata

7) take to colab to run
~                         
