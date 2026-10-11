# BoT-SORT
- State of the art performance
- Mostly clear usage instructions
- Deals with objection motion and occlusion quite well
- <span style="color:red">Only supports MOT17 and MOT20, no custom dataset :'( text</span>.
	- As written in the positional arguments part:
```C
positional arguments:
  path                  path to dataset under evaluation, currently only
                        support MOT17 and MOT20.
```
	- This was not written anywhere else >:(

# I think...no more research code/repository

# PyTrack

# UltralyticsYolo track
- [x] Try out detection and tracking
- [ ] Save ground truth images with bounding boxes already in them
- [x] Train own detection model

## Train own detection model
### Dataset structure
- datasets/{dataset_name}
	- images
	- labels
	- *.txt* files with paths to images
		- Train and test split
	- *.yaml* file with configurations
- More info [here](https://docs.ultralytics.com/datasets/detect/)

### Train
```python
	model = YOLO('yolov8s.yaml') # load the network with empty weights
	results = model.train(data='../../datasets/2024-01-\
								31_enlabeler_tracking/objtrack.yaml',
								epochs=20,
								imgsz=640)
```
- More info [here](https://docs.ultralytics.com/modes/train/#key-features-of-train-mode)

### Track
- Work in progress
```python
	results = model.track(imgs, presist=True)
	# plot results
	cv2.imshow(results[0].plot())
```
- Currently does not work well since the detection model is not meant to detect garbage
- Call tracking function per burst, since inter-burst tracking doesn't make any sense