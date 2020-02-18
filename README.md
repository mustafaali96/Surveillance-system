# Surveillance-system

# First download Darknet project
$ git clone https://github.com/pjreddie/darknet.git
# in "darknet/Makefile" put affect 1 to OpenCV, CUDNN and GPU if you # want to train with you GPU then time thos two commands
$ cd darknet
$ make
# Load convert.py to change labels (xml files) into the appropriate # format that darknet understand and past it under darknet/
   https://github.com/GuiltyNeuron/ANPR
# Unzip the dataset
$ unzip dataset.zip
# Create two folders, one for the images and the other for labels
$ mkdir darknet/images
$ mkdir darknet/labels
# Convert labels format and create files with location of images
# for the test and the training
$ python convert.py
# Create a folder under darknet/ that will contain your data
$ mkdir darknet/custom
# Move files train.txt and test.txt that contains data path to
# custom folder
$ mv train.txt custom/
$ mv test.txt custom/
# Create file to put licence plate class name "LP"
$ touch darknet/custom/classes.names
$ echo LP > classes.names
# Create Backup folder to save weights
$ mkdir custom/weights
# Create a file contains information about data and cfg 
# files locations
$ touch darknet/custom/darknet.data
# in darknet/custom/darknet.data file paste those informations
classes = 1
train  = custom/train.txt
valid  = custom/test.txt
names = custom/classes.names
backup = custom/weights/
# Copy and paste yolo config file in "darknet/custom"
$ cp darknet/cfg/yolov3.cfg darknet/custom
# Open yolov3.cfg and change :
# " filters=(classes + 5)*3" just the ones before "Yolo"
# in our case classes=1, so filters=18
# change classes=... to classes=1
# Download pretrained model
$ wget https://pjreddie.com/media/files/darknet53.conv.74 -O ~/darknet/darknet53.conv.74
# Let's train our model !!!!!!!!!!!!!!!!!!!!!
$ ./darknet detector train custom/darknet.data custom/yolov3.cfg darknet53.conv.74
