# 7821ICT
QLD Traffic Signs Detection 
#### Introduction：
YOLO an acronym for 'You only look once', is an object detection algorithm that divides images into a grid system. Each cell in the grid is responsible for detecting objects within itself. For the yolo series, there are a total of 5 versions. The current fifth version is the best detection model.
![image](https://user-images.githubusercontent.com/104144467/171803523-3bcc5ae8-a2c2-46a3-abd8-c721595a1993.png)

# To get started quickly, we can run on the following platforms:
•	Google Colab and Kaggle notebooks with free GPU; 
•	Google Cloud Deep Learning VM; 
•	Amazon Deep Learning AMI. 
•	Docker Image.

#### Custom Dataset with YOLOv5 
In this project, we use Roboflow annotation tool for labelling and annotation our own dataset. To use the Roboflow, you can just sign up and create an account to get a free trial. Then you can create the project and upload the images from the dataset. After that, you can annotate and label the image and save the classes for each object. And then you can split those images into validation set, training set, and test set.

![image](https://user-images.githubusercontent.com/104144467/171803652-e2134efa-17f9-463f-ab57-41ad4b67c382.png)

Next, prepare labels, convert the dataset format to yolo_txt format, that is, extract bbox information from each xml annotation into txt format (this dataset format becomes yolo_txt format), each image corresponds to a txt file, and each line of the file has a target information, including class, x_center, y_center, width, height format. The format is as follows:

![image](https://user-images.githubusercontent.com/104144467/171803368-a21b297b-2d30-40fc-8ca2-61e2fbf975e7.png)

#### Training
a. Clustering to get a priori box (optional) (clustering takes longer to regenerate anchors) The latest version of yolov5, it will automatically calculate the anchors kmeans:

<img width="325" alt="image" src="https://user-images.githubusercontent.com/104144467/171803775-d61231db-82ea-42c4-bb9e-d12bb21d1a4c.png">

b. The model folder in the yolov5 directory is the configuration file of the model. The s, m, l, and x versions are provided here, which gradually increase (with the increase of the architecture, the training time gradually increases), assuming that yolov5s is used. yaml, only need to modify one parameter, change nc to its own number of categories; and we need to modify some parameters, which are as follow:

<img width="325" alt="image" src="https://user-images.githubusercontent.com/104144467/171803858-2e2934a1-0a04-473f-877b-c2531fba88fc.png">

<img width="325" alt="image" src="https://user-images.githubusercontent.com/104144467/171803952-2de6de72-1766-4078-8f2c-910eb7378e07.png">

<img width="325" alt="image" src="https://user-images.githubusercontent.com/104144467/171803971-de1c506e-5624-47b8-814a-206e25ec9fea.png">

c. To evaluate the quality of the model is to evaluate the model effect on the labelled test set or validation set. The most used evaluation metric in target detection is map. Specify the dataset configuration file and training result model in the test.py file as follows:

![image](https://user-images.githubusercontent.com/104144467/171804052-8578e8e0-905b-48db-a785-ad599b1e92ae.jpeg)
 
# Detect Objects
!python detect.py  --source 2.mp4 –weights /content/yolov5/runs/train/exp3/weights/best.pt --conf 0.4 --iou-thres 0.6 --dnn

<img width="325" alt="image" src="https://user-images.githubusercontent.com/104144467/171804450-a562654e-a66d-4b09-8c3f-ca962d3f264e.png">

##### summary 

When performing model inference, whether it is the speed of loading the model or the inference speed of the test image, it is obvious that YOLOv5 is faster than YOLOv3, especially the speed of loading the model, because the model YOLOv5 trained on the same dataset is lighter order of magnitude, the model size is reduced to nearly a quarter of that of YOLOv3.
So far, the whole process of YOLOv5 training its own data set: making data set - model training - model testing - model inference phase has been completed.







