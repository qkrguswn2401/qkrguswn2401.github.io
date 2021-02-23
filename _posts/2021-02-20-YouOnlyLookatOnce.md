---
title: "You Look at Once"
date: 2021-02-16 08:26:28 -0400
categories: Paper Review
---

RCNN: Performs deteciton on various regions proposals and performs prediction multiple times for various regions in a image.  RCNN only looks at boudning boxes and neglects other parts of the image.  


YOLO is real-time object detection.
YOLO is more like FCNN that passes the image through the FCNN and passteh output is the prediction.  It splitst he input image in mxm grid and each grid generation, 2 bounding boxes and softmax for those boxes exist.  


Single CNN simultaneous predcits bounding boxes and predict what class the box is.  YOLO frame detection as regression probelm that is why it is extremely fast.  Because YOLO looks at the entire image unlike RCNN it takes other regions than bounding boxes into  account.   Compared to other object detection algorithms, accuracy is lower especially for smaller object.

How YOLO detects:
  1. First image is split into S x S grid.  Then, it get 2 bounding boxes for each grid.  Each bound box has confidence score for existence of object in the bounding box multiplied by IOU.  IOU is how closely bounding is drawn for the object.  
  2. Then, grid pixel has C (class) number of probabilities for the grid pixcel.  Bounding box has 5 features: W, H, W,H, and confidnce where x,y are the center coordinate of the image.    

network:  
  It is Based on GoogleNet and composed of 24 + 2 FC.
  
