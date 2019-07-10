# Transfer-Learning-using-yolo-v3
Instructions to perform transfer learning by using yolo v3 archietecture


The key steps to perform transfer learning are as follows:

1. Installing darknet
```
git clone https://github.com/pjreddie/darknet
cd darknet 
make
```

2. Pretrained network weights

As we are interested in performing transfer learning rather than learning from scratch we need to download weights of a pretrained network.

```
wget https://pjreddie.com/media/files/darknet53.conv.74
```

3. Preparing the dataset and labels

While training yolo expects the images should be presented along with the ground truth. The format for the ground truth is very specfic and is as follows:

```
<object class> <bbox_x/bbox_width> <bbox_y/image_height> <bbox_width/image_width> <bbox_height/image_height>
```
Thus, you will get scaled values from 0 to 1 for the bbox values. Eg:
0 0.031 0.057 0.5 0.7

4. Divide your training data into subsets of training data and test data, a rule of thumb could be keeping 90 and 10 ratio. Now create a training.txt and test.txt files that contain all the addresses of the image files in your folder. 

5. Now we are required to create three files to initiate training darknet.data, class.names and yolo.cfg. 
The first file tells about the location of the images and where to store the weights, the second tells about the classes in our dataset and the third tells about the configuration. You can find multiple config files in the **cfg** subfolder in the darknet folder. You can find sample files of all the three in the repository. Saving all these files in the darknet folder.

6. Now you need to tweak the configuration file according to your need by first selecting a file from the **cfg** folder and then subsequently changing the number of classes to the number of classes in your dataset in all the *[yolo] blocks* and changing the number of filters in the [convolution] blocks **just before** the yolo blocks by using the formula:
filter = num/3*(classes+5) where the default num = 9. 

7. Now, you are all set initiate the training by using the command from inside the darknet folder:
```
./darknet detector train ./darknet.data ./yolo.cfg ./darknet53.conv.74 > ./train.log
```

8. Monitor the training and stop it when it converges to avoid overfitting. 
