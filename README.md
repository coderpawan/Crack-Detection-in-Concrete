# UG-Project-ML-Crack-Detection

This is my UG project under the guidance of Dr. Vishwajit Anand Sir

## Compiled results

My model has achieved a perfect F1 score of 1 . To know more read along

<img width="764" alt="image" src="https://user-images.githubusercontent.com/75925792/213254881-30ef6b02-49de-4984-b0f2-3bcc3bb59225.png">

## My Methodology -

### Bilateral Filtering :

After manual data exploration and analysis of the images , it was found that the images were contaminated with salt and pepper like noise . I wanted to amplify the differene between the positive and the negative image class , so image processing was a vital step of our solution approach . Initially I experimented with **Median Filtering** , since it is known fact in Image Processing and computer vision that salt and pepper noise is best removed my median filter .

However the results were not that satisfactory . This was because median filtering does not preserve edges , and the crucial differenciating factor in our dataset are the crack edges . After studying a bit , I observed that **Bilateral Filtering** preserves the edges as well as gets rid of salt and pepper like noises with some tradeoff as compared to the median filter , hence this was selected . It gave satisfactory results on our dataset .

![image](https://user-images.githubusercontent.com/86561124/212848270-09c036ab-bb05-4093-a25d-fa4fb6ef8e11.png)

### Opening Operation (Morphological operation) :

To further remove the concrete like pattern and amplify the difference between the classes , I decided to use the morphological operations . After experimenting with morphological operations opening and closing on the dataset , it was found that single iteration of opening operation with a 3x3 kernel was found to be suitable for our dataset . Opening is a morphological operation in which first erosion and then dilation occus on the image , and is used to remove the small pixels of noise while preserving the foreground bigger subjects .The dialation due to morphological operations sometimes resulted in lost of critical information and hence, we finally decided against employing it.

![image](https://user-images.githubusercontent.com/86561124/212850087-8b97e31d-291a-4be3-aaa5-39f5a3569513.png)

### Grayscaling of Images :

I separated the R, G and B channels of the images and observe them . There wasn't any significant difference in the R,G and B layers of the images , hence we decided that converting the images to grayscale won't cause loss to any feature set of our dataset , and instead **boost the speed of our procedure by around 3x** (since the neural network would have to now deal with 1 layer instead of 3 and hence would have to deal with 3 times less numbers approximately , hence having promisingly faster computation speed .

### Data-Augmentation :

Since the dataset is small , and is image based , hence I decided to use data augmentation to increase the size of the dataset . From manual inspection , it was observed that in some of the positive examples , the cracks are at the corners of the image and hence random zooming way throw the cracks out of the pictures , thus creating inconsistencies in the dataset . Hence I decided to only user **perfect 90 and 180 degree rotations , flipping** etc so as to avoid the risk of creating false positives in our dataset .

I also decided to **vary the brightness** by very less amount of around 10% , since the dataset did not have huge difference in contrast and brightness .

Soon I was able to increase my dataset from 300 examples per class to 3000 examples per class .

![IMG_0482_1_15](https://user-images.githubusercontent.com/75925792/213257537-0a6eda35-6952-4e40-bf37-009c72108d84.jpg)
![Positive_original_IMG_0482_1_15 jpg_8d0f2cbd-e68f-4b0b-b337-930e26cf7bb5](https://user-images.githubusercontent.com/75925792/213257626-324827fb-e0ab-4d98-80a7-0d6f79b9f715.jpg)

### The ML Modelling part

Since my dataset consists of images , I was able to choose few ML algorithms as per my requirements . After a bit of analysis of work done in this field from reading research papers , I was able to eliminate down to a few architectures that would be able to perform well on my dataset . Hence I decided to use **Transfer Learning** instead of training custom architecture models for our dataset .

![image](https://user-images.githubusercontent.com/86561124/212847014-ba8d53bb-3237-4005-9d4d-74619bf87133.png)
![image](https://user-images.githubusercontent.com/86561124/212847083-aeee27c1-64d3-4f33-a18a-2dbe2f7f15e8.png)

I experimented Myself with **ResNet** architecture and **VGG16** based architectures , and after the experiment , I found out that ResNet model performed better than the VGG16 Model . Hence I decided to **use ResNet architecture** for our final predictions .
