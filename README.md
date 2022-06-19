# Ascii_Art
This python program can be used to generate ASCII art in the form of photos and videos
## Table of contents
* How to run the project
* Internal working of the project 
* Learnings from the project
* Resources

## How to run the project
This project requires installation of certain python packages:
* Open cv
* Pillow
* NumPy
* Glob
This project uses the font file and the image/video file hence requires them to be present in the same folder. It also requires the font type file that we use in the program.
	
## Internal working of the project 
For conversion of videos to ASCII art we capture each frame of the video and count the number of frames in the video.
```
video=cv2.VideoCapture("sample_video.mp4")
count=0
flag=1
while flag:
    flag,image=video.read()
    try:
        cv2.imwrite("images/frame%d.jpg"%count,image)
    except:
        break
    count+=1
```
Then we convert each of the captured frames to ASCII art.
For this we first set the background colour
```
bg = "white"
if bg == "white":
    bg_code = (255,255,255)
elif bg == "black":
    bg_code = (0,0,0)
```
Then we take the height and width of each image and resize it to calculate height and width of output image and make a new image using PIL
Then we map these characters to create ASCII art.
After that we check what is the background colour and invert and crop the ouput image acoordingly and save the output image.
Succesively we store each image to an image array and store this in an output video file.
```
img_array=[]
for filename in glob.glob('outputImages/*.jpg'):
    img = cv2.imread(filename)
    height, width, layers = img.shape
    size = (width,height)
    img_array.append(img)


out = cv2.VideoWriter('OutputVideo.avi',cv2.VideoWriter_fourcc(*"DIVX"), 25, size)
 
for i in range(len(img_array)):
    out.write(img_array[i])
```
This final video file is our ASCII art video.
## Learnings from the project
From this project we learn to use various python packages and their functions like, open cv and pillow.
* How to read images
* How to get attributes of an image
* How to convert an image to ASCII art
* How to read a video file

## Resources
* https://medium.com/analytics-vidhya/the-ultimate-handbook-for-opencv-pillow-72b7eff77cd7
* https://docs.opencv.org/4.x/d7/dbd/group__imgproc.html
* https://learnopencv.com/read-write-and-display-a-video-using-opencv-cpp-python/
* https://www.geeksforgeeks.org/python-play-a-video-using-opencv/
