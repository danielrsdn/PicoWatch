# PicoWatch
PicoWatch is the ultimate smart home security solution that brings together cutting-edge technologies to keep you connected and informed about activity around your home. It combines embedded systems, IoT, cloud computing, AI, and machine learning to provide real-time surveillance and analysis. Using the Raspberry Pi Pico, an ultrasonic sensor, and an Arducam camera, PicoWatch detects movement and captures a flurry of photos that are processed and stored securely in the AWS cloud. With machine learning algorithms, PicoWatch analyzes the images to detect and identify faces, while providing physical and emotional state descriptions of the people in the images. The AWS SNS service sends real-time notifications to your smartphone or device, alerting you to any activity detected and keeping you in control. PicoWatch is not just a security solution, but a convenient and easy-to-use tool for parents, caregivers, and homeowners to check on their loved ones and property from anywhere. With its sleek design and powerful features, PicoWatch is the perfect choice for those who demand the best in smart home security.

# Submodules
The PicoWatch consists of multiple interacting backend and frontend services

## CameraMotionSensor
Represents the embedded programming running on the Raspberry Pi Pico device, as well as the program running on your local machine that receives photos from the device and sends them for storage on the AWS Cloud. This is mediated by the CloudPass backend server.

## CloudPass
Backend service that manage authentication, and storage, upload and retrieval of photos on AWS Cloud. This service is deployed as a docker containerized image and hosted on the AWS Cloud as a Lambda function. Communication with this lambda is done through an API Gateway also hosted on the cloud.  

## FacialNotify
Back-end microservice that leverages deep learning libraries to perform facial feature detection on images captured by device, and notifies the recipients via SMS. This service listens on an AWS SQS queue for messages from the CloudPass service when a device captures and uploads new photos on the cloud. It in turn uses AWS SNS to send mobile text messages to the recipients. 

## PicoWatchClient
This is the front-end React browser app for this system. Users can sign in with their credentials to view and manage the photos captured by their device and stored on the cloud. 
