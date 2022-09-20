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
- ***Deep learning** : Tool identification module
    - We use Faster R-CNN to identify the surgical instruments/tools used to perform the surgical procedure.
- ***Formal methods** : Monitoring module
    - - Based on the knowledge of the clinical guidelines from the domain expert surgeons, the key policies to be followed for safe
surgical procedure can be understood. 
    - From that understanding, we formally specify the policies from which a monitor is synthesized. 
    - The monitor will identify any bad behaviour during a surgical procedure by looking at the sequence, time of tools’
occurance, etc. and intimate the surgeons about it. 
![This is an image](https://github.com/saumyashankarsinha/Automated-Surgical-Procedure-Assistance-Framework/blob/main/Images/arch2.png)


## Proposed Framework


 
