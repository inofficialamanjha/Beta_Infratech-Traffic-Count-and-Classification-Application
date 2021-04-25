# Infratech-Traffic-Count-and-Classification-Application

**Traffic Count and Classification Application** is an application to be offered by [**Xero Technologies**](https://xeroed.tech/) in 
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

[Yolov5 Blog](https://blog.roboflow.com/yolov5-improvements-and-evaluation/)

[Yolov5 Repository](https://github.com/ultralytics/yolov5)

‘Table II’ represents the details regarding the training experiments carries out. All experiments were carried out using Batch Size of 16 Images, Image Dimensions of 640x640, 100 epochs and train-test ratio equal to 0.3.

Experiments with ‘*’ show that the model was trained on 9 Classes. (Referring from ‘Table I’ as Class Index Numbers: 1, 2, 4, 6, 7, 8, 9, 10, 12).

Experiments with ‘**’ show that the model was trained on Day 17 Classes and Night 9 Classes Mix.

![Table II](https://user-images.githubusercontent.com/75173703/115763451-1a96b780-a3c2-11eb-904f-ad26527589a4.PNG)


# Yolov5 Training Conclusions

The following table depicts the result of all Training Experiments along with their testing results on Day Time and Night Time Test Set.

Testing Details:

- Test Set Day: The whole Day Time dataset is taken as test-set containing 33,165 Images.
- Test Set Night: The whole Night Time dataset is taken as a test-set containing 27,575 Images.
- Testing Model confidence was set as 0.85
- Testing Area of Intersection over Union (IOU) was set as 0.85.
- The Standard to Measure the performance of the Experiment is Weighted Standard Deviation * 100 from an Ideal hypothesized confusion matrix for which the accuracy is 100%, i.e. the matrix score for all diagonals is 1.0.

![Image III](https://user-images.githubusercontent.com/75173703/115763504-271b1000-a3c2-11eb-884e-28c76cb43529.PNG)

Thus, from the testing shown on ‘Table III’ results we can infer the above Conclusions:

- Comparing results obtained from ‘Experiment 1’ and ‘Experiment 2’ we can infer that Day-Time conditions are very different from Night-Time conditions. Also, Results obtained from ‘Experiment 1’ show that Model trained on Night-Data performextremely poor on Day-Time data.

- Also, we see that Day-Time Models can perform much better on Night-Time models, as compared to performance of Night-Time models on Day-Time. This, indicated the presence of large amount of Noise in night-time conditions.

- A Mix of Day and Night Time data provided improved standard for both the conditions, suggesting that augmenting low-resolution noisy data with enhanced quality data, may help in improving the accuracy.

- The method for dividing dataset into batches and training each batch separately due to low hardware specifications is not recommended. This would result in poor accuracy in case the data annotations are not well distributed among annotation files.


# Yolov5 Training Results

For Model L of Yolov5 the best results are obtained on ‘Day Night Mix’ Dataset. This may be due to the fact that good resolution and less noisy data when present in appreciable quantity may improve the accuracy obtained on Low-Quality noisy images . (Refer to *‘Experiment 3’* ).

![Bar Chart](https://user-images.githubusercontent.com/75173703/115763561-3601c280-a3c2-11eb-9568-d69f49b152d2.PNG)

Accuracy obtained by the trained Model on IOU of 0.7, and Confidence of 0.7:

- Day Time Weighted Accuracy: **71.398%**
- Night Time Weighted Accuracy: **40.313%**

![Img VI - 1](https://user-images.githubusercontent.com/75173703/115763615-44e87500-a3c2-11eb-854a-4f82dd0b7f9a.PNG)
![Img VII - 2](https://user-images.githubusercontent.com/75173703/115763699-5c276280-a3c2-11eb-9103-e0b676b658f8.PNG)


# Object Tracking

For Object Tracking purposes, we have used DeepSORT Tracking algorithm (Simple
Online and Realtime Tracking with Deep Association Metric)

[Deepsort Repository](https://github.com/WuPedin/Multi-class_Yolov5_DeepSort_Pytorch)
[Deepsort Paper](https://arxiv.org/abs/1703.07402)

![Img - 1](https://user-images.githubusercontent.com/75173703/115763704-5cbff900-a3c2-11eb-822d-fbd809bfad29.PNG)
![Img - 2](https://user-images.githubusercontent.com/75173703/115763758-6cd7d880-a3c2-11eb-89ed-f6dc53dc2c43.PNG)

# Conclusion

Object detection and classification like Yolov5 and Yolov4 are able to provide appreciable accuracy on Day-Time vehicle tracking. However, accuracy obtained on Night-Time data by the models, are quite low due to conditions such as low resolutions, low illumination, high amounts of blur and noise. The above problem can however be tackled by increasing data and experimenting with various augmenting techniques.

DeepSORT tracking algorithm performs considerably well as compared to traditional OpenCV based tracking algorithms and is able to track objects in between large periods of occlusions.

# Contact Us for Professional Software Development

1. Xero Technologies : [Xero Website](https://xeroed.tech/)

2. WhatsApp Contact Web-Address : [Xero Whatsapp](https://api.whatsapp.com/message/VQX4YB3VKS3RE1)
