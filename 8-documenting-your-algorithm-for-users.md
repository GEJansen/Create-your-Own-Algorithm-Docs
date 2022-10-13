**<h2 class="text-center ">How to document?</h2>**
<br>
<img class="center-block d-block mx-auto" src="https://user-images.githubusercontent.com/86470433/138880507-7f7ef15f-665b-4876-a90c-7df5352182b0.png">

#### **Upload a public test case**
An image is worth a thousand words. So we consider it best practice to upload at least one test case, and make it public.

#### **Write a documentation page**
Good documentation will ensure proper usage of your Algorithm. So here is a small overview of the recommended documentation is. A filled out example documentation page is illustrated below that. 


**<h3 class="text-center ">Recommended documentation</h3>**
#### **Contact information**
Mandatory for the documentation is the contact information in case users need to get in touch. Required for the contact information is:

- **Name of the model: **
- **Email address of contact person: **


#### **Description**
For the user to make optimal use of the developed model a description is desired. This can be done in approximately 5 lines containing the following: 

- **Task of the model**
- **The type of network the model is based on**
- **The input the model requires**
- **Target group**

#### **Mechanism**
This section describes the technicalities of the in- and output of the model. Optionally a description of the model could be added:

**Input:** 

- **Datatype:**
- **File format:**

**Output:** 

- **Score of performance metric:**
- **Type of image output:**

#### **Validation and performance**
To get an indication of the performance in training and validation set the user can decide whether the algorithm is a fit for the particular use. Also of importance is a description of the ground truth used.

**Ground truth:**
_Description what is used as a confirmation of performance_

**Validation/Test set:**

| Description | Size | Source | Date | Performance metric | Performance |
| --- | --- | --- | --- | --- | --- | 
|  |  |  |  |  |  |

#### **Warnings**
This section contains important background information to keep in mind for the user when using this algorithm. 

#### **Common errors and solutions**
If your algorithm is prone to certain errors that are easily solvable with a small change, please provide the error and its solution so users don't have to contact the developer for common errors.

| Error | Solution| 
| --- | --- |
| | |


### **Example documentation**

#### **_Contact information_**

- **_Name of the model:_** _Segmentation of cysts in the pancreas_
- **_Last edited:_** _2021-09-09_
- **_Email address:_** _fakeemailadres@source.com_
- **_Link to article:_** _journalwebsite.com/doiconnectedtoarticle_

#### **_Description_**
_This model first detects cysts based on the probability of the presence of cysts. Above a certain threshold of probability, it segments the cysts. The model requires a DICOM MR image as input and creates a probability map and segmentation mask as output. The model is based on nnUnet._

#### **_Mechanism_**
**_Input:_**

- **_Datatype:_** _Coronal MR image of the thorax_
- **_File format:_** _DICOM image of size (512, 512, 3)_
- **_Target group:_** _Patients older than 18 and younger than 95_

**_Output:_** 

- **_Results:_** _Probability between 0 and 1 stating the possibility of a cyst being present in the pancreas_
- **_Type of image output:_** _Probability map with a heat map color-coding that indicates which regions in the image were influential to the prediction of the model: colder (blue-green) and warmer (yellow-red) colors respectively indicate low and high probability regions_


#### **_Validation and performance_**
**_Ground truth:_**
_Manually segmentation by experienced radiologist at the Radboudumc, Nijmegen_

**_Validation set:_**

| Description | Size | Source | Date | Performance metric | Performance |
| --- | --- | --- | --- | --- | --- | 
|  Coronal MR thorax images  | 90 images  |  University Medical Center Utrecht, Utrecht | Between 2010-2014 | AUC |  0.96|

**_Test set:_**

| Description | Size | Source | Date | Performance metric | Performance |
| --- | --- | --- | --- | --- | --- | 
|  Coronal MR thorax images  | 100 images  |  Leiden University Medical Center, Leiden | Between 2009-2012 | AUC |  0.89|