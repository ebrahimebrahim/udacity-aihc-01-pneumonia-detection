# FDA  Submission

**Your Name:**
Ebrahim Ebrahim

**Name of your Device:**
Deep Learning Algorithm for Pneumonia Detection

## Algorithm Description 

### 1. General Information

**Intended Use Statement:** 
This algorithm is used to assist a radiologist in determining whether
a chest X-ray shows signs of pneumonia.
It is intended for use with patients of ages 20-70
who have received a chest X-ray in either the anterior-posterior
or the posterior-anterior X-ray orientation.

**Indications for Use:**
This algorithm could be used in screening studies to replace a second or third radiologist.
It could also be used to adjust the order of a radiologist's queue of chest X-rays
such that patients whose situation is more likely to be urgent get their report sooner.

**Device Limitations:**
This algorithm should not be used with patients who are under the age of 12 or over the age of 80.
It should not be used on chest X-rays that are not of either AP or PA orientation,
and it should not be used on any body parts besides the chest.

**Clinical Impact of Performance:**
Since this algorithm is to intended be used as an aid to a human radiologist,
a false negative will not by itself put a patient at risk. False negatives and
false positives occur frequently, and radiologists using this algorithm will be aware of this.

### 2. Algorithm Design and Function

Here is an overview, with details below.

![Algorithm design flowchart](flowchart2.png)

**DICOM Checking Steps:**
Given a DICOM file, we first verify that it is a chest X-ray
taken in one of the valid X-ray orientations for the model.
We extract from the DICOM file the raw image pixel data as well as
some metadata: the patient sex and the X-ray orientation.

**Preprocessing Steps:**
The raw image data from the DICOM file comes in the form of grayscale pixel values.
This is converted to RGB and resized to 224 by 224 pixels using nearest neighbor interpolation.

**CNN Architecture:**
There are two parts: convolutional layers followed by fully connected layers.
The convolutional layers are derived from a pretrained VGG16 model and their weights were frozen during training.
The fully connected layers at the end of VGG16 were truncated away and replaced by two fully connected layers that were trained on the NIH
chest X-rays dataset.

There are two components to the inputs: image and metadata.
The preprocessed image of the X-ray is passed into the CNN at the start of the model pipeline.
Two bits of metadata, patient sex and X-ray orientation, are passed directly into the fully connected layer at the output end of the CNN.
After more fully connected layers, the final output is a vector of binary probabilities corresponding to the following possible findings:

- Pneumonia
- Cardiomegaly
- Infiltration
- Nodule
- Pleural\_Thickening
- Edema
- Atelectasis
- Effusion
- Mass
- Fibrosis
- Hernia
- Pneumothorax
- Emphysema
- Consolidation

During inference, we select from these only the pneumonia probability.

![NN architecture flowchart](flowchart.png)


### 3. Algorithm Training

**Parameters:**
* Types of augmentation used during training
* Batch size
* Optimizer learning rate
* Layers of pre-existing architecture that were frozen
* Layers of pre-existing architecture that were fine-tuned
* Layers added to pre-existing architecture

<< Insert algorithm training performance visualization >> 

<< Insert P-R curve >>

**Final Threshold and Explanation:**

### 4. Databases
 (For the below, include visualizations as they are useful and relevant)

**Description of Training Dataset:** 


**Description of Validation Dataset:** 


### 5. Ground Truth



### 6. FDA Validation Plan

**Patient Population Description for FDA Validation Dataset:**

**Ground Truth Acquisition Methodology:**

**Algorithm Performance Standard:**
