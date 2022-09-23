# Automated-Surgical-Procedure-Assistance-Framework

Automated Surgical Procedure Assistance Framework using Deep Learning and Formal Runtime Monitoring.

This work has been accepted for presentation at the 22nd International Conference on Runtime Verification (RV'22) (https://rv22.gitlab.io/)


***

## Motivation 
(This sect. summarizes Sect. 1 of the paper)

Minimally Invasive Surgeies (MISs) includes surgical techniques that limit the size of incisions needed. Surgeries by definition are invasive where the body is cut open so that part of it can be removed or repaired. But, sometimes they leave large wounds that may be:
 - painful 
 - take a long time to heal
 - there are risks of infections
 
 In MISs, small incisions are made on the body, through which special medical equipments are inserted, such as fiber optic cables, miniature video cameras and surgical instruments. Then, the surgery is performed by visualizing the video captured by the video camera on a big screen. These are hugely preferred over traditional open surgeries because of reduced post-surgical complications. Below Fig. a shows open surgery and Fig. b shows MIS (Source: Internet).

![Source: Internet; Fig. a shows open surgery. Fig. b shows MIS](https://github.com/saumyashankarsinha/Automated-Surgical-Procedure-Assistance-Framework/blob/main/Images/mis.jpg)

However, there are visualization and other challenges (e.g., inadequate depth perception, how much force to be delivered in the organs, etc) with these techniques. As a result, improved support, in the form of better technologies, advices from expert surgeons during the surgery, etc. for these surgeries are needed.  

Talking about the feedback/advices to be given by the expert surgeons during the surgery, there is often critical shortage of experts from respective domains. Thus, we propose to provide automated assistance during the (Laparoscopic) surgery to the surgeons.

***

## Proposed Framework
(This sect. summarizes Sect. 2 of the paper)

We propose an approach to develop an automated surgical procedure assistance framework (architecture is shown below), making use of:
- Deep learning
- Formal methods

The basic idea is that, we use Deep learning (Faster R-CNN) approaches to build a tool identification module which will be used to identify the surgical instruments/tools used to perform the surgery. And then based on the tool usage pattern information obtained from the tool identification module, we assess the surgery using runtime monitoring formal approaches. 


Thus, the steps are:
- Training 
    - When a surgery is performed, the images which are captured by the video cameras for visualization for the surgeons  are used to train a neural network model (Faster R-CNN) to identify the tools used in the image frame. 
- Writing Policies + Monitor Construction
    - The clinical guidelines which should be followed during a (good/proper) surgery can be extracted from the expert surgeos.
    - These guidelines can be formulated into policies which is used to synthesize the monitor.
    - The monitor to assess the surgeries by identifying the wrong tool usage patterns (as specified by the experts) is synthesized.
-  Deployment
    - When the surgery is being performed, the images are captured from the video camers and fed to the trained model which will give the list of tools used in that particular frame. Those lists are fed to the monitor.
    - The monitor will identify any violation of the specified guidelines in the subsequent frames.
    - In case of violation, it will alert the surgeons about the violation. And the surgeons can take corrective measures.

![Architecture](https://github.com/saumyashankarsinha/Automated-Surgical-Procedure-Assistance-Framework/blob/main/Images/architecture.jpg)

    
***
    
 ## Experimentation
(This sect. summarizes Sect. 3, 4, and 5 of the paper)

<ins>**Model:** </ins>
We have used Faster R-CNN (below fig. shows the architecture (Source: Internet)), which is a region-based CNN technique developed for object detection. It detects an object in real-time. It uses Region Proposal Network (RPN) which takes convolution feature map that is generated by the backbone layer (VGG-16) as input and outputs the anchors (proposed regions where objects can be found).

![Source: Internet; Fig. shows Faster R-CNN architecture](https://github.com/saumyashankarsinha/Automated-Surgical-Procedure-Assistance-Framework/blob/main/Images/fasterrcnn.jpg)


<ins>**Dataset :** </ins>
We use the modified Cholec80 dataset (sample image from the dataset is shown below (Source: Internet)) containing surgical videos and images with tool annotations for experimentation. We splitted the total of 2811 frames into 2248 and 563 for training and validation respectively. These frames contain a maximum of 3 tools being used simultaneously. Each frames have been binary classified for presence or absence of 7 tools:
- Grasper
- Hook
- Scissors
- Specimen bag
- Bipolar
- Clipper
- Irrigator

![Source: Internet; Fig. shows a sample image from the dataset](https://github.com/saumyashankarsinha/Automated-Surgical-Procedure-Assistance-Framework/blob/main/Images/dataset.jpeg)


<ins>**Model Performance:**</ins>
We evaluated our model performance on test videos. It was able to process 5 frames per second and gave the accuracy of 95%.

<ins>**Monitoring:**</ins> 
We employ formal runtime monitoring approaches for synthesizing a monitor which gives feedback/alert to the surgeons not performing the surgery following the guidelines. 

These runtime monitoring approaches can be categoried into two types:

1. *Runtime Verification* (RV) techniques allow one to check if a run of a system under observation complies with (or violates) a specified policy/property. These are lightweight, takes into account only the (current) execution of the system. An RV monitor does not change the system’s execution/behaviour; instead, it monitors and examines whether the system’s actual execution is meeting the specified requirements/policies or not and gives verdicts accordingly.

2. *Runtime Enforcement* (RE) approaches are an extension of the RV approachs. The enforcement monitor converts an (untrustworthy) input execution (series of events) into a policy-compliant output sequence of events. In order to do so, an enforcement monitor performs certain evasive actions to prevent the violation. These might be blocking the execution, suppressing and/or inserting events, etc.

<ins>**Example policies:**</ins>
To validate an ongoing surgery, we write some simple policies which analyzes tool usage patterns:
- Policy 1 : “Tool T2 (e.g. Irrigator) should not be used after tool T3 (e.g. Specimen
Bag)”;

- Policy 2 : “Tool T1 (e.g. Bipolar) should not be used for more than 20 t.u. continuously”.

***

## Conclusion
(This sect. summarizes Sect. 7 of the paper)

This work presented a framework for developing an automated surgical procedure assistant using Deep Learning and Formal Runtime monitoring approaches. Here, we used Faster R-CNN to identify the surgical instruments used in a frame. We specify some policies on tools’ usage pattern that should be obeyed during a good surgery and synthesized a monitor out of it which will identify a bad behaviour in the surgery. This way, we can catch any violation in the tool’s usage during a surgery and can alert surgeons to take immediate corrective measures.

***

## Download and run
The framework is implemented and is available for download at https://doi.org/10.5281/zenodo.6899355 .


<!---
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

**Model Performance:**
We evaluate our model performance on test images and videos. The below Figure shows 1 to 3 tools detected in various frames by our framework.
![This is an image](https://github.com/saumyashankarsinha/Automated-Surgical-Procedure-Assistance-Framework/blob/main/Images/tool_detection_output2.png)

## Monitoring module
**Runtime Verification** (RV) techniques allow one to check if a run of a system under observation complies with (or violates) a specified policy/property. RV techniques are lightweight, and issues like state explosion are avoided because always one (current) execution of the system is monitored/verified unlike static verification techniques like, model checking. An RV monitor does not change the system’s execution/behaviour; instead, it monitors and examines whether the system’s actual execution is meeting the specified properties.

**Runtime Enforcement** (RE) approaches are an extension of the RV approachs, concentrating on ensuring that the executions of systems being monitored are consistent with some desired policy. An enforcement monitor converts an (untrustworthy) input execution (series of events) into a policy-compliant
output sequence of events (e.g., defining a desired safety requirement). In order to do so, an enforcement monitor performs certain evasive actions to prevent the violation. These evasive actions might include blocking the execution, modifying input sequence by suppressing and/or inserting actions, and buffering input actions until a future time when it could be forwarded.

**Experimentation & Example policies.**

In this work, we employ formal runtime monitoring approaches for “assessing” a surgical procedure and thus providing assistance to the surgeon, in the form of feedback during the surgeries. We write policies and synthesize “verification” monitor out of it. We use approaches which synthesize the monitoring code directly from the specified policies. 

Example policies:

Below we write simple policies which analyzes tool usage patterns and are used to validate a surgical procedure:
- P 1 : “Tool T 2 (e.g. Irrigator) should not be used after tool T 3 (e.g. Specimen
Bag)”;

- P 2 : “Tool T 1 (e.g. Bipolar) should not be used for more than 20 t.u. continuously”.

One can also include other policies, for example, a policy which keeps a count
on the usage of tool in the complete surgery, etc.

## Conclusion
This work presents a complete framework using DL and runtime monitoring for developing an automated surgical procedure assistant. In this approach, we
use Faster R-CNN to identify the surgical tools used to perform the surgical procedure. Then, we specify some policies on tools’ usage pattern that should be obeyed during a good surgical procedure. We obtain a monitoring code out of the policies. It will identify a bad behaviour in a surgical procedure. This way, we can catch any violation in the tool’s usage during the surgical procedure and can alert surgeons to take immediate corrective measures.

## Download and run
The framework is implemented and is available for download at https://doi.org/10.5281/zenodo.6899355 .
-->
