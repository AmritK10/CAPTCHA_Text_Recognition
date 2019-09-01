# CAPTCHA_Text_Recognition
## Intro
Created a model to recognise the characters in "[Really Simple CAPTCHA](https://wordpress.org/plugins/really-simple-captcha/)" plugin and hence break the CAPTCHA.<br/>
## Dataset
The plugin generates 4-letter CAPTCHAs using a random mix of four different fonts.<br>
A dataset of 10,000 images of CAPTCHAS generated by the plugin was used. The images are present in the <b>generated_captcha_images</b> folder.<br>
As the dataset is small we don't train our model on this entire image. We form another dataset of segmented characters (letters) of the image and design a model to train on these letters.<br>
In this way each individual letter is identified by the model and the combined letters are used to break the CAPTCHA.<br>
## OpenCV 
Opencv was used to perform character segmentation and to form the indivdual letters' dataset. Some of the functions used are:<br>
<ul>
  <li><b>cv2.imread(path): </b>Reads in the image</li>
  <li><b>cv2.cvtColor(img, cv2.COLOR_BGR2GRAY): </b>Converts image to gray scale</li>
  <li><b>cv2.copyMakeBorder(gray, 8, 8, 8, 8, cv2.BORDER_REPLICATE): </b>Add some extra padding around the image</li>
  <li><b>cv2.threshold(gray,0,255,cv2.THRESH_BINARY_INV | cv2.THRESH_OTSU)[1]: </b>Thresholds the image (converts it to pure black and white)</li>
  <li><b>cv2.findContours(thresh, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE): </b>Finds the contours (continuous blobs of pixels) in the image (Segements the letters)</li>
</ul>

## Model
A shallow convolutional model was created and trained on individual letters. It was used to predict the letters in the CAPTCHAS following segmentation hence breaking the CAPTCHA.

## Results
<img width="393" alt="Screen Shot 2019-09-02 at 1 02 01 AM" src="https://user-images.githubusercontent.com/31596604/64081355-59738780-cd1d-11e9-9c07-a81d10038c68.png">
<img width="391" alt="Screen Shot 2019-09-02 at 1 02 07 AM" src="https://user-images.githubusercontent.com/31596604/64081356-5a0c1e00-cd1d-11e9-8d82-cf923b27ce2e.png">
<img width="380" alt="Screen Shot 2019-09-02 at 1 02 13 AM" src="https://user-images.githubusercontent.com/31596604/64081357-5a0c1e00-cd1d-11e9-96d2-e8cac0bf5497.png">

## Note for running code
Add folder <b>extracted_letter_images</b> in the working directory before running.
