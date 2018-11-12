# YOLO
When it comes to deep learning-based object detection, there are three primary object detectors you’ll encounter:

  R-CNN and their variants, including the original R-CNN, Fast R- CNN, and Faster R-CNN
  Single Shot Detector (SSDs)
  YOLO
  R-CNNs are one of the first deep learning-based object detectors and are an example of a two-stage detector.

In the first R-CNN publication, Rich feature hierarchies for accurate object detection and semantic segmentation, (2013) Girshick et al. proposed an object detector that required an algorithm such as Selective Search (or equivalent) to propose candidate bounding boxes that could contain objects.
These regions were then passed into a CNN for classification, ultimately leading to one of the first deep learning-based object detectors.
The problem with the standard R-CNN method was that it was painfully slow and not a complete end-to-end object detector.

Girshick et al. published a second paper in 2015, entitled Fast R- CNN. The Fast R-CNN algorithm made considerable improvements to the original R-CNN, namely increasing accuracy and reducing the time it took to perform a forward pass; however, the model still relied on an external region proposal algorithm.

It wasn’t until Girshick et al.’s follow-up 2015 paper, Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks, that R-CNNs became a true end-to-end deep learning object detector by removing the Selective Search requirement and instead relying on a Region Proposal Network (RPN) that is (1) fully convolutional and (2) can predict the object bounding boxes and “objectness” scores (i.e., a score quantifying how likely it is a region of an image may contain an image). The outputs of the RPNs are then passed into the R-CNN component for final classification and labeling.

While R-CNNs tend to very accurate, the biggest problem with the R-CNN family of networks is their speed — they were incredibly slow, obtaining only 5 FPS on a GPU.

To help increase the speed of deep learning-based object detectors, both Single Shot Detectors (SSDs) and YOLO use a one-stage detector strategy.

These algorithms treat object detection as a regression problem, taking a given input image and simultaneously learning bounding box coordinates and corresponding class label probabilities.

In general, single-stage detectors tend to be less accurate than two-stage detectors but are significantly faster.

YOLO is a great example of a single stage detector.

First introduced in 2015 by Redmon et al., their paper, You Only Look Once: Unified, Real-Time Object Detection, details an object detector capable of super real-time object detection, obtaining 45 FPS on a GPU.

Note: A smaller variant of their model called “Fast YOLO” claims to achieve 155 FPS on a GPU.

YOLO has gone through a number of different iterations, including YOLO9000: Better, Faster, Stronger (i.e., YOLOv2), capable of detecting over 9,000 object detectors.

Redmon and Farhadi are able to achieve such a large number of object detections by performing joint training for both object detection and classification. Using joint training the authors trained YOLO9000 simultaneously on both the ImageNet classification dataset and COCO detection dataset. The result is a YOLO model, called YOLO9000, that can predict detections for object classes that don’t have labeled detection data.

While interesting and novel, YOLOv2’s performance was a bit underwhelming given the title and abstract of the paper.

On the 156 class version of COCO, YOLO9000 achieved 16% mean Average Precision (mAP), and yes, while YOLO can detect 9,000 separate classes, the accuracy is not quite what we would desire.

Redmon and Farhadi recently published a new YOLO paper, YOLOv3: An Incremental Improvement (2018). YOLOv3 is significantly larger than previous models but is, in my opinion, the best one yet out of the YOLO family of object detectors.

The COCO dataset consists of 80 labels, including, but not limited to:

  People
  Bicycles
  Cars and trucks
  Airplanes
  Stop signs and fire hydrants
  Animals, including cats, dogs, birds, horses, cows, and sheep, to name a few
  Kitchen and dining objects, such as wine glasses, cups, forks, knives, spoons, etc.
  …and much more!

# Limitations and drawbacks of the YOLO object detector
Arguably the largest limitation and drawback of the YOLO object detector is that:

  It does not always handle small objects well
  It especially does not handle objects grouped close together
  The reason for this limitation is due to the YOLO algorithm itself:

The YOLO object detector divides an input image into an SxS grid where each cell in the grid predicts only a single object.
  If there exist multiple, small objects in a single cell then YOLO will be unable to detect them, ultimately leading to missed object detections.
  Therefore, if you know your dataset consists of many small objects grouped close together then you should not use the YOLO object detector.

In terms of small objects, Faster R-CNN tends to work the best; however, it’s also the slowest.

SSDs can also be used here; however, SSDs can also struggle with smaller objects (but not as much as YOLO).

SSDs often give a nice tradeoff in terms of speed and accuracy as well.

It’s also worth noting that YOLO ran slower than SSDs. YOLO object detector took ~0.3 seconds, approximately an order of magnitude slower!

If you’re using the pre-trained deep learning object detectors OpenCV supplies you may want to consider using SSDs over YOLO. From my personal experience, I’ve rarely encountered situations where I needed to use YOLO over SSDs:

I have found SSDs much easier to train and their performance in terms of accuracy almost always outperforms YOLO (at least for the datasets I’ve worked with).
YOLO may have excellent results on the COCO dataset; however, I have not found that same level of accuracy for my own tasks.

# Use the following guidelines when picking an object detector for a given problem:

  If I know I need to detect small objects and speed is not a concern, I tend to use Faster R-CNN.
  If speed is absolutely paramount, I use YOLO.
  If I need a middle ground, I tend to go with SSDs.
  In most of my situations I end up using SSDs or RetinaNet — both are a great balance between the YOLO/Faster R-CNN.
