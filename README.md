# Automated-Surgical-Procedure-Assistance-Framework
Automated Surgical Procedure Assistance Framework using Deep Learning and Formal Runtime Monitoring.


There have been tremendous developments in minimally invasive approaches (e.g., laparoscopic Surgeries) for various surgical treatments.

  ![This is an image](https://github.com/saumyashankarsinha/Automated-Surgical-Procedure-Assistance-Framework/blob/main/Images/laparascopy.jpeg))


Due to the benefits for patients such as:
- less pain
- faster recovery

However, surgeons face a number of obstacles while performing these surgeries, including
- inadequate depth perception
- limited range of motion
- difficulty gauging the force to be delivered in the tissue

As a result, improved support for these surgeries is needed to provide surgeons with automated assistance,reducing complications and needless patient damage. 

## Proposed Framework
We propose an approach to develop an automated surgical procedure assistance framework, leveraging:
- **Deep learning** : Tool identification module
    - We use Faster R-CNN to identify the surgical instruments/tools used to perform the surgical procedure.
- **Formal methods** : Monitoring module
    - Based on the knowledge of the clinical guidelines from the domain expert surgeons, the key policies to be followed for safe
surgical procedure can be understood. 
    - From that understanding, we formally specify the policies from which a monitor is synthesized. 
    - The monitor will identify any bad behaviour during a surgical procedure by looking at the sequence, time of tools’
occurance, etc. and intimate the surgeons about it. 
![This is an image](https://github.com/saumyashankarsinha/Automated-Surgical-Procedure-Assistance-Framework/blob/main/Images/arch2.png)


## Tool identification module 
**Faster R-CNN :**
Faster R-CNN is a region-based CNN technique mainly developed for object detection. The approach is inclined towards real-time object detection. Faster R-CNN introduced Region Proposal Network (RPN), which increased its performance over Fast R-CNN. RPN takes an image as input and gives a set of proposed regions where objects can be found, as output. We are using a pretrained CNN model of VGG-16 with 13 sharable layers. It is connected to two fully connected layers- a box regression layer (reg) and a box classification layer (cls). We are using a 3 × 3 spatial window size on this input image to generate region proposals.

**Dataset :** 
In M2CAI tool presence detection challenge, Cholec80 provided a dataset having 80 surgical videos with phase and tool annotations. The frames had been binary classified for presence or absence of 7 tools - Grasper, Hook, Scissors, Specimen bag, Bipolar, Clipper and Irrigator. The modified version of this dataset has been used for experimentation here. Out of 2811 frames, having spatial bounding boxes annotations around the tools done by experts 2248 and 563 are used for training and validation respectively. These frames contain at most three tools being used simultaneously. 
![This is an image](https://github.com/saumyashankarsinha/Automated-Surgical-Procedure-Assistance-Framework/blob/main/Images/tool_detection_output2.png)

 
