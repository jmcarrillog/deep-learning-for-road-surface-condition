## Design of Efficient Deep Learning models for Determining Road Surface Condition from Roadside Camera Images and Weather Data

This repository contains the data and source code of the [TAC-ITS'19](https://www.tac-atc.ca/en/conference/papers/comparison-deep-learning-models-determining-road-surface-condition-roadside-camera-images-and) paper titled *Comparison of Deep Learning models for Determining Road Surface Condition from Roadside Camera Images and Weather Data*, it also uncludes PDF documents of the paper and the slides.

The official proceedings are available in the [TAC-ITS'19](https://www.tac-atc.ca/en/conference/papers/comparison-deep-learning-models-determining-road-surface-condition-roadside-camera-images-and) Conference website. Paper prepared for presentation
at the Artificial Intelligence and Machine Learning for Smart Mobility Session.

Authors: *Juan Carrillo <sup>1</sup>, Mark Crowley <sup>1</sup>, Guangyuan Pan <sup>2</sup>, Liping Fu <sup>2</sup>.*

* *<sup>1</sup> Department of Electrical and Computer Engineering, University of Waterloo*
* *<sup>2</sup> Department of Civil and Environmental Engineering, University of Waterloo*

### Abstract
> Road maintenance during the Winter season is a safety critical and resource demanding
operation. One of its key activities is determining road surface condition (RSC) in order to prioritize
roads and allocate cleaning efforts such as plowing or salting. Two conventional approaches for
determining RSC are: visual examination of roadside camera images by trained personnel and
patrolling the roads to perform on-site inspections. However, with more than 500 cameras
collecting images across Ontario, visual examination becomes a resource-intensive activity,
difficult to scale especially during periods of snowstorms. This paper presents the results of a
study focused on improving the efficiency of road maintenance operations. We use multiple Deep
Learning models to automatically determine RSC from roadside camera images and weather
variables, extending previous research where similar methods have been used to deal with the
problem. The dataset we use was collected during the 2017-2018 Winter season from 40 stations
connected to the Ontario Road Weather Information System (RWIS), it includes 14.000 labeled
images and 70.000 weather measurements. We train and evaluate the performance of seven
state-of-the-art models from the Computer Vision literature, including the recent DenseNet,
NASNet, and MobileNet. Moreover, by following systematic ablation experiments we adapt 
previously published Deep Learning models and reduce their number of parameters to about ~1.3% 
compared to their original parameter count, and by integrating observations from weather 
variables the models are able to better ascertain RSC under poor visibility conditions.

### Keywords
Deep Learning, Machine Learning, Spatial Statistics, Road Monitoring, Computer Vision.

### Remark
We design a Deep Convolutional Neural Network model to automatically classify Road Surface Condition (RSC) and optimize its efficiency by two orders of magnitude compared to previous models. This paper buils on our previous work on data integration for road monitoring, described in another [paper](https://github.com/jmcarrillog/data-integration-for-road-monitoring).

### Graphical abstract

* **Winter road maintenance: Current approach**

<img src="/readme-images/current_approach.png" width="600" />

* **Winter road maintenance: Suggested approach**

<img src="/readme-images/suggested_approach.png" width="600" />

### Input data
* 14,000 images from roadside cameras installed in 40 Road Weather Information System (RWIS) stations across Ontario. The images are labeled into three categories (Figure 1) of Road Surface Condition (RSC) according to guidelines used by the Ministry of Transportation of Ontario (MTO). To access this dataset please contact Prof. Liping Fu at the University of Waterloo [iTSS Lab](https://itsslab.com/).

<img src="/readme-images/rsc_categories.png" width="600" />

*Figure 1. Example images from a roadside camera near Otter lake in Ontario.
Left: Bare pavement. Center: Partial snow cover. Right: Full snow cover.*

* [Coordinates](/data/number_imgs_per_rwis_station.csv) of the 40 RWIS stations used for this project as seen in Figure 2. This table also includes the number of images retrieved from each station as well as their respective RSC category.

<img src="/readme-images/area_of_interest.png" width="300" />

*Figure 2. Location of the sample 40 RWIS stations in the province of Ontario.*

* [Weather data](/data/RWIS_weather_historical) for the 40 RWIS stations listed above, from November 2017 to March 2018. For each station this dataset contains observations of five weather variables collected every 10 minutes. The folder contains (40 stations x 5 months x 5 variables) 1,000 .csv files, for a total of more than 3,600,000 weather records. From these observations we extract 70,000 records to joint them with the date and time of each of the 14,000 images. Table 1 describes the weather variables and units.

*Table 1. Weather variables and their units.*

Variable | Units
--|--
Air Temp | (°C)
Dew Point | (°C)
Pressure | (kPa)
Relative Humidity | (%)
Wind Speed | (km/h)

### Source code
The Python source code used in this project is distributed in 39 Jupiter notebooks, stored after execution to preserve the outputs and results of each experiment. To facilitate access we grouped these notebooks into five folders depending on the stage of the project they were used for.

#### Data preparation

Notebook | Description
--|--
[image-resize.ipynb](/code/data-preparation/image-resize.ipynb) | Crop and resize images
[split-train-test.ipynb](/code/data-preparation/split-train-test.ipynb) | Split 90% of images for training and 10% for testing

#### Initial comparison of Deep Learning models
Notebook | Description
--|--
[baseline.ipynb](/code/initial-model-comparison/baseline.ipynb) | Baseline model
[densenet-169_finetune_only_fc.ipynb](/code/initial-model-comparison/densenet-169_finetune_only_fc.ipynb) | DenseNet model, finetuning only fully connected layers
[densenet-169_finetune_last_5perc.ipynb](/code/initial-model-comparison/densenet-169_finetune_last_5perc.ipynb) | DenseNet model, finetuning only last 5% of layers
[densenet-169_finetune_last_15perc.ipynb](/code/initial-model-comparison/densenet-169_finetune_last_15perc.ipynb) | DenseNet model, finetuning only last 15% of layers
[inception-resnet-v2_finetune_only_fc.ipynb](/code/initial-model-comparison/inception-resnet-v2_finetune_only_fc.ipynb) | Inception-ResNet model, finetuning only fully connected layers
[inception-resnet-v2_finetune_last_5perc.ipynb](/code/initial-model-comparison/inception-resnet-v2_finetune_last_5perc.ipynb) | Inception-ResNet model, finetuning only last 5% of layers
[inception-resnet-v2_finetune_last_15perc.ipynb](/code/initial-model-comparison/inception-resnet-v2_finetune_last_15perc.ipynb) | Inception-ResNet model, finetuning only last 15% of layers
[inception-v3_finetune_only_fc.ipynb](/code/initial-model-comparison/inception-v3_finetune_only_fc.ipynb) | Inception model, finetuning only fully connected layers
[inception-v3_finetune_last_5perc.ipynb](/code/initial-model-comparison/inception-v3_finetune_last_5perc.ipynb) | Inception model, finetuning only last 5% of layers
[inception-v3_finetune_last_15perc.ipynb](/code/initial-model-comparison/inception-v3_finetune_last_15perc.ipynb) | Inception model, finetuning only last 15% of layers
[mobilenet-v2_finetune_only_fc.ipynb](/code/initial-model-comparison/mobilenet-v2_finetune_only_fc.ipynb) | MobileNet model, finetuning only fully connected layers
[mobilenet-v2_finetune_last_5perc.ipynb](/code/initial-model-comparison/mobilenet-v2_finetune_last_5perc.ipynb) | MobileNet model, finetuning only last 5% of layers
[mobilenet-v2_finetune_last_15perc.ipynb](/code/initial-model-comparison/mobilenet-v2_finetune_last_15perc.ipynb) | MobileNet model, finetuning only last 15% of layers
[nasnetmobile_finetune_only_fc.ipynb](/code/initial-model-comparison/nasnetmobile_finetune_only_fc.ipynb) | NasNet-mobile model, finetuning only fully connected layers
[nasnetmobile_finetune_last_5perc.ipynb](/code/initial-model-comparison/nasnetmobile_finetune_last_5perc.ipynb) | NasNet-mobile model, finetuning only last 5% of layers
[nasnetmobile_finetune_last_15perc.ipynb](/code/initial-model-comparison/nasnetmobile_finetune_last_15perc.ipynb) | NasNet-mobile model, finetuning only last 15% of layers
[xception_finetune_only_fc.ipynb](/code/initial-model-comparison/xception_finetune_only_fc.ipynb) | Xception model, finetuning only fully connected layers
[xception_finetune_last_5perc.ipynb](/code/initial-model-comparison/xception_finetune_last_5perc.ipynb) | Xception model, finetuning only last 5% of layers
[xception_finetune_last_15perc.ipynb](/code/initial-model-comparison/xception_finetune_last_15perc.ipynb) | Xception model, finetuning only last 15% of layers

#### Reduction of channels in convolutional layers
Notebook | Description
--|--
[baseline.ipynb](/code/initial-model-comparison/baseline.ipynb) | Original baseline model, equivalent to ICF 2.0
[baseline_icf_1.9.ipynb](/code/channels-reduction/baseline_icf_1.9.ipynb) | Modified baseline, ICF 1.9
[baseline_icf_1.8.ipynb](/code/channels-reduction/baseline_icf_1.8.ipynb) | Modified baseline, ICF 1.8
[baseline_icf_1.7.ipynb](/code/channels-reduction/baseline_icf_1.7.ipynb) | Modified baseline, ICF 1.7
[baseline_icf_1.6.ipynb](/code/channels-reduction/baseline_icf_1.6.ipynb) | Modified baseline, ICF 1.6
[baseline_icf_1.5.ipynb](/code/channels-reduction/baseline_icf_1.5.ipynb) | Modified baseline, ICF 1.5
[baseline_icf_1.4.ipynb](/code/channels-reduction/baseline_icf_1.4.ipynb) | Modified baseline, ICF 1.4
[baseline_icf_1.3.ipynb](/code/channels-reduction/baseline_icf_1.3.ipynb) | Modified baseline, ICF 1.3
[baseline_icf_1.2.ipynb](/code/channels-reduction/baseline_icf_1.2.ipynb) | Modified baseline, ICF 1.2
[baseline_icf_1.1.ipynb](/code/channels-reduction/baseline_icf_1.1.ipynb) | Modified baseline, ICF 1.1
[baseline_icf_1.0.ipynb](/code/channels-reduction/baseline_icf_1.0.ipynb) | Modified baseline, ICF 1.0

#### Reduction of neurons in fully connected layers
Notebook | Description
--|--
[baseline_icf_1.7.ipynb](/code/channels-reduction/baseline_icf_1.7.ipynb) | Modified baseline, ICF 1.7, 72 neurons in FC layers
[baseline_icf_1.7_nfc_63.ipynb](/code/neurons-reduction/baseline_icf_1.7_nfc_63.ipynb) | Modified baseline, ICF 1.7, 63 neurons in FC layers
[baseline_icf_1.7_nfc_54.ipynb](/code/neurons-reduction/baseline_icf_1.7_nfc_54.ipynb) | Modified baseline, ICF 1.7, 54 neurons in FC layers
[baseline_icf_1.7_nfc_45.ipynb](/code/neurons-reduction/baseline_icf_1.7_nfc_45.ipynb) | Modified baseline, ICF 1.7, 45 neurons in FC layers
[baseline_icf_1.7_nfc_36.ipynb](/code/neurons-reduction/baseline_icf_1.7_nfc_36.ipynb) | Modified baseline, ICF 1.7, 36 neurons in FC layers
[baseline_icf_1.7_nfc_27.ipynb](/code/neurons-reduction/baseline_icf_1.7_nfc_27.ipynb) | Modified baseline, ICF 1.7, 27 neurons in FC layers
[baseline_icf_1.7_nfc_18.ipynb](/code/neurons-reduction/baseline_icf_1.7_nfc_18.ipynb) | Modified baseline, ICF 1.7, 18 neurons in FC layers
[baseline_icf_1.7_nfc_9.ipynb](/code/neurons-reduction/baseline_icf_1.7_nfc_9.ipynb) | Modified baseline, ICF 1.7, 9 neurons in FC layers

#### Incorporating weather data
Notebook | Description
--|--
[baseline_icf_1.7_nfc_36_weather.ipynb](/code/using-weather/baseline_icf_1.7_nfc_36_weather.ipynb) | Modified baseline, ICF 1.7, 36 neurons in FC layers. Plus Machine Learning models using weather data.

### Acknowledgements

<img src="/readme-images/university_of_waterloo_logo.jpg" width="250" />

Juan Carrillo gives special thanks to Mark Crowley at the [Machine Learning Lab](https://uwaterloo.ca/scholar/mcrowley/lab), and Guangyuan Pan and Liping Fu at the [iTSS Lab](https://itsslab.com/) for their mentoring and contributions during this research project. Thanks as well to Matthew Muresan and Taimur Usman for the interesting technical discussions.
