- [x] Use current YOLOv8 model for detection
	- [x] Use these results for OpenCV trackers
	- [x] ID assignment is incorrect
- [ ] Implemented filer then evaluate again
	- [ ] Already in Bitbucket
	- [ ] Correct for bounding box

- [x] Also run tracking using Ultralytics
- [x] Run evaluation using MOTmetrics
	- [ ] Align prediction IDs with GT IDs
		- [ ] In the first frame, assign the prediction ID with the best matched GT ID
		- [ ] Document how this is done with schematics
	- [x] Find examples of different MOT event types
		- [x] Draw out all the possible scenarios
	- [ ] Get metrics per burst
- [x] Refactor the two repositories lmao what a mess
	- [x] `burst_separation.py` would not work due to the new dataset structure. -fixed
- [x] NaN ID count as a valid ID. Should set these distances to NaN
	- [ ] Also run BoT results through manual metrics
# Tracking scenarios
- [x] Go through all possible tracking scenarios
	- [x] OpenCV
		- [x] GT
		- [x] Det
			- [x] Behaves like MOT?
	- [x] MOT

# Evaluation
- [x] Show examples of cases of tracking (switch, transfer etc). For single ones a combinations. 
- [x] Accumulator per burst.
- [x] IoU thresholds or distance thresholds in MOTtracker evaluation, need to check what effect of that is.
- [x] Get MOT metric per burst. Need to have right number of objects per burst and localization accuracy per burst.
- [ ] Correct ID matching for opencv tracker evaluation of predictions.

# Order
- [x] Finish all the scenarios
- [x] Set IoU and distance of NaN ID objects as NaN as well so they are counted correctly
- [x] Estimate flow speed and see if there is any correlation
	- No > _ <
- [x] Design custom metrics
	- [x] We don't need to extract most of the objects, if we can get a few good tracks we are happy.
	- [x] FP tracks are bad
	- [x] Switches are very bad
	- [x] Check if matches are attached with other event types
	- [x] Check how good matches actually are within each burst, across the frames
	- [x] Percentage of good tracks over total number of tracks
	- [x] Need this for OpenCV too
	- [ ] Ignore ascends for now
- [x] Visualize the metrics

# Brain noodle
- There are 480 images
- Some images have no gt labels, making the total number of labelled frames to be less than 480
- Everything was fine when running OpenCV trackers using gt
- For detections I ran it on all images, so now we have results for all frames, even if nothing is tracked or detected
- This makes the number of labelled frames and number of detections mismatch in length and ID, causing unexpected behavior
- I was using gt frames to get the burst and frame ids for the dataframe, but since they are mismatched with the detections things go wrong.

## 05/08
- [x] Finish the new report
- [x] Check how many bursts have at least 1 good track
- [x] Check if there is any 0/0 cases
- [x] Do exclusivity check for good tracks

## 05/28
- Ran tracking with lower confidence and IoU thresholds (50% and 30%, respectively)
- 48% of bursts have good tracks
	- No change :(