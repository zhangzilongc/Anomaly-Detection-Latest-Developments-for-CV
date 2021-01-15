Anomaly Detection Latest Developments for CV
====================================================

*Anomaly detection* recently has attracted more and more attention in the field of computer vision. Current anomaly detection tasks about computer vision (*ADCV*) can be roughly divided into 2 classes.

1. (Outlier Detection) The targets are to detect outliers that are significantly deviated from the current samples. The distribution of the outliers is far different from the distribution of the samples. For instance, in one-class classification, the target is to detect outliers when the test set mixes the figures of the bears with the figures of the dogs and the cats.

2. (Novelty Detection) The targets are to detect the anomaly samples which are much similar to normal samples. The distribution of anomaly samples is nearly the same as the normal samples. For instance, in the practical applications (e.g. in fabrication processes, defect detection), the samples only have small defects. And for sample figures over megapixels, only a few anomaly pixels can be observed.

In the context of recent *ADCV*, most tasks assume that only normal/target-class data is available in the training stage. And the target is to detect the outliers/anomaly samples. This assumption is consistent with the condition that the samples are under normal state conditions most of the time and the anomaly state is unknown and unpredictable. From my point, the most challenging problem in *ADCV* is that how to design a task to detect anomaly.

In this repository, recently used datasets about *ADCV* and the papers about the development of *ADCV* will be listed. In addition, some descriptions about the datasets and some summaries about the papers will be elaborated. Simultaneously, at the last, SOTA methods will be listed.

**The repository will be updated every month. The update information will contain the newest development of ADCV.**

Table of Contents
-----------------


* `1. Datasets <#1-datasets>`_
* `2. Papers <#2-papers>`_

  * `2.1. Overview & Survey <#21-overview--survey>`_
  * `2.2. 2015-2016 <#22-2015-2016>`_
  
  
1. Datasets
-----------
The datasets about *ADCV* listed below contain the normal/target-class data (train) and the anomaly/other-classes data (test).

All the classfication datasets (e.g. CIFAR10, CIFAR100, ImageNet etc). Regard the certain class as the target class and regard other classes as the anomaly.

`MVTEC AD Dataset <https://www.mvtec.com/company/research/datasets/mvtec-ad/>`_\ :MVTec AD is a dataset for benchmarking anomaly detection methods with a focus on industrial inspection. It contains over 5000 high-resolution images divided into fifteen different object and texture categories. Each category comprises a set of defect-free training images and a test set of images with various kinds of defects as well as images without defects. Pixel-precise annotations of all anomalies are also provided. More information can be found in the corresponding paper [`MVTec AD — A Comprehensive Real-World Dataset for Unsupervised Anomaly Detection <https://openaccess.thecvf.com/content_CVPR_2019/papers/Bergmann_MVTec_AD_--_A_Comprehensive_Real-World_Dataset_for_Unsupervised_Anomaly_CVPR_2019_paper.pdf>`_].

 

2. Papers
---------

2.1 Overview & Survey
^^^^^^^^^^^^^^^^^^^^^
Coming Soon

2.2 2015-2016
^^^^^^^^^^^^^^^^^^^^^
Coming Soon

