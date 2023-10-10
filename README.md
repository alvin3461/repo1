Objective: have an offline check outside of Cognex vision to return the bushing angle just from the image.

Method: this notebook takes a raw image of a bushing and applies various image processing techniques to determine the angel of the keyway relative to the center of the hole.

Assumptions: 
  1. System is sensitive to the angle of the camera mounting i.e. if the camera is rotated, it will also affect the output of the image. This cannot be elimiated unless we have an external global level value provided to us from another device that we can reference to.
  2. The relative position of the center of the bushing hole needs to be relatively similar to the reference images.

This is accomplished by:
  1. Taking the image file and converting it to a grayscale image so we only have one dimension of pixel values instead of three from RGB.
  2. We convert the image (bitmap) to a numpy array for it's array manipulation functions apply do some image formatting.
  3. A median filter is used to mitigate noise, then the four corner areas are manually converted to white pixels to cut out non-useful features.
  4. The center of mass of the resulting centroid is obtained to contruct a circle to split the keyway from the rest of the body.
  5. The angle delta is calculated between the keyway center of mass and the body center of mass to return the angle between the two.

Suggestions for improvement:
  1. Make it agnostic to planar shifts
