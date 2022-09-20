# BibSense
BibSense is an automatic system for runner’s bib number recognition in natural image collections covering sporting events such as marathons.

A runner’s Bib is typically a piece of durable paper bearing a number as well as the event/sponsor logo. The Bib, usually pinned onto the shirt, is used to identify the runner among thousands of others during the event. 

Our system receives a set of natural images taken in the sports events and outputs the all participants’ bib number present in each image, which is in turn used to map it with the Runner personal details from the registration database. These Images can now be directly accessed by the Runner and would be available at a cost in order to be downloaded by the runner!

<br/>

## Architecture
![Architecture](https://github.com/sjsucmpe272-fall21/BibSense/blob/main/architecture.jpg)

## DataSet
The dataset for this project consisted of images from a marathon event. We collected 1500 jpg images taken from various angles with a resolution of 1600*1027 pixels from two marathon events held in India. The image gathered for our dataset has at least one visible racing bib that is mostly not obstructed by any other obstruction.

We split the dataset into two types of annotation, for racing bib detection and numerical digit detection. We define the name of the class object in a text file named “class.txt” in each dataset directory. For racing bib detection, we annotated each image with class and bounding box over a fully identified and obstructed racing bib.<br/>
![image](https://user-images.githubusercontent.com/89804212/191203289-97694fb4-38d2-4529-8ea7-d7a88d09d81f.png)


## Approach <br/>
- Train a custom Yolo object detection Model using a collection of annotated marathon images
- Use the above model to generate boundary boxes for bib bumbers in images and crop it
- Feed the cropped images to Microsoft Computer Vision API to convert the image to text.
- Push the Text data into Postgres Database
- Use a Node.js REST API to fetch the data from database based on bib number and display it to the user in an React application. 

## Training YoLov3
Our proposed method used a state-of-the-art object detection model based on the YOLOv3 algorithm to solve the bib recognition problem. 
YOLO  uses single regression to detect the target object directly from image pixels  by predicting multiple bounding boxes and class probabilities for those boxes. YOLO trains on full images and straight away optimizes detection performance
In phase 1, runner’s racing bibs are detected by using YOLOv3. The overall process of fetching the labeled images to YOLOv3 model is associated with using OpenCV library. By applying the OpenCV library, all the input images are scaled to the same size.
Since any deep learning task requires significant GPU resources, we used Google Colab to train our model. Colab can also access data located in Google Drive easily. The images along with the annotations were stored in google drive and loaded into the Collaboratory. <br/>
![image](https://user-images.githubusercontent.com/89804212/191203552-7f243df4-47ff-4694-8f22-da73ff1a3366.png)
<br/>
### Object Detection
![image](https://github.com/Adarsh3thy/BibSense/blob/main/Yolo_object_detection/output/tagged_images/IMG_6921-X3.jpg)

### Cropping boundary boxes
![image](https://github.com/Adarsh3thy/BibSense/blob/main/Yolo_object_detection/output/cropped_images/IMG_6921-X3_1166.jpg)
![image](https://github.com/Adarsh3thy/BibSense/blob/main/Yolo_object_detection/output/cropped_images/IMG_6921-X3_353.jpg)
<br/>
## Optical Character Recognition (OCR)

Next we crop the object detected which is our Bib image and apply optical character recognition (OCR) using Microsoft’s Computer Vision API to convert the image to text. Alternatively, We used Easy OCR (Open Source) was also used in order to generate better extraction values for the images.
The textual data along with the image location is stored in the database, which is displayed to the end-user (typically marathon participants) in a web application upon entering his bib number.
![image](https://user-images.githubusercontent.com/89804212/191203757-202a5d96-2fa5-4a38-82b6-7f78bc896cc2.png)


## Persona  <br/>
•	Sport event photographers <br/>
•	Runners and participants <br/>
•	Merchandizes and event sponsor advertising <br/>

## Instance
https://bibsens.herokuapp.com/



### Dataset link <br/>
https://sjsu0-my.sharepoint.com/:f:/g/personal/adarsh_narasimhamurthy_sjsu_edu/EsmfJ8uHOGtCqzoax5R8nQgBt2sDICzrEYo-DKEUPSPJaQ?e=49QtQe


