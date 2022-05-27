---
title: "Automatic Licence Plate Recognition"
excerpt: "Licence plate detection and recognition with Mobilenetv2-SSDFPNLite + LPRnet<br/><img src='/images/alpr-system.PNG'>"
collection: portfolio
---
## Demo
A demo of the pipeline is located [here](https://huggingface.co/spaces/leakyrelu/MobilenetV2SSDLite_LPRnet)

## Pipeline
The pipeline uses the two-stage detection and recognition pipeline described in this [paper](https://ieeexplore.ieee.org/document/9071863)

## Implementation
Modifications to the prescribed architecture were made in the interest of optimizing parameter efficiency for execution  on low-resource edge devices. Specifically, the following modifications were made to the LPRnet architecture:

1. Depthwise separable convolutional layers are used 
2. Global context layers are used as suggested in the paper 
3. MobilenetV2SSDLite is used as the object detection network for licence plate detection as opposed to MobilenetSSD 
