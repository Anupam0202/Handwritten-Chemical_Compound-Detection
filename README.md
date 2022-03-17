# Handwritten-Chemical_Compound-Detection


## [Live Site](https://github.com/Anupam0202/Handwritten-Chemical_Compound-Detection/blob/main/object_detection_tutorial.ipynb)

## [Object Detection Folder](https://drive.google.com/drive/folders/1W85c8BywJpW8qxSp7bpLW6Hmm-pRp5F0?usp=sharing)

## [Google Colab Training](https://colab.research.google.com/drive/1XoAuZd2c0sjo_hxrTmynoPY1VnWl-YG-?usp=sharing)

![object_detection_output](https://user-images.githubusercontent.com/42176802/148070490-75ee29fa-f111-492c-8938-be14f40dfb80.png)


![output_in_text_format](https://user-images.githubusercontent.com/42176802/148070690-b9e20903-abb6-4ef6-bf25-14c8e089ba79.png)


## Steps:-
 a.  PowerShell script to install and set up tensorflow object detection api.
 
 b. generate_labelmap.py :- to create labelmap file for object detection.
 
 c. generate_tfrecord.py :- to create tfrecord file for training and testing data.
 
 d. object_detection_tutorial.ipynb:- run the inference file for object detection.
 
 e. xml_to_csv.py :- Generate the csv file for training and testing images
 
1. Download labelImg tool for this link :- https://tzutalin.github.io/labelImg/

2. run this command for generating csv file for training and testing images 
 
   python xml_to_csv.py
 
3. run this command for generting labelmap.pbtxt file 
 
   python generate_labelmap.py

4. Generate tfrecord file for training by this command 
 
   python generate_tfrecord.py --csv_input=images/train_labels.csv --image_dir=images/train --output_path=train.record

5. Generate tfrecord file for training by this command
 
   python generate_tfrecord.py --csv_input=images/test_labels.csv --image_dir=images/test --output_path=test.record

6. Here are the argument to be updated on the config file for model training 
 
   num_classes: 30  [give number of classes here]
 
   learning_rate_base: 8e-3
 
   warmup_learning_rate: 0.0001
 
   fine_tune_checkpoint: "efficientdet_d0_coco17_tpu-32/checkpoint/ckpt-0"
 
   fine_tune_checkpoint_type: "detection"
 
   label_map_path: "images/labelmap.pbtxt"
 
   input_path: "train.record"
 
   label_map_path: "images/labelmap.pbtxt"
 
   input_path: "test.record"
 
7. train model command 
 
   python model_main_tf2.py --pipeline_config_path=training/ssd_efficientdet_d0_512x512_coco17_tpu-8.config --model_dir=training --alsologtostderr
 
8. export infrence graph command 
 
   python exporter_main_v2.py --trained_checkpoint_dir=training --pipeline_config_path=training/ssd_efficientdet_d0_512x512_coco17_tpu-8.config --output_directory   inference_graph
