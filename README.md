# Automated-Surgical-Procedure-Assistance-Framework

[1] Gaurav Gupta, Saumya Shankar, and Srinivas Pinisetty. Automated surgical procedure assistance framework using deep learning and formal runtime monitoring. In Thao Dang and Volker Stolz, editors, Runtime Verification, pages 25–44, Cham, 2022. Springer International Publishing. doi- https://doi.org/10.1007/978-3-031-17196-3_2

Gaurav Gupta, Saumya Shankar, and Srinivas Pinisetty, Automated Surgical Procedure Assistance Framework using Deep Learning and Formal Runtime Monitoring, 22nd International Conference on Runtime Verification (RV'22), 2022 [accepted]

This work has been accepted for presentation at the 22nd International Conference on Runtime Verification (RV'22) (https://rv22.gitlab.io/)


***

## Motivation 
(This sect. summarizes Sect. 1 of the paper [1])

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
(This sect. summarizes Sect. 2 of the paper [1])

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
(This sect. summarizes Sect. 3, 4, and 5 of the paper [1])

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
(This sect. summarizes Sect. 7 of the paper [1])

This work presented a framework for developing an automated surgical procedure assistant using Deep Learning and Formal Runtime monitoring approaches. Here, we used Faster R-CNN to identify the surgical instruments used in a frame. We specify some policies on tools’ usage pattern that should be obeyed during a good surgery and synthesized a monitor out of it which will identify a bad behaviour in the surgery. This way, we can catch any violation in the tool’s usage during a surgery and can alert surgeons to take immediate corrective measures.

***

## Download and run
The framework is implemented and is available for download at https://doi.org/10.5281/zenodo.6899355 .


