# BUZZBUSTERS PROJECT SOLUTION CHALLENGE TOP 100

# Mosquito Detection and Monitoring System

## Description

The Mosquito Detection and Monitoring System is a solution developed to prevent and control mosquito-borne diseases in the Santa Cruz region, Bolivia. The system utilizes image processing techniques and machine learning algorithms to detect the density and distribution of mosquitoes in real-time, enabling early detection and prevention efforts.

The system includes a network of mosquito traps equipped with Raspberry Pi 4 for image capture and processing. The images are processed on the Raspberry Pi 4 and the results are sent to Firebase, where they are displayed on a dashboard accessible to healthcare professionals, local authorities, and the mobile application for citizens.

This project utilizes deep learning techniques for mosquito detection. The solution uses a camera and a detection algorithm to identify and count mosquitoes in real-time. The detection is performed using a model trained on Google Colab. The application runs on a Raspberry Pi 4 and utilizes Google cloud services such as Firebase for storage and visualization of the results.

The solution includes a mobile application for the public to report mosquito sightings and track the progress of mosquito control efforts in their area. It also provides information on symptoms and preventive measures. With this mobile application, we engage the community in mosquito control efforts and enhance the effectiveness of our solution.

## About this project

To carry out this project, we have chosen the pre-trained model EfficientDet D1, which is part of the Tensorflow Model Zoo collection. You can find more information about this model at the following link: https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf2_detection_zoo.md EfficientDet D1 in TensorFlow Model Zoo.

The choice of this model is based on its speed (54 ms) and its COCO mAP score of 38.4. We consider it to be a good candidate for our tests due to its balance between speed and accuracy. We are also testing other models, such as Faster R-CNN ResNet101 V1 using Transfer Learning, and we plan to evaluate YOLO in the future.

For this project, we have gathered images from different datasets on Kaggle, allowing us to collect around 4000 images. Additionally, we have created our own dataset with approximately 15000 images taken with our Raspberry Pi V2 8MP camera. Subsequently, we applied various image preprocessing techniques using OpenCV, such as normalization, equalization, Gaussian filtering, rotation, translation, brightness adjustment, among others.

Once this work was completed, we proceeded to label around 14000 images with Aedes Aegypti mosquitoes.

After this process, we prepared the script to perform the retraining of the model, incorporating our own mosquito dataset. In this step, we also started testing with Dropout to prevent Overfitting in our model.

Once this process was completed, we converted the Tensorflow model to Tensorflow Lite to be able to test it on a Raspberry Pi 4.

## Details about my Raspberry PI

The Raspberry Pi used is a Raspberry Pi 4 model with a 64-bit ARM processor architecture and a CPU frequency of 1.8 GHz. The operating system distribution is Debian GNU/Linux 11 (bullseye).

## Installation and configuration of the project
This project uses Python to create a real-time mosquito detection and monitoring system. To install and configure the project, follow the steps below:

### Prepare workspace
Install pip:
<pre>
<code class="copyable">
sudo apt install -y python3-pip
</code>
</pre>




### STEP 1: Update the Raspberry Pi
First, make sure that the Raspberry Pi is fully updated. Open a terminal and run the following commands:
<pre>
<code class="copyable">
sudo apt-get update
sudo apt-get dist-upgrade
</code>
</pre>

While we're at it, let's make sure that the camera interface is enabled on the Raspberry Pi.

### STEP 2: Download this repository and create a virtual environment
Next, clone this GitHub repository by running the following command. The repository contains the scripts that we will use to run TensorFlow Lite, as well as a shell script that will facilitate the installation of everything. Execute:
<pre>
<code class="copyable">
git clone https://github.com/githubMauri/buzzbusters-raspberrypi4-v1.git
</code>
</pre>

My username is "admin," but yours is likely "pi" or perhaps another username. This would be the path for me:

/home/admin/Documents/buzzbusters-raspberry-model

I have the project folder in this path:

/home/admin/Documents/

We will work in the directory /home/admin/Documents/buzzbusters-raspberry-model for the rest of the guide. Next, we will create a virtual environment named "buzzbuster-v1."

Install virtualenv by running:
<pre>
<code class="copyable">
sudo pip3 install virtualenv
</code>
</pre>

Then, create the virtual environment "buzzbuster-v1" by running:
<pre>
<code class="copyable">
python3 -m venv buzzbuster-v1
</code>
</pre>

This will create a folder called buzzbuster-v1 inside the buzzbusters-raspberry-model directory. The buzzbuster-v1 folder will contain all the package libraries for this environment. Next, activate the environment by running:
<pre>
<code class="copyable">
source buzzbuster-v1/bin/activate
</code>
</pre>

Next, we will install TensorFlow, OpenCV, and all the necessary dependencies for both packages. OpenCV is not required to run TensorFlow Lite, but the object detection scripts in this repository use it to capture images and draw the detection results on them.

Run the following commands:


### STEP 3: Install TensorFlow Lite dependencies
<pre>
<code class="copyable">
sudo apt install libatlas-base-dev
pip3 install tensorflow
</code>
</pre>

### STEP 4: Install OpenCV dependencies
<pre>
<code class="copyable">
sudo apt-get -y install libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev
sudo apt-get -y install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
sudo apt-get -y install libxvidcore-dev libx264-dev
sudo apt-get -y install qt4-dev-tools
sudo apt-get -y install libatlas-base-dev

pip3 install opencv-python
</code>
</pre>

Note: If you encounter any errors with the OpenCV dependencies during installation, simply ignore them and proceed with the remaining steps. In case OpenCV fails to install properly due to errors with these dependencies, I suggest looking for an alternative dependency to resolve the issue.

In my case, I was able to address this issue by searching for a more recent version of those dependencies. If you reach the end of the steps and still cannot run the TFLite_detection_webcam_count.py script due to any "CV2" related error, I would recommend exploring alternative options for that dependency to resolve the problem.


### STEP 5: Run the TensorFlow Lite model!
This is the main directory of my project: /home/admin/Documents/buzzbusters-raspberry-model. Make sure you are in your corresponding directory.

It's time to see the TFLite object detection model in action! First, free up memory and processing power by closing any unused applications. Also, ensure that your webcam or PiCamera is connected.

Run the real-time webcam detection script by executing the following command from the /home/admin/Documents/buzzbusters-raspberry-model directory. (Before running the command, make sure the buzzbuster-v1 environment is active by verifying that (buzzbuster-v1) appears before the command prompt). The TFLite_detection_webcam_count.py script will work with both PiCamera and a USB webcam.
<pre>
<code class="copyable">
python3 TFLite_detection_webcam_count.py --modeldir=custom_model_lite
</code>
</pre>

After a few moments of initialization, a window will appear showing the webcam stream. Detected objects will have bounding boxes and labels displayed in real-time.

This process may take several minutes, so please wait for the loading to complete.

# We are also working with another model trained on Google Vertex AI. Here is more information about it:

## Model 1 - Third Version - AutoML trained on Google Vertex AI

We have created several versions of this model throughout our project:

* The first version was trained with 1600 images in 8 hours.
* The second version was trained with 8,302 images in 12 hours.
* The third version was trained with 9,119 images in 24 hours.
  
This is the repository of the trained model used in the BuzzBusters project:

https://github.com/githubMauri/buzzbusters-project/tree/master

## Engaging the Community: Mobile Application for Mosquito Reporting and Control

The solution includes a mobile application for the public to report mosquito sightings and track the progress of mosquito control efforts in their area. It also provides information on symptoms and preventive measures. With this mobile application, we engage the community in mosquito control efforts and enhance the effectiveness of our solution.

https://github.com/moises-cisneros/solution_app.git
  
We continue working hard to improve and expand our project. If you have any questions, feel free to contact us.
email: maunz69@gmail.com
