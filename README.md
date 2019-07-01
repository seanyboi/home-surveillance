# Surveillance Application
This surveillance application involves using a Raspberry Pi along with a 
Camera to detect if a room is occupied through motion detection. If a room is 
occupied it will capture an  image and save the stored image to Dropbox.

# Step 1
Configure conf.json with important variable. This keeps our code clean and 
allows universal use across multiple files. Variable assigned involve 
resolution, frames per second and thresholds.

# Step 2
Integrate application with Dropbox. Create application within Dropbox App 
Console found at www.dropbox.com/developer.

# Step 3 - Motion Detection
We initialise the camera and grab a reference of it. We then loop over every 
frame that is being processed by the camera. Each frame is converted into an 
array and we apply Gaussian Blur to remove unnecessary high frequency noise. 
The weighted mean is then calculated of previous frames along with the 
current frame. This allows our background to adjust to changes such as 
lighting conditions throughout the day. We calculate a delta from our 
background model - current_frame.

# Step 4 - Thresholding / Finding Contours
Thresholding the delta image followed by dilating it will allow us to then 
find the contours. Contours are then looped over to see if they pass the 
minimum area criteria eg) are they big enough to pass for a human. Bounding 
box is then computed and placed on feed.

# Step 5 - Uploading Image to DropBox
If the room has been flagged as occupied then an image is uploaded to 
dropbox. However it makes sure that enough time has passed so consecutive 
images are not uploaded of same person constantly.
