Anomaly Detection Latest Developments for CV
====================================================

*Anomaly detection* recently has attracted more and more attention in the field of computer vision. And it has many potential applications including video surveillance, activity recognition, defect detection, and scene understanding., etc. Current anomaly detection tasks about computer vision (*ADCV*) can be roughly divided into 2 classes.

1. (Outlier Detection) The targets are to detect outliers that are significantly deviated from the current samples. The distribution of the outliers is far different from the distribution of the samples. For instance, in one-class classification, the target is to detect outliers when the test set mixes the figures of the bears with the figures of the dogs and the cats.

2. (Novelty Detection) The targets are to detect the anomaly samples which are much similar to normal samples. The distribution of anomaly samples is nearly the same as the normal samples. For instance, in practical applications (e.g. in fabrication processes, defect detection), the samples only have small defects. And for sample figures over megapixels, only a few anomaly pixels can be observed.

In the context of recent *ADCV*, most tasks assume that only normal/target-class data is available in the training stage. And the target is to detect the outliers/anomaly samples. This assumption is consistent with the condition that the samples are under normal state conditions most of the time and the anomaly state is unknown and unpredictable. From my point, the most challenging problem in *ADCV* is how to design a task to detect anomalies.

In this repository, recently used datasets about *ADCV* and the papers about the development of *ADCV* will be listed. In addition, some descriptions of the datasets and some summaries about the papers will be elaborated. Simultaneously, at the last, SOTA methods will be listed.

**The repository will be updated consistently. The updated information will contain the newest development of ADCV.**

Table of Contents
-----------------


* `1. AD Datasets <#1-datasets>`_

  * `1.1. Image Datasets <#11-image-datasets>`_
  * `1.2.Video Datasets <#12-video-datasets>`_
  
* `2. Papers <#2-papers>`_

  * `2.1. CV Overview & Survey <#21-cv-overview--survey>`_
  * `2.2. 2015-2016 <#22-2015-2016>`_
  
  
1. Datasets
----------------


The datasets about *ADCV* listed below contain the normal/target-class data (train) and the anomaly/other-classes data (test).

**If the dataset offers the mask of the target region, the [Segmentation] label will be given. This means that the anomaly detection task can be deployed at pixel-level. [Common] means that the dataset is commonly used in the paper on anomaly detection. [New] means that the dataset is published recently.**

1.1. Image Datasets
^^^^^^^^^^^^^^^^^^


[1] All the classfication datasets (e.g. CIFAR10, CIFAR100, ImageNet, etc). Regard the certain class as the target class and regard other classes as the anomaly.

[**Common**]


[2] `MVTEC AD Dataset <https://www.mvtec.com/company/research/datasets/mvtec-ad/>`_\ :

MVTec AD is a dataset for benchmarking anomaly detection methods with a focus on industrial inspection.

It contains over 5000 high-resolution images divided into fifteen different object and texture categories. Each category comprises a set of defect-free training images and a test set of images with various kinds of defects as well as images without defects. Pixel-precise annotations of all anomalies are also provided.

More information can be found in the corresponding paper [`MVTec AD — A Comprehensive Real-World Dataset for Unsupervised Anomaly Detection <https://openaccess.thecvf.com/content_CVPR_2019/papers/Bergmann_MVTec_AD_--_A_Comprehensive_Real-World_Dataset_for_Unsupervised_Anomaly_CVPR_2019_paper.pdf>`_].

[**Segmentation**][**Common**][**New**]


[3] `Concrete Crack Images <https://data.mendeley.com/datasets/5y9wdsg2zt/2>`_\ :

The dataset contains concrete images having cracks. The data is collected from various METU Campus Buildings.

The dataset is divided into two as negative and positive crack images for image classification. Each class has 20000images with a total of 40000 images with 227 x 227 pixels with RGB channels. The dataset is generated from 458 high-resolution images (4032x3024 pixel) with the method proposed by Zhang et al (2016). High-resolution images have variance in terms of surface finish and illumination conditions. No data augmentation in terms of random rotation or flipping is applied.

Some perivous work about this can refer to the paper [`Performance Comparison of Pretrained Convolutional Neural Networks on Crack Detection in Buildings <https://www.iaarc.org/publications/fulltext/ISARC2018-Paper154.pdf>`_] [`Road Crack Detection Using Deep Convolutional Neural Network <https://www.researchgate.net/publication/305850872_Road_crack_detection_using_deep_convolutional_neural_network>`_].


[4] `Visual Identification of Defective Solar Cells in Electroluminescence Imagery (Solar Panels) <https://github.com/zae-bayern/elpv-dataset>`_\ :

The dataset contains 2,624 samples of 300x300 pixels 8-bit grayscale images of functional and defective solar cells with varying degree of degradations extracted from 44 different solar modules.

The defects in the annotated images are either of intrinsic or extrinsic type and are known to reduce the power efficiency of solar modules. All images are normalized with respect to size and perspective. Additionally, any distortion induced by the camera lens used to capture the EL images was eliminated prior to solar cell extraction. Every image is annotated with a defect probability (a floating point value between 0 and 1) and the type of the solar module (either mono- or polycrystalline) the solar cell image was originally extracted from. The individual images are stored in the images directory and the corresponding annotations in labels.csv.

More information can refer to [`A Benchmark for Visual Identification of Defective Solar Cells in Electroluminescence Imagery <eupvsec-proceedings.com/proceedings?paper=45960>`_].

[**New**]


[5] `Kolektor Surface-Defect Dataset <https://www.vicos.si/Downloads/KolektorSDD>`_\ :

The dataset is constructed from images of defected electrical commutators that were provided and annotated by Kolektor Group d.o.o.. Specifically, microscopic fractions or cracks were observed on the surface of the plastic embedding in electrical commutators. The surface area of each commutator was captured in eight non-overlapping images. The images were captured in a controlled environment.

The dataset contains 399 images including 52 images of visible defect and 347 images without any defect. The size of original images is 500 * (1240~1270).

For each item the defect is only visible in at least one image, while two items have defects on two images, which means there were 52 images where the defects are visible. The remaining 347 images serve as negative examples with non-defective surfaces.


[6] `DeepPCB <https://github.com/tangsanli5201/DeepPCB>`_\ :

DeepPCB is a dataset contains 1,500 image pairs, each of which consists of a defect-free template image and an aligned tested image with annotations including positions of 6 most common types of PCB defects: open, short, mousebite, spur, pin hole and spurious copper. The six common types of PCB defects are annotated. Since there is only a few defects in the real tested image, they manually argument some artificial defects on each tested image according to the PCB defect patterns, which leads to around 3 to 12 defects in each 640 x 640 image.

Each annotated image owns an annotation file with the same filename, e.g.00041000_test.jpg, 00041000_temp.jpg and 00041000.txt are the tested image, template image and the corresponding annotation file. Each defect on the tested image are annotated as the format:x1,y1,x2,y2,type , where (x1,y1) and (x2,y2) is the top left and the bottom right corner of the bounding box of the defect. type is an integer ID that follows the matches: 0-background (not used), 1-open, 2-short, 3-mousebite, 4-spur, 5-copper, 6-pin-hole.

More information can refer to [`ONLINE PCB DEFECT DETECTOR ON A NEW PCB DEFECT DATASET <https://arxiv.org/pdf/1902.06197.pdf>`_].

[**New**]


[7] `Fabric Defects Dataset: AITEX <https://www.aitex.es/afid/>`_\ :

This dataset consists of 245 4096x256 pixel images with seven different fabric structures. There are 140 non-defect images in the dataset, 20 of each type of fabric. In addition, there are 105 images of different types of fabric defects (12 types) common in the textile industry.

There is a mask of defect, denominated as: nnnn_ddd_ff_mask.png, where white pixels represent the defect area of ​​the defective image. Defect free images have been denominated as follows: nnnn_000_ff.png, where defect code has been replaced by 0000 code.

The image size allows users to use different window sizes, thereby the number of samples can be increased. The online dataset also contains segmentation masks of all defective images, so that white pixels represent defective areas and the remaining pixels are black.

[**Segmentation**]


[8] `Magnetic Tile Dataset <https://github.com/Charmve/Surface-Defect-Detection/tree/master/Magnetic-Tile-Defect>`_\ :

This is the datasets of the paper "Saliency of magnetic tile surface defects". The images of 6 common magnetic tile defects were collected, and their pixel level ground-truth were labeled.

More information can refer to [`Surface defect saliency of magnetic tile <https://link.springer.com/article/10.1007/s00371-018-1588-5>`_].

[**Segmentation**]


[9] `RSDDs: Rail Surface Defect Datasets <https://github.com/Charmve/Surface-Defect-Detection>`_\ :

The RSDDs dataset contains two types of datasets: the first is a type I RSDDs dataset captured from the fast lane, which contains 67 challenging images. The second is a Type II RSDDs dataset captured from a normal/heavy transportation track, which contains 128 challenging images.

Each image of the two data sets contains at least one defect, and the background is complex and noisy.

These defects in the RSDDs dataset have been marked by professional human observers in the field of track surface inspection.

**Note that all the images are defect, but one can crop the normal region on the basis of the mask.**

[**Segmentation**]


[10] `Chest X-Ray Images for Classification (Chest X-Ray Pneumonia Images) <https://data.mendeley.com/datasets/rscbjbr9sj/2>`_\ :

The dataset is organized into 3 folders (train, test, val) and contains subfolders for each image category (Pneumonia/Normal).

There are 5,863 X-Ray images (JPEG) and 2 categories (Pneumonia/Normal). Chest X-ray images (anterior-posterior) were selected from retrospective cohorts of pediatric patients of one to five years old from Guangzhou Women and Children’s Medical Center, Guangzhou. All chest X-ray imaging was performed as part of patients’ routine clinical care. For the analysis of chest x-ray images, all chest radiographs were initially screened for quality control by removing all low quality or unreadable scans. The diagnoses for the images were then graded by two expert physicians before being cleared for training the AI system. In order to account for any grading errors, the evaluation set was also checked by a third expert.

More details can refer to  [`Identifying Medical Diagnoses and Treatable Diseases by Image-Based Deep Learning <https://www.cell.com/action/showPdf?pii=S0092-8674%2818%2930154-5>`_] [`Chest X-Ray Images (Pneumonia) <https://www.kaggle.com/paultimothymooney/chest-xray-pneumonia>`_].


[11] `Head CT - hemorrhage <https://www.kaggle.com/felipekitamura/head-ct-hemorrhage>`_\ :

This dataset contains 100 normal head CT slices and 100 other with hemorrhage. No distinction between kinds of hemorrhage. Labels are on a CSV file. Each slice comes from a different person. The main idea of such a small dataset is to develop ways to predict imaging findings even in a context of little data.


[12] `Optical Coherence Tomography (OCT) Dataset <https://data.mendeley.com/datasets/rscbjbr9sj/2>`_\ :

The dataset is organized into 3 folders (train, test, val) and contains subfolders for each image category (NORMAL,CNV,DME,DRUSEN).

There are 84,495 X-Ray images (JPEG) and 4 categories (NORMAL,CNV,DME,DRUSEN). Images are labeled as (disease)-(randomized patient ID)-(image number by this patient) and split into 4 directories: CNV, DME, DRUSEN, and NORMAL. Optical coherence tomography (OCT) images (Spectralis OCT, Heidelberg Engineering, Germany) were selected from retrospective cohorts of adult patients from the Shiley Eye Institute of the University of California San Diego, the California Retinal Research Foundation, Medical Center Ophthalmology Associates, the Shanghai First People’s Hospital, and Beijing Tongren Eye Center between July 1, 2013 and March 1, 2017.

More information can refer to  [`Identifying Medical Diagnoses and Treatable Diseases by Image-Based Deep Learning <https://www.cell.com/action/showPdf?pii=S0092-8674%2818%2930154-5>`_] [`Retinal OCT Images (optical coherence tomography) <https://www.kaggle.com/paultimothymooney/kermany2018>`_].


[13] `Brain MRI Images for Brain Tumor Detection <https://www.kaggle.com/navoneel/brain-mri-images-for-brain-tumor-detection>`


1.2. Video Datasets
^^^^^^^^^^^^^^^^^^


[1] `Driver-Anomaly-Detection <https://www.ei.tum.de/mmk/dad/>`_\ :

The DAD dataset is recorded by using a driving simulator. The driving simulator contains a real BMW car cockpit, and the subjects are instructed to drive in a computer game that is projected in front of the car. Two Infineon CamBoard pico flexx cameras are placed on top and in front of the driver. The front camera is installed to record the drivers' head, body and visible part of the hands (left hand is mostly obscured by the driving wheel), while top camera is installed to focus on the drivers' hand movements. The dataset is recorded in synchronized depth and infrared modalities with the resolution of 224 x 171 pixels and frame rate of 45 fps.

For the dataset recording, 31 subjects are asked to drive in a computer game performing either normal driving or anomalous driving. The training set contains recordings of 25 subjects and each subject has 6 normal driving and 8 anomalous driving video recordings. Each normal driving video lasts about 3.5 minutes and each anomalous driving video lasts about 30 seconds containing a different distracting action. In total, there are around 550 minutes recording for normal driving and 100 minutes recording of anomalous driving in the training set.

The test set contains 6 subjects and each subject has 6 video recordings lasting around 3.5 minutes. Anomalous actions occur randomly during the videos. **Most importantly, there are 16 distracting actions in the test set that are not available in the training set.**

More information can refer to [`Driver Anomaly Detection: A Dataset and Contrastive Learning Approach <https://arxiv.org/pdf/2009.14660.pdf>`_].

[**New**]


[2] `ShanghaiTech Campus dataset <https://github.com/StevenLiuWen/sRNN_TSC_Anomaly_Detection>`_\ :

ShanghaiTech Campus dataset has 13 scenes with complex light conditions and camera angles. It contains 130 abnormal events and over 270, 000 training frames. Moreover, pixel level ground truth of abnormal events is also annotated in the dataset.

There are 317398 frames in total including 300308 regularity frames and 17090 irregularity frames. And the total abnormal events are 130, and the scenes are 13.

More information can refer to [`Video Anomaly Detection With Sparse Coding Inspired Deep Neural Networks <https://ieeexplore.ieee.org/document/8851288>`_].

[**New**]


[3] `UCF-Crime dataset <https://webpages.uncc.edu/cchen62/dataset.html>`_\ :

UCF-Crime dataset is a new large-scale first of its kind dataset of 128 hours of videos.

It consists of 1900 long and untrimmed real-world surveillance videos, with 13 realistic anomalies including Abuse, Arrest, Arson, Assault, Road Accident, Burglary, Explosion, Fighting, Robbery, Shooting, Stealing, Shoplifting, and Vandalism. These anomalies are selected because they have a significant impact on public safety. This dataset can be used for two tasks. First, general anomaly detection considering all anomalies in one group and all normal activities in another group. Second, for recognizing each of 13 anomalous activities.

More information can refer to [`Real-world Anomaly Detection in Surveillance Videos <https://arxiv.org/pdf/1801.04264.pdf>`_].

[**New**]


[4] `Avenue Dataset for Abnormal Event Detection <http://www.cse.cuhk.edu.hk/leojia/projects/detectabnormal/dataset.html>`_\ :

Avenue Dataset contains 16 training and 21 testing video clips with a total of 47 abnormal events, including throwing objects, loitering and running. The apparent size of people may change because of the camera position and angle. The videos are captured in CUHK campus avenue with 30652 (15328 training, 15324 testing) frames in total.

Video Description: The training videos capture normal situations. Testing videos include both normal and abnormal events. Three abnormal samples are shown as follows.

Their dataset contains the following challenges: 1. Slight camera shake (in testing video 2, frame 1051 - 1100) presents. 2. A few outliers are included in training data. 3.Some normal patterns seldom appear in training data.

More information can refer to [`Abnormal Event Detection at 150 FPS in Matlab <http://shijianping.me/abnormal_iccv13.pdf>`_].

[**Common**]


[5] `UCSD Anomaly Detection Dataset <http://www.svcl.ucsd.edu/projects/anomaly/dataset.html>`_\ :

The UCSD Anomaly Detection Dataset was acquired with a stationary camera mounted at an elevation, overlooking pedestrian walkways. The crowd density in the walkways was variable, ranging from sparse to very crowded. In the normal setting, the video contains only pedestrians. Abnormal events are due to either: 1. The circulation of **non pedestrian** entities in the walkways. 2. Anomalous pedestrian motion patterns.

Commonly occurring anomalies include bikers, skaters, small carts, and people walking across a walkway or in the grass that surrounds it. A few instances of people in wheelchair were also recorded. All abnormalities are naturally occurring, i.e. they were not staged for the purposes of assembling the dataset.

The data was split into 2 subsets, each corresponding to a different scene. The video footage recorded from each scene was split into various clips of around 200 frames.

More information can refer to [`Anomaly Detection in Crowded Scenes <https://www.researchgate.net/publication/221362278_Anomaly_Detection_in_Crowded_Scenes>`_].

[**Common**]


[6] `LV Dataset <https://cvrleyva.wordpress.com/2017/04/08/lv-dataset/comment-page-1/#comment-240>`_\ :

The LV dataset is a challenging dataset, where all videos are collected online and abnormal events are realistic. An abnormal frame is labelled as a true positive when at least 20% of abnormal regions of a frame is correctly detected, otherwise it is a false positive.

And it comprises video sequences characterized by the following aspects: 1. Realistic events without actors performing predeﬁned scripts with a diverse subject interaction. 2. Highly unpredictable abnormal events in different scenes, some of them of very short duration. 3. Scenario correspondence, where the training and test data are captured from the same scene. 4. Challenging environmental conditions; sequences are acquired under changing illumination and camera motion.

The LV dataset consists of 30 sequences with 14 different abnormal events. The abnormal events contain fighting, people clashing, arm robberies, thefts, car accidents, hit and runs, ﬁres, panic, vandalism, kidnapping, homicide, cars in the wrong-way, people falling, loitering, prohibited u-turns and trespassing.

More information can refer to [`The LV dataset: A realistic surveillance video dataset for abnormal event detection <https://ieeexplore.ieee.org/document/7935096>`_].

[**Common**]


[7] `Anomalous Behavior Data Set <http://vision.eecs.yorku.ca/research/anomalous-behaviour-data/>`_\ :

This website provides a data set for anomalous behaviour detection in video. The data set contains 8 image sequences that depict a wide range of challenging scenarios, including: illumination effects, scene clutter, variable target appearance, rapid motion and camera jitter. All sequences are available with manually constructed ground truth that identifies anomalous behaviour relative to a training portion of the video. Also provided is software for groundtruth construction and subsequent evaluation.

The videos with groundtruth contain traffic-train, belleview, boat-sea, boat-river, subway-exit, canoe, caouflage and airport-wrongdir.

[**Common**]


2. Papers
---------

2.1 CV Overview & Survey
^^^^^^^^^^^^^^^^^^^^^

[1]`An overview of deep learning based methods for unsupervised and semi-supervised anomaly detection in videos <https://arxiv.org/pdf/1801.03149.pdf>`_\

2.2 2015-2016
^^^^^^^^^^^^^^^^^^^^^
Coming Soon

