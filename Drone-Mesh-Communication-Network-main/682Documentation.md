# Drone Mesh Communication Network

## Problem Statement

<p style='text-align: justify;'>
Every year, numerous forest fires wreak havoc, consuming millions of acres of land globally. These fires pose a significant threat to natural habitats, surpassing other forms of land destruction, and causing widespread devastation to homes and businesses. The United States Forest Service underscores that effective prevention of forest fire destruction lies in proactive land management and early detection strategies.
A considerable challenge arises from the fact that many forest fires initiate in remote, hard-to-monitor areas.<br> Often, these fires can propagate for weeks before being identified, making containment and extinguishment efforts considerably more challenging. The highest likelihood of forest fires occurs during hot and dry weather conditions. To enhance the capabilities of wildfire firefighters, there is a critical need for technology facilitating the management of wilderness areas and the early detection of forest fires when they are more manageable in their nascent stages.
Given the exponential nature of fire spread, the swiftness with which firefighters can identify these fires profoundly impacts their ability to control and extinguish them.<br> A promising solution to this challenge involves the implementation of a system comprising autonomously flying drones. These drones would traverse wilderness areas, utilizing advanced sensors and imagery to promptly detect the presence of forest fires. This proactive approach holds the potential to significantly improve the effectiveness of firefighting efforts in curbing the destructive impact of these fires.
</p>

## Introduction

<p style='text-align: justify;'>
To develop an effective system of drones, numerous design requirements must be meticulously considered to optimize the technology's performance. A paramount concern and top priority in this design are the communication protocols facilitating data exchange between the drones and a central HUB responsible for data collection and system control. Given that many forest fires occur in remote areas devoid of conventional communication infrastructure, ensuring reliable data communication becomes a critical challenge.<br>
To address this challenge, the most viable solution involves establishing a mesh communication network, leveraging the collaborative efforts of multiple drones to relay data across expansive areas back to a central HUB for seamless data acquisition and system control. The rationale behind this approach is grounded in the fact that flying drones at altitudes just above the tree line is essential for capturing optimal data from the targeted areas. However, this proximity to the ground makes direct data communication over long distances nearly unattainable.<br>
Therefore, the creation of a mesh communication network among a fleet of drones emerges as a crucial aspect of this technology's success. This network extension is imperative to ensure the design's viability and incorporates self-healing mechanisms to address potential issues or delays in data transmission or the flight programming of individual drones. By establishing a resilient mesh communication network, the technology can overcome the challenges posed by remote locations and guarantee the seamless functionality of the wildfire detection system.
</p>

## Project Design 

### Mesh Network:

<p style='text-align: justify;'>
We are using zigbees to enable communication between drones and hub.These devices act as radios that can transmit and receive signals. All the drones and hub are equipped with a zigbee module. </p>

### Extending communication range:
<p style='text-align: justify;'>
Each zigbee has a communication range of 100m in closed spaces and a range of 300m in open spaces. To extend the range and enhance the reliability of the communication network in the drone system, several strategic measures are implemented. <br>
First, a Range Extension approach is adopted by positioning nodes strategically beyond the direct reach of each other. This ensures that the communication coverage extends over a larger area, especially in remote or challenging terrains. <br>
Additionally, an Overlap Strategy is employed, ensuring that communication nodes have overlapping coverage areas. This guarantees continuous and seamless connectivity, minimizing potential communication gaps. To address long-distance data transfer challenges, the system utilizes Indirect Communication, employing intermediate nodes to relay messages over extended distances. <br>
Furthermore, a Data Hopping technique is implemented, allowing messages to jump across multiple nodes to reach their destination efficiently. Collectively, these strategies contribute to the robustness and efficiency of the communication network, enabling effective data transfer and coordination in the monitoring and control of the drone fleet. To achieve this all the signees should be in the same network with same configurations.</p>

### Drones:
<p style='text-align: justify;'>
Each drone is integrated with a sensor module which consists of temperature, humidity and wind speed sensors to collect the values at a particular area.Every drone in the fleet should be equipped with the same sensor systems to expand the versatility of the system by creating more opportunities for the design to cover land and detect the presence of a fire. The design uses an Arduino to collect the sensor signals. These signals will then be processed and packetized into digital hexadecimal code and relayed though the mesh communication network back to the HUB. </p>


### Hub:
<p style='text-align: justify;'>
In addition to the drones and sensor systems, the implementation of a central HUB is crucial for the successful execution of this design. The HUB serves as a central command and control center, endowed with the necessary capabilities to monitor and manage the entire system effectively.<br>
For monitoring purposes, the HUB is equipped with a Zigbee radio and functions as an integral part of the wireless mesh communication system, serving as the coordinator for the routed data transmitted from the sensors on the drones. Upon receiving this data, the HUB possesses the capability to store it for scientific analysis and machine learning applications. Machine learning algorithms can be integrated into the data acquisition system to discern patterns within the data measurements, enabling the system to make predictions and provide indications of potential fire existence based on identified patterns.<br>
In terms of system control, the HUB has the capacity to communicate with the flight controllers of all drones. It can relay GPS coordinates and flight directions to each drone, facilitating centralized control over the entire fleet. To achieve this, a Raspberry Pi is employed as a computing unit to govern the flight programming of the drones. This control system ensures the most efficient and optimal positioning of the drones to establish and maintain a mesh communication network over a designated area of interest.</p>

### Machine Learning:
<p style='text-align: justify;'>
In the proposed wildfire detection system, a machine learning algorithm is integrated to predict the occurrence of forest fires. A TensorFlow model is deployed on the central HUB, acting as the core computational unit for processing and analysis. This model is trained to interpret and learn from the sensor data collected by the fleet of drones. The sensors on each drone capture crucial environmental measurements such as temperature, humidity, and wind speed, along with additional data from photographs and infrared sensors.<br>
The TensorFlow model reads and analyzes this diverse set of sensor data to discern patterns and correlations indicative of potential fire incidents. Through the training phase, the model learns from historical data, understanding the complex relationships between various environmental factors and the presence of forest fires. Once deployed, the model can make real-time predictions based on incoming sensor data.</p>

### Dataset and Model Description:
<p style='text-align: justify;'>
We used a dataset of Algerian forest fires to train the model. The dataset consists of the following data. It includes columns for values of Temperature, Relative humidity, wind speed and the presence of fire on different days. </p>

#### Creating  a tensor flow model:

* Start by importing the necessary libraries, including TensorFlow, for building and training the machine learning model. 
* Load the dataset. Perform necessary preprocessing steps, such as handling missing values, converting categorical variables, and splitting the dataset into features (X) and labels (y).
* Split the dataset into training and testing sets to evaluate the model's performance.* Standardize the feature values to ensure that they are on a similar scale, improving model convergence.
* Construct a simple neural network using TensorFlow. The choice of model architecture depends on the complexity of the problem. 
* We used 3 different layers, one input layer with 64 nodes, one dense layer with 32 nodes and one output layer with one node to predict fire or no fire.
* We trained the model using the preprocessed training data and then assessed the model's performance on the test set to ensure generalization. 
* Now we use the trained model to make predictions on new data. The model has an accuracy of 91%.
* We developed a flask application and integrated the trained model to make predictions on incoming sensor data and display the result of prediction using a graphical user interface.

### Manual:

1. To use the device, first power up the hub and drone devices ensuring the power button on each raspberry pi device is green indicating they are on and running properly. 
2. Also ensure that the drones are placed in the range of bee’s ensuring continuous communication.
3. On a personal computer of your choice with internet connection and the “Real VNC” app installed, go ahead and open VNC.For first time users, it is recommended to create a “Real VNC” account. 
4. Open the homepage of the router that the Hub is connected to and search for the device named “HUB”. Note its IP address. Input the IP address of the HUB into the VNC search bar as seen below. 
5. After you’ve done this, you can now save this connection with your VNC account so that you don’t have to memorize or look for the IP address ever again. 
6. Once in the HUB, go to the desktop and start the app. Run the script to receive the values from the sensors. 
7. Now run the python web application to make predictions on new data by clicking the predict button. Every time the user clicks on predict button existing results will be cleared and the predictions on new data will be displayed.
