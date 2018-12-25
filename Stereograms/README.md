# Stereogram

The goal of this project was to turn a depth map into a stereogram. A stereogram is a single image that creates the illusion of a 3D image when seen correctly for example:

![N|]()

Though the colorization of my stereograms is not as sophisticated as above, it follows the same principle. The algorithm used is as follows:
  Stereogram{
  # with the depth map image as input
      for each row in the image, y
        for each unused pixel in the image, (x,y)
            generate a random color
            color the corresponding pixel in the stereogram
            find the depth, d of the pixel from the depth map
            create a distance, disp, 
            x = x + disp
            if (x,y) is still in the image
                goto "color the corre..."
  }

When creating a distance(disp), I found that some equations work better for certain images than others. 

here, *disp = 100 + d/2* :

![N|First]()

![N|First]()

Here, *disp = 140 + d/8*:

![N|First]()
![N|First]()
![N|First]()
![N|First]()

For a bonus, this same effect works for videos:

The algorithm is as follows:
  for each frame, f, in the video
    sg[f] = Stereogram(f)
    
![N|First]()
![N|First]()
