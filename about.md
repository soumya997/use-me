---
title: ABOUT PAGE
layout: _layouts/default.html
filename: about.md
--- 

## Day Planner

- [ ] <mark style="background: #BBFABBA6;">Model ensembling</mark> 
- [ ] <mark style="background: #BBFABBA6;">Make a classifier to filter out the FPs</mark> 
- [ ] <mark style="background: #BBFABBA6;">Try to figure out doing NMS with multiple image size inference like</mark> [this](https://www.kaggle.com/nicksergievskiy/cots-ens-yolov5-submission-scoring-error) 
- [ ] <mark style="background: #BBFABBA6;">Train Yolox, yolor</mark> 
- [ ] Fix systamatic eval of <mark style="background: #FFB86CA6;">yolov5</mark> 
- [ ] Augment some data for validation


## Major ramp ups
- [ ] Fine tune the provided model
- [ ] Train CascadeRCNN with default config in mmdet
- [ ] Use yolov5 evolution for HPT
- [ ] Train yolox and yolor
- [ ] Look into ensemble




### tf-reef Comp plannings:
1. `Base Plan:`   My planning is to to development in <mark style="background: #D2B3FFA6;">960x960</mark> images and do all the **`model building`, `hyper-parameter tuning`, `folds`, `augmentation`, `TTA`, `Ensemble`, `tracking`, [`sahi`](https://github.com/obss/sahi)**.
2. `Result visualization:` There are chances that the model is mostly predicting FP so to check that use this. Reduce FP. Find best <mark style="background: #BBFABBA6;">confedence value</mark> for the model by plotting the results. 
3. `Model With GPU:`Do 3 folds on the best model with on 4k or 9k images and see the LB. this will be considered in the submission with high LB.
4. `Model List:`
	- [ ] EfficientDet
	- [ ] YOLOV5
	- [ ] FasterRCNN with different backbones
		- [ ] ResNet-D [50,101,152]
	- [ ] YOLOX
	- [ ] Use TRACKING
	- [ ] Use Tiling/sahi
5. `The focus should be to pick one model and do the hyper-param tuning to the end.` In the model head, ROI, ROI allignment, Anchore box, FPN, NMS threshold small.
6. Do classification and then do object detection approach. Like in the COVID x-ray comp by nischay dhankar.
7. `Move to colab` ✅
8. Find a way to use unlabled data also [training might be time consuming]
9. `Augmentation:` 
	1. [Mosaic data augmentation](https://blog.roboflow.com/yolov4-data-augmentation/)
	2. copy paste
	3. cutmix, mixup
	4. light scattering, 
	5. cutout inside bbox
	6. Optical Distortion
10. `Few links on Augmentation:` 
	1. https://neptune.ai/blog/data-augmentation-in-python
11. `Mixed precision:` making float32 to float16 to reduce training time, but at the same time it does not redure model performance 
12. `Inference on high image size:` train on lower image size, inference on higher image. [helps if the img has small objects associated with it]
13. `Change the classifier/Use another model for feature extraction:` Use different model for feature extraction and add them all in one place and feed them into FasterRCNN.

### Orders from Group:
- [ ] find good augmentation techniques
- [ ] Find mean and std-dev of the data(for normalizing) Rather than using imagenet weights
- [ ] Try to split data into proper cross validation
- [ ] Add comp metric to the training loop

### tf-reef findings
- [ ] `Yes, I used 960x960 sizes, I suggest keep changing training parameters you will find a way. setting lower nmsthre helped!` ==mahipal singh==
- [ ] `They are using video 1 and video 2 for training and video 3 for validation`
- [ ] `download image from intenet for training`
- [ ] `When I tested the model in high resolution, there were a lot of "fake starfish" on the picture, but why did I get a higher score?`
 - `Ans:` F2 score metric is used in this competition. The F2 metric weights recall more heavily than precision, as in this case it makes sense to tolerate some false positives in order to ensure very few starfish are missed. That's why you observe more FP with improved KPI.
