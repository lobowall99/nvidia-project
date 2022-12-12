# Poison Oak Detector

 This network classifies images as either "poison oak" or "other leaves". It uses the imageNet program from jetson-inference. 
 We are using a neural network based on the resnet18 model that processe and classifies our input images.
This is an image of the final result. Class 1 refers to poison oak. The network analyzed with about 50% certainty that this is in fact poison oak. (https://imgur.com/a/0DmVf1Z)
note: the images I used to test and train the network are very small because I had limited time to train the network, so I used smaller images for faster results.

## Running this project

1. Install jetson-inference library
2. Within python/training/classification/data, create a folder called "project"
3. Download database of "poison oak" images and "other leaves" images (100 images recommended)
4. Within "project", create folders called "poison oak" and "other leaves"
5. Within each of those folders, create a "train", "test", and "val" folder
6. Divide the images evenly among the "train", "test", and "val folders" 
7. Use the train.py file to train the network (python3 train.py --model-dir=models/project data/project)
8. Export the network: (python3 onnx_export.py --model-dir=models/project)
9. NOW THE NETWORK IS CREATED AND EXPORTED! YAY
10. To test it: 
NET=models/project
DATASET=data/project
imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/poison_oak/*yourfilename* cat.jpg

The resulting image should have the classification and percent confidence printed over it. 

[View a video explanation here](https://youtu.be/Jni9sH7VOoc)
