# Colorizing the Prokudin Gorskii Images

The Prokudin-Gorskii collection is a grouping of images separated into RGB channels:

![N|Originals](https://github.com/connorkutz/Computer-Vision/raw/master/Colorizing%20Prokudin%20Gorskii/positives.jpg)

The goal of this project was to separate the images and align them to create a colorized photo of high quality:

![N|Goal](https://github.com/connorkutz/Computer-Vision/raw/master/Colorizing%20Prokudin%20Gorskii/ideal.jpg)

A first naive attempt was to divide the BGR image strip into equal thirds to see how closely they stack. This doesn't work because the supplied images have borders causing the edges to be severely misaligned:

![N|First](https://github.com/connorkutz/Computer-Vision/raw/master/Colorizing%20Prokudin%20Gorskii/first%20result.jpg)

The next step was to implement an algorithm to determine the exact amount of displacement need to align the edges of each color channel. The recommended method is called "Sum of Squared Differences," which averages a each image to see how similar they are, testing against various displacements to find the best fit. After trying the first time, it actually made my images worse because I was using the equation backwards and finding the displacement that made the images the most different:

![N|Second](https://github.com/connorkutz/Computer-Vision/raw/master/Colorizing%20Prokudin%20Gorskii/second%20result.jpg)

After correcting my issue with the sum of squared differences equation, I realized that the borders of the images were interfering with the ability to detect similarity so I implemented simple code to remove approximately 6% of the borders of each image after they were split into their channels. The result was a very well aligned photo where almost all of the edges match up to the other channels:

![N|Third](https://github.com/connorkutz/Computer-Vision/raw/master/Colorizing%20Prokudin%20Gorskii/third%20result.jpg)

The issue after this step is that the color filters used by Gorskii weren't perfectly accurate causing many of the photos to be overly saturated in the green channel. 

![N|Example](https://github.com/connorkutz/Computer-Vision/raw/master/Colorizing%20Prokudin%20Gorskii/final2.jpg)
![N|Example](https://github.com/connorkutz/Computer-Vision/raw/master/Colorizing%20Prokudin%20Gorskii/final3.jpg)
![N|Example](https://github.com/connorkutz/Computer-Vision/raw/master/Colorizing%20Prokudin%20Gorskii/final4.jpg)
![N|Example](https://github.com/connorkutz/Computer-Vision/raw/master/Colorizing%20Prokudin%20Gorskii/final5.jpg)

There was only one instance where the algorithm and equation failed to find the correct alignment for the color channels. This is most likely due to the shadows in the blue channel being very underexposed:

![N|Bad Example](https://github.com/connorkutz/Computer-Vision/raw/master/Colorizing%20Prokudin%20Gorskii/final7.jpg)