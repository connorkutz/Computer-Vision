# Edge Detection Improvements

Edge detection is used in the majority of computer vision applications. Generally, it outlines the distinct object and shape divisions within the image as shown:

![N|#Title]()

For this project, I will be exploring the methods of edge detection and what can be done to improve them. 

To date, there are 2 main methods to detect edges in images. The first approach was known as the Sobel Operator which are implemented as convolution of two 3x3 matrices.

![N|#Title]()

The effect of these convolutions is a highlight on any change in magnitude running vertically or horizontally. Combined, they work for diagonal edges too. 

The second commonly used form of edge detection is known as Laplacian of Gaussian. Effectively, when this filter applied to an image, it yields the second derivative of the image. On relatively smooth areas of the photo, the filter will give a zero. When there is a change in the image, the filter will give a positive response on the darker side and a negative response on the lighter size. 

To make this easier to visualize, here is an example in one dimension.

![N|#Title]()

The most effective way to date of detecting edges is known as Canny edge detection, named after its creator, John Canny. It is popular for its low error rate, its reliability in finding the center of an edge, and the fact that it will only mark an edge once. It uses the Sobel Operators in combination with a few other optimizations to make the result more accurate.

The steps of the Canny edge detection algorithm are as follows:

![N|#Title]()

*Step 1: A Gaussian filter is applied to remove any noise to prevent false positives.* 

This step is relatively self explanatory. The sigma value is chosen in proportion to the resolution of the image so as not to remove too much detail. The size of the operator can be as large or as small as wanted, a 5x5 matrix is a nice medium to get the best runtime and a sufficient smoothness.

![N|#Title]()

*Step 2: The Sobel Operator is applied as described above to find intensity gradients.*

In this step, Sobel operators are created to specification and applied as a convolution. First in the x direction, then the y. Once the gradient magnitudes are given by the convolutions, they are combined and normalized via the absolute value of the sum as:

	 gradient = sqrt(xGradient.^2 + yGradient.^2)

![N|#Title]()

*Step 3: Edges are thinned to ensure that an edge is represented by one pixel width.*

Though it appears sloppy, the detail is retained as shown in Step 3.Technically, this step is known as "Non-Maximum Suppression." The algorithm for non-maximum suppression goes like this:

	for each pixel, [i,j], in the image
        calculate the angle, A[i,j], of the edge on which it lies
        round the A[i,j] to the nearest 45º
        %% eg: 0º, 45º, 90º, 135º
    end
    for each pixel, [i,j], on an edge in the 0º direction
    	if the magnitude at [i,j] is greater than the magnitudes of the
        two adjacent pixels in the 0º and 180º directions, then it is an edge,
        so suppress the other two pixels (set them to 0).
    end
    for each pixel, [i,j], on an edge in the 45º direction
        if the magnitude at [i,j] is greater than the magnitudes of the
        two adjacent pixels in the 45º and 225º directions, then it is an edge,
        so suppress the other two pixels (set them to 0).
    end
    for each pixel, [i,j], on an edge in the 90º direction
        if the magnitude at [i,j] is greater than the magnitudes of the
        two adjacent pixels in the 90º and 270º directions, then it is an edge,
        so suppress the other two pixels (set them to 0).
    end
    for each pixel, [i,j], on an edge in the 135º direction
        if the magnitude at [i,j] is greater than the magnitudes of the
        two adjacent pixels in the 135º and 315º directions, then it is an edge,
        so suppress the other two pixels (set them to 0).
    end

![N|#Title]()

*Step 4: Any edges that may have been broken into pieces during step 4 are connected.*

Here edges are separated into two groups, strong edges and weak edges by a predetermined threshold. Then if a weak edge pixel has no strong neighbors, it can be removed.

	for each pixel, [i,j]
    	if the value at [i,j] is below a certain threshold
        	the pixel at [i,j] is weak
        else
            the pixel is strong
    end
    for each pixel, [i,j]
        if the pixel at [i,j] is weak
           check its 8 neighbors if none of them are strong, zero the pixel
            if is has a strong neighbor, maximize the pixel (usually 255)
        if the pixel at [i,j] is strong
        maximize the pixel (set to 255)
    end

![N|#Title]()

To date, the Canny edge detection algorithm is still the most versatile and most widely used edge detector. Though there are other lesser used algorithms, they still don't have the same resilience and reliability.

![N|#Title]()
![N|#Title]()
![N|#Title]()
![N|#Title]()
![N|#Title]()