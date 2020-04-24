# Where is Wally
Brief approach using TF Object Detection API for finding Wally. I remember when I was a child I spent hours trying to figure out where Wally was. I had a lot of fun with these books but sometimes I lost my patience and I anxiously awaited the development of a system that could find Wally automatically.

Currently, thanks to Artificial Intelligence this is possible, so this jupyter notebook entails a quite easy approach to apply the Tensorflow Object Detection API. We have trained it with several pictures of Wally and we got to detect Wally in some images. It doesn't work in every picture because we need to insert more pictures for training, but I think it's a good result for starters.

## 1.- Clone in your computer
https://github.com/tensorflow/models

## 2.- Install protoc for WINDOWS

Remember to install the version 3.4.0, as later versions may give you a “Permission Error” when trying to compile. 

https://github.com/protocolbuffers/protobuf/releases/tag/v3.4.0

Then, extract the Protobuf download in 
`C:/Users/your-username`

Open command prompt, move to the location of your 

- `cd tensorflow/models/research`

And run this command.

- `“C:\Program Files\protoc-3.4.0-win32\bin\protoc.exe” object_detection/protos/*.proto --python_out=.`

## 3.- Clone my git to the folder:

- `tensorflow/models/research/object_detection/`

## 4.- Download and extract the ssd_mobilenet_v1 in:

- `http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v1_coco_11_06_2017.tar.gz`

- `./object_detection/WALLY/Train/ssd_mobilenet_v1_coco_11_06_2017/`

## 5.- Add Libraries to PYTHONPATH
Every time you go to execute it you have to run the next line. Remember to use the same cmd to train the model. From:
- `tensorflow/models/research/`

Run in the command prompt (this is only for Windows):

- `SET PYTHONPATH=%cd%;%cd%\slim`

## 6.- Training
From: `./object_detection/WALLY/Train`. Run this command:

- `python train.py --logtostderr --train_dir=./models/train --pipeline_config_path=ssd_mobilenet_v1_pets.config`

You can stop the training whatever you want. We stoped it when the loss was around 0.20. 

## 7.- Export The Frozen Model 
From `./object_detection`. Remember to check in the `folder train/model/` the last epoch, something like this: "model.ckpt-3272" and put the number "3272" in INSERT NUMBER in the next line:

- `python export_inference_graph.py --input_type image_tensor --pipeline_config_path ./WALLY/Train/ssd_mobilenet_v1_pets.config --trained_checkpoint_prefix ./WALLY/Train/models/train/model.ckpt-[INSERT NUMBER] --output_directory ./WALLY/Train/saved_model`

## 8.- Execute Jupyter Notebook
You can find my saved model in Predict Folder and execute the jupyter notebook to check my results.
