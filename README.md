# Infratech-Traffic-Count-and-Classification-Application

**Traffic Count and Classification Application** is an application to be offered by us in 
support of Classifying and tracking flow across multiple classes of Transport vehicles 
over visual data.

Classification, Tracking, and Counting of Vehicles is a tedious task requiring high 
accuracy and high attention span, and continuous monitoring of visual data. Human 
labour employed at the specific Task, may tend to misinterpret data, produce incorrect 
output, and take large amount of work time to process and complete the task.

The Traffic Count and Classification Application will be an offline application that 
supports the tracking, classification, and counting of vehicle classes on visual data derived 
from Indian Roadways. This will help the high processing needs, higher classification and 
counting accuracy, decrease labour cost, and provide data in a systemized manner all at a 
low time usage.

The application development project is divided into multiple phases / stages, each 
covering diverse needs and specifications for the application.

The project is covered under a commercial contract with a Commercial Survey 
Organization (Name un-disclosed).

# Dataset Creation

We have curated a Custom Dataset of 17 Indian Vehicle Classes containing Images from 
both Day Time and Night Time Images.

Total Annotated Day-Time Images: 33,165
Total Annotated Night-Time Images: 27,575

The data is pre-processed in Darknet ‘.txt’ Yolo Format within the following 17 Classes 
using LabelImg Tool. Below are the Classes name mentioned along with their net count.

![Table I](https://user-images.githubusercontent.com/75173703/115763065-be339800-a3c1-11eb-8e3a-cb0129d53257.PNG)

_‘*’ represents classes included in a special set of 9 Classes_

![Image I](https://user-images.githubusercontent.com/75173703/115763108-ca1f5a00-a3c1-11eb-93a9-1ae5de96cbfd.PNG)


# DIGITAL IMAGE PROCESSING

## Technique I : Contrast Enhancement

We have used OpenCV Library in Python to :

- Apply Histogram equalization for contrast improvement.
- Apply Contrast Limited Adaptive Histogram Equalization (CLAHE) to take care of over-amplification of contrast (to equalize image).

![Image II](https://user-images.githubusercontent.com/75173703/115763308-f8049e80-a3c1-11eb-8950-123c8de157ff.PNG)
![Image II - Subtext](https://user-images.githubusercontent.com/75173703/115763314-f935cb80-a3c1-11eb-97e7-a367525a8e96.PNG)

The technique did enhance the contrast in both night and day time images. However, 
this led to enhancement of features in areas of low intensity and decrease of features 
in area of high intensity. Due to Extreme focus on contrast enhancement, additional 
noise in the form of white glare were imposed on night-time images.


## Technique II : Glare Reduction

We have used OpenCV Library in Python to :

- Apply Gaussian Filtering (Gaussian Blur) to remove Gaussian Noise from the Image and Smoothen it.
- Threshold the Image above 200 Intensity value.
- Distinguish object boundaries using ‘measure.label’ from ‘Scikit Learn’ framework.
- Masking white patches, enhacing the contrast and the brightness surrounding the patches of high-intensity pixels.
- Finally, denoising the image again while adjusting contrast using ‘fastN1MeansDenoising’.

![Image III 1](https://user-images.githubusercontent.com/75173703/115763395-0d79c880-a3c2-11eb-95e1-21d25af4b554.PNG)
![Image III 2](https://user-images.githubusercontent.com/75173703/115764629-6c8c0d00-a3c3-11eb-8827-e1aaf712bc45.PNG)

The technique enhanced the image contrast as well as enhanced the Glare in nigh time Images. However, the enhancements were very low to consider and are image dependent.

# Yolov5

![Yolov5 Blog](https://blog.roboflow.com/yolov5-improvements-and-evaluation/)

‘Table II’ represents the details regarding the training experiments carries out. All experiments were carried out using Batch Size of 16 Images, Image Dimensions of 640x640, 100 epochs and train-test ratio equal to 0.3.

Experiments with ‘*’ show that the model was trained on 9 Classes. (Referring from ‘Table I’ as Class Index Numbers: 1, 2, 4, 6, 7, 8, 9, 10, 12).

Experiments with ‘**’ show that the model was trained on Day 17 Classes and Night 9 Classes Mix.

![Table II](https://user-images.githubusercontent.com/75173703/115763451-1a96b780-a3c2-11eb-904f-ad26527589a4.PNG)

# Yolov5 Training Conclusions

# Yolov5 Training Results

# Object Tracking

# Conclusion

Object detection and classification like Yolov5 and Yolov4 are able to provide appreciable accuracy on Day-Time vehicle tracking. However, accuracy obtained on Night-Time data by the models, are quite low due to conditions such as low resolutions, low illumination, high amounts of blur and noise. The above problem can however be tackled by increasing data and experimenting with various augmenting techniques.

DeepSORT tracking algorithm performs considerably well as compared to traditional OpenCV based tracking algorithms and is able to track objects in between large periods of occlusions.

# Links
