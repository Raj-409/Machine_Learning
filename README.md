# Machine_Learning
 #OpenCV is a cross-platform library using which we can develop real-time computer vision applications. It mainly focuses on image processing, 
#video capture and analysis including features like face detection and object detection.
import cv2     
import numpy as np
from tkinter.filedialog import *   # tkinter filedialog:Python Tkinter (and TK) offer a set of dialogs that you can use when working with files.
                                  

photo = askopenfilename()
img = cv2.imread(photo) # Imread is a method in cv2 which is used to store images in the form of numbers.

# Transforming an image to grayscale: cvtColor(image, flag) is a method in cv2 which is used to transform an image into the colour-space mentioned as ‘flag’.
                                     
grey = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

# Smoothening a grayscale image: To smoothen an image, we simply apply a blur effect. This is done using medianBlur() 
#function. Here, the center pixel is assigned a mean value of all the pixels which fall under the kernel. In turn,
# creating a blur effect.
grey = cv2.medianBlur(grey, 5)

# ReSized3 = cv2.resize(smoothGrayScale, (960, 540))

# Retrieving the edges of an image: In this step, we will work on the first specialty. Here, we will try to retrieve 
#the edges and highlight them. This is attained by the adaptive thresholding technique. The threshold value is the mean of the 
#neighborhood pixel values area minus the constant C. C is a constant that is subtracted from the mean or weighted sum of the
#neighborhood pixels. Thresh_binary is the type of threshold applied, and the remaining parameters determine the block size.
edges = cv2.adaptiveThreshold(grey, 255, cv2.ADAPTIVE_THRESH_MEAN_C, cv2.THRESH_BINARY, 9, 9)

#cartoonize
# Preparing a Mask Image
'''In the above code, we finally work on the second specialty. We prepare a lightened color image that we mask with
edges at the end to produce
a cartoon image. We use bilateralFilter which removes the noise. It can be taken as smoothening of an image to an extent.'''
color = cv2.bilateralFilter(img, 9, 250, 250)

#  Giving a Cartoon Effect: So, let’s combine the two specialties.
# This will be done using MASKING. We perform bitwise and on two images to mask them
cartoon = cv2.bitwise_and(color, color, mask = edges)

# cv2.imshow() method is used to display an image in a window.
cv2.imshow("Image", img)
cv2.imshow("Cartoon", cartoon)

#save
# cv2. imwrite() method is used to save an image to any storage device. This will save the image according to the 
# specified format in current working directory.
cv2.imwrite("cartoon.jpg", cartoon)

# Parameters: cv2.waitkey(wait time in milliseconds)
#destroyAllWindows() in the script). If you use '0' as the parmater then the image will be displayed for infinite time 
#until you press the esc key.
cv2.waitKey(0)

# destroyAllWindows() simply destroys all the windows we created. To destroy any specific window, use the function cv2. 
#destroyWindow() where you pass the exact window name.
cv2.destroyAllWindows()
