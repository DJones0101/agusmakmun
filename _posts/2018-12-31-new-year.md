---
layout: post
title:  "The Most exciting thing I Learned in 2018: OpenCV"
categories: [python, OpenCV]
---
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;



&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Today is December 31, the last day of 2018. Tomorrow is my birthday, but it's not as meaningful as today is. On the last day of the year, I like to reflect on the things that I have learned in this span of 365 days. I have learned a ton. The best thing that I did in 2018 is starting this page, and it took me a while to figure it out. But this post is about the most exciting thing I learned.No doubt, OpenCV is the most exciting thing I learned in 2018. In this post, I will show you how to detect colors using OpenCV and show you what OpenCV can do.


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;


# The Python Code
Make sure you have a USB camera connected to you your computer.
The first lines of the code are the import statements. In the future, I will write a post about how to install OpenCV, but for now, let's assume you have it installed already.In the next lines, I define the boundaries of the colors in HSV color space. More on finding color boundaries in HSV 
[here](https://stackoverflow.com/questions/10948589/choosing-the-correct-upper-and-lower-hsv-boundaries-for-color-detection-withcv/10951189#10951189).

{% highlight python %}
	import cv2
	import numpy as np

	lower = {"red": np.array([0, 100,100]),        
            	"blue": np.array([110, 50,50]),
            	"green": np.array([65,60,60]),} 

	upper = {"red": np.array([10, 255, 255]), 
            	"blue": np.array([130, 255, 255]),
            	"green": np.array([80,255,255]),} 


{% endhighlight %}


To make the code readable I define a function called detect_color. This function takes in a frame and the color you want to recognize, it blurs the fame and converts it to HSV color space, next it finds the range of the color in the frame. Lastly, it returns a masked image and a result.


{% highlight python %}
	def detect_color(frame, color):

		kernel = np.ones((5,5),np.uint8)
		blurred = cv2.GaussianBlur(frame, (11, 11), 0)
		hsv = cv2.cvtColor(blurred,cv2.COLOR_BGR2HSV)
		mask = cv2.inRange(hsv,lower[color], upper[color])
		mask = cv2.morphologyEx(mask, cv2.MORPH_OPEN, kernel)
		mask = cv2.morphologyEx(mask, cv2.MORPH_CLOSE, kernel)
		result = cv2.bitwise_and(frame,frame, mask=mask)

		return result, mask
	
{% endhighlight %}



Inside the main function set the escape key to equal 27. Create a named window and start capturing video with cv2.VideoCapture(0) function. Next, we check to see if the webcam is grabbing the video feed.

{% highlight python %}
	
	EscKey = 27

	windowName = "Live Feed"
	color = "red"
	cv2.namedWindow(windowName)
	cap = cv2.VideoCapture(0)

	if cap.isOpened():
	 	success, frame = cap.read()
	else:
		print("Problem with the camera")
		success = False
	
{% endhighlight %}


Now that we are successfully reading in a video frame by frame we can send each frame and the color we want to the detect_color function. Next, we find the contours in the masked image using the findContours function.

To detect the largest contour, we use the max function with the contour we found earlier. Now we find the center of the circle and the radius with minEnclosingCircle   and draw it on the frame.  If the radius is larger than zero, we detected our marble with the color we were looking for. 



{% highlight python %}
	
	while success:

		success, frame = cap.read()
		result, mask = detect_color(frame,color)
		cnts = cv2.findContours(mask.copy(), cv2.RETR_EXTERNAL,
					cv2.CHAIN_APPROX_SIMPLE)[-2]
		radius = 0

		if len(cnts) != 0:
			c = max(cnts, key=cv2.contourArea)
			((x, y), radius) = cv2.minEnclosingCircle(c)
			cv2.circle(frame, (int(x), int(y)), int(radius), (0,255,255), 2)


		cv2.imshow(windowName, np.hstack([frame,result]))

		if radius > 0 :
			print("%s Marble detected!!" % color)
		else:
			print("Nothing detected!!!")


		if cv2.waitKey(1) == EscKey:
			break


	cv2.destroyWindow(windowName)		
	cap.release()
	
{% endhighlight %}


# The Output

Here's the live video feed.
![image](/static/img/Live_Feed.png)

Press the esc key to close the window. Isn't this cool!! Well it's getting late, I have to find a site that's streaming the count down. HAPPY NEW YEAR!!