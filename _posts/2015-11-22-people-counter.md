---
layout: post
title: People Counter
---

### Abstract

A people counter is a device used to measure the number and direction of people traversing a certain passage or entrance, often used at buildings, so that the total number of visitors can be recorded.
This project aims to count number of people crossing a line at a time in viewframe of camera. Input to system will be live feed from the camera and output is count of people who have crossed the line. I will be calculating number of people who have crossed line in either direction. This way I can have counter for people going inside and outside the room.
It has varied applications in Retail store, Museums, Libraries and to calculate number of people going in/out of venue.
I have used opencv and numpy libraries for this project.

### Introduction


Real time people counter has important application and can be used to collect statistics of moving people. This technique is used by following industries: 

* Retail stores & chains.
* Malls and shopping centers.
* Colleges and universities.
* Government libraries and recreational parks.
* Events & exhibitions including fairs & sports arenas.
* Museums and art galleries
* Tourist and historical sites.
* Transportation terminals .
* Large halls for occasional events.

There have been earlier attempts to solve this problem by using different technologies such as

![Infrared people counting](https://upload.wikimedia.org/wikipedia/commons/thumb/0/0b/First_Generation_Infrared_Beam_Counter.jpg/330px-First_Generation_Infrared_Beam_Counter.jpg)
![Thermal counting](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5d/Second_Generation_Thermal_Counter.png/330px-Second_Generation_Thermal_Counter.png)

* Infrared beams
* Thermal counting - uses thermal sensor to detect heat sources. Thermal Imaging

But both approaches have their limitation especially during occlusion cases.
I am using Computer Vision Algorithms to count number of people.



### Approach

There are two approaches for this problem

1. Tracking by repeated detection
	- Works well when object is easily detectable
	- Need a way to link detected object in subsequent frames.
2. Tracking with dynamics
	* This approach is based on model of expected motion.
	* Robust to missing/weak observations.

I used first approach as objects are easily detectable in my case and are continuously moving.

* Capture Frame from Video Source.
* Calculate Background Image ( I haven't used Median filter to recalculate background image as its memory intensive operation and moreover Input Video is captured in controlled environment.)
* Background Subtraction - Frame Difference between background calculated in above step and current frame.
* Clear Noise - I am doing 3 iterations of "opening"  with (5,5) square kernel.
* Thresholding image and converting to binary to get binary segmented image.
* Finding Blobs - Using cv2.findcontours to find blobs boundary in segmented image.
* Discarding contours with area below a threshold area (1800 pi2).
* Mark each blob as ROI and track blobs in subsequent frames. I am storing each track points until subject is out of camera view.
* Count number of connected components in image.
* Keeping track of connected components with a label on each blob in next captured images.
* Count of people is incremented when center point of tracked blob crosses the monitored line in successive frames. 

Assumptions Made:

* Objects of Interest are always moving and therefore background subtraction will always give me ROI. This is true in this case since environment is controlled.
* One detected blob represents a person in image. In other words only humans are moving through the street. Any other moving object/animal will also be detected. I thought of using classifier to detect humans but then drop the idea due to shortage of time.

Other Approaches could be:

1. HOG (Histograms of Oriented Gradients) is state of art method for detecting people. HOG - Human Detection
2. LBP (Local binary patterns) with HOG is also feasible approach.
3. Mean-shift/Camshift algorithms could be used to track objects after object detection in subsequent frames.
4. For tracking multiple objects at one, MCMCDA (Markov Chain Monte Carlo Data Association) Tracking could be used. MCMCDA.
5. Watershed Algorithm could be used to differentiate people when they are very close to each other.

### Experiments and results

* I took my sample dataset form here.
{% include youtubePlayer.html id="OC0vJC8j8S8" %}
* I have tweaked the algorithm for given camera view angle only.
* I am able to successfully remove shadows of people in video.
* I have assumed range of area of blob and only detecting blobs which fall in considered range.
* This approach is only working when changes in subsequent frames are more. No person is standing or waiting.
* I am also combining multiple closeby contours to get large convex hull of merged contour. 
* Tracking convex hull of nearby contour gave better result than tracking individual contour.

### Qualitative results
After Thresholding

{% include youtubePlayer.html id="LPheWS9GEPE" %}

Results

{% include youtubePlayer.html id="-r-64f_01T0" %}

Results are accurate especially since I have tweaked parameters for given controlled environment. I tried to run this technique on Videocapture of street with cycles and humans with their pets, but results weren't as expected in that case.

I have uploaded code for this project at [Github](https://github.com/sbhal/cv_people_counter_project).

