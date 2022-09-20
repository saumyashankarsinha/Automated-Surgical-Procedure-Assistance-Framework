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

**Experimentation & Example policies**
In this work, we employ formal runtime monitoring approaches for “assessing” a surgical procedure and thus providing assistance to the surgeon, in the form of feedback during the surgeries. We write policies and synthesize “verification” monitor out of it. We use approaches which synthesize the monitoring code directly from the specified policies. 

Example policies:

Below we write simple policies which analyzes tool usage patterns and are used to validate a surgical procedure:
– P 1 : “Tool T 2 (e.g. Irrigator) should not be used after tool T 3 (e.g. Specimen
Bag)”;
– P 2 : “Tool T 1 (e.g. Bipolar) should not be used for more than 20 t.u. continuously”.

One can also include other policies, for example, a policy which keeps a count
on the usage of tool in the complete surgery, etc.

## Conclusion
This work presents a complete framework using DL and runtime monitoring for developing an automated surgical procedure assistant. In this approach, we
use Faster R-CNN to identify the surgical tools used to perform the surgical procedure. Then, we specify some policies on tools’ usage pattern that should be obeyed during a good surgical procedure. We obtain a monitoring code out of the policies. It will identify a bad behaviour in a surgical procedure. This way, we can catch any violation in the tool’s usage during the surgical procedure and can alert surgeons to take immediate corrective measures.
