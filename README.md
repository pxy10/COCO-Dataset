## 常用数据集

### [COCO](https://cocodataset.org/#download)

在github中提供了COCO数据集的[测试demo](https://github.com/pxy10/COCO-Dataset/blob/main/20201020_coco_dataset.ipynb)。

#### 目标检测 & 实例分割

+ 数据集：[val2017](http://images.cocodataset.org/zips/val2017.zip)，共包含5000张图
+ 标签：[annotations_trainval2017](http://images.cocodataset.org/annotations/annotations_trainval2017.zip)

在该数据集中，共包含90种不同类型的物体和12种大类：

```python
COCO categories: 
person bicycle car motorcycle airplane bus train truck boat traffic light fire hydrant stop sign parking meter bench bird cat dog horse sheep cow elephant bear zebra giraffe backpack umbrella handbag tie suitcase frisbee skis snowboard sports ball kite baseball bat baseball glove skateboard surfboard tennis racket bottle wine glass cup fork knife spoon bowl banana apple sandwich orange broccoli carrot hot dog pizza donut cake chair couch potted plant bed dining table toilet tv laptop mouse remote keyboard cell phone microwave oven toaster sink refrigerator book clock vase scissors teddy bear hair drier toothbrush

COCO supercategories: 
outdoor electronic furniture indoor appliance person kitchen animal vehicle sports food accessory
```

标签通过`instances_val2017.json`文件的形式提供，文件内容比较乱，可以通过`pycocotools`中提供的`api`进行读取和显示。

```python
coco=COCO(annFile)
anns = coco.loadAnns([id of image])
```

其中`anns`中给出了`segmentation`和`bounding box`的信息。(segmentation是按照一系列坐标点构成的：[x1, y1, x2, y2...]；bounding box是按照[x, y, w, h]给出的)，下面是其中一段示例：

```
{"segmentation": [[344.9,28.88,332.98,23.23,325.45,23.86,307.89,30.13,299.73,42.05,295.34,49.58,292.2,57.11,279.02,67.15,275.89,72.8,278.4,106.68,286.55,143.07,292.2,160.01,290.32,166.91,288.44,177.57,285.93,186.99,282.16,202.67,287.81,235.93,294.71,245.34,295.34,255.38,297.22,263.53,305.38,269.18,324.83,267.92,326.08,264.16,358.08,266.04,373.14,269.81,379.41,262.28,383.18,256.63,386.31,247.85,390.08,240.94,395.1,213.97,393.22,198.91,390.08,185.73,388.82,176.95,391.33,139.93,396.35,106.05,398.24,86.6,395.1,82.83,375.65,62.76,368.75,49.58,363.73,38.91,356.2,32.64]],"area": 23972.5884,"iscrowd": 0,"image_id": 475484,"bbox": [275.89,23.23,122.35,246.58],"category_id": 14,"id": 418347}
```

#### 语义分割(semantic segmentation of *stuff* classes)

+ 数据集：[val2017](http://images.cocodataset.org/zips/val2017.zip)，共包含5000张图
+ 标签：[2017 Stuff Train/Val annotations](http://images.cocodataset.org/annotations/stuff_annotations_trainval2017.zip)

其中共包括92种不同类型的物体；标签文件中存在`stuff_val2017_pixelmaps`文件夹，其中即为pixel的标签图像。

另外在`json`文件中也包含了`segmentaion`的信息（分为0/1），不过是编码后的结果，可以通过`pycocotools`中的`coco.annToMask()`进行解码。

```
{"segmentation": {"counts": "VTj2>d;LZE6d:LZE6`:_OeD`0g00f:3YE5_:?PE_Oo:?QECo:\\1O0100O10001OO11N010000000001O0000000000000000000000001O001O0000000000O10000000000000000O1nMlDn1W;12N00003MN02O01001O00O1010O1O0MbDZN^;f1bDYN_;g13000OM302NOhNdDFI556Y;4X120OOOl^^4", "size": [426, 640]}, "area": 4868.0, "iscrowd": 0, "image_id": 139, "bbox": [216.0, 233.0, 81.0, 70.0], "category_id": 132, "id": 20000007},
```

#### 全景分割(Panoptic Segmentation)

+ 数据集：[val2017](http://images.cocodataset.org/zips/val2017.zip)，共包含5000张图
+ 标签：[panoptic_annotations_trainval2017](http://images.cocodataset.org/annotations/panoptic_annotations_trainval2017.zip)

好像并不支持`pycocotools`。



### [ImageNet](http://image-net.org/index)

包括[Object Bounding Boxes](http://image-net.org/download-bboxes)和[Object Attributes](http://image-net.org/download-attributes)；可用于进行目标检测和图像分类的任务。



### [PASCAL-Context](https://cs.stanford.edu/~roozbeh/pascal-context/#introduction)

该数据集是`PASCAL VOC`的补充，提供了图像全景范围内的segmentation的label。

+ [数据集](https://pjreddie.com/projects/pascal-voc-dataset-mirror/)
+ [annotations](https://cs.stanford.edu/~roozbeh/pascal-context/trainval.tar.gz)

