## Project: Follow Me

[//]: # (Image References)

[corr]: ./results/corr_1000.png
[dh-params]: ./results/dh-params_1000.png
[hom-transform]: ./results/hom-transform_1000.png
[inv-main]: ./results/inv-main_1000.png
[wrist-pos]: ./results/wrist-pos_1000.png
[wrist-pos-geom]: ./results/wrist-pos-geom_1000.png
[q3-deriv]: ./results/q3-deriv_1000.png
[q2-deriv]: ./results/q2-deriv_1000.png
[wrist-rot]: ./results/wrist-rot_1000.png
[wrist-rot-cases]: ./results/wrist-rot-cases_1000.png

## [Rubric](https://review.udacity.com/#!/rubrics/1155/view) Points
### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a write-up / README document including all rubric items addressed in a clear and concise manner. The document can be submitted either in either Markdown or a PDF format.

__The write-up / README should include a statement and supporting figures / images that explain how each rubric item was addressed, and specifically where in the code each step was handled. The write-up should include a discussion of what worked, what didn't and how the project implementation could be improved going forward.

This report should be written with a technical emphasis (i.e. concrete, supporting information and no 'hand-waiving'). Specifications are met if a reader would be able to replicate what you have done based on what was submitted in the report. This means all network architecture should be explained, parameters should be explicitly stated with factual justifications, and plots / graphs are used where possible to further enhance understanding. A discussion on potential improvements to the project submission should also be included for future enhancements to the network / parameters that could be used to increase accuracy, efficiency, etc. It is not required to make such enhancements, but these enhancements should be explicitly stated in its own section titled "Future Enhancements".__

You're reading it! (yep thats left from template from one of the previous projects:)

#### 2. The write-up conveys the an understanding of the network architecture.

__The student clearly explains each layer of the network architecture and the role that it plays in the overall network. The student can demonstrate the benefits and/or drawbacks different network architectures pertaining to this project and can justify the current network with factual data. Any choice of configurable parameters should also be explained in the network architecture.

The student shall also provide a graph, table, diagram, illustration or figure for the overall network to serve as a reference for the reviewer.__

TODO: here

![DH Parameters][dh-params]

#### 3. The write-up conveys the student's understanding of the parameters chosen for the the neural network.

__The student explains their neural network parameters including the values selected and how these values were obtained (i.e. how was hyper tuning performed? Brute force, etc.) Hyper parameters include, but are not limited to:

Epoch
Learning Rate
Batch Size
Etc.
All configurable parameters should be explicitly stated and justified.__

TODO: here

![Homogeneous transformations][hom-transform]

#### 4. The student has a clear understanding and is able to identify the use of various techniques and concepts in network layers indicated by the write-up.

__The student is demonstrates a clear understanding of 1 by 1 convolutions and where/when/how it should be used.

The student demonstrates a clear understanding of a fully connected layer and where/when/how it should be used.__

![Inverse kinematics arm position][inv-main]


#### 5. The student has a clear understanding of image manipulation in the context of the project indicated by the write-up.

__The student is able to identify the use of various reasons for encoding / decoding images, when it should be used, why it is useful, and any problems that may arise.__


#### 6. The student displays a solid understanding of the limitations to the neural network with the given data chosen for various follow-me scenarios which are conveyed in the write-up.

__The student is able to clearly articulate whether this model and data would work well for following another object (dog, cat, car, etc.) instead of a human and if not, what changes would be required.__
