# Aquiplicity2025
Aquiplicity 2025 JavaScript

Aquiplicity (multiplicity image stacker)

This is a JavaScript version of Aquiplicity full GUI and browser ran of course
Note all testing was done in Chrome browser.
1. Features button to import imags
2. Button to COMPOSE the stack of images into one master image
3. Button to SAVE image once lasso editing is complete

WHAT PROJECT DOES: Program takes images and stacks them, bringing attributes of all images to a master image and combining them. The first image is a baseline called image0.jpg such as an empty picture of a landscape. The other images have an actor like a woman in the same exact landscape image (tripod taken for registration of pixels and exactness) but the woman is in different locations on each image. The program stacks these images.

Actually three master images are created internally.  This is because each has a threshold for what pixels change.  In this way it's hoped to catch mroe nuance changes in pixels. From the three only ONE master image is finally displayed. After the master image is show the program allows you to click-and-drag a lasso by holding the CTRL key. The image from the pixel you started from will bring back sections of just that image, so for instance if a piece of her dress didn't carry to the master image correctly, one can fix any missing pixels for asthetic reasons.

After holding CTRL click the mouse and drag a free hand selection with a lasso tool on the master image. Whichever pixel the image is on at the moment of click, will determine what image of the stack is picked to repair the image. For instance, even if ten images are stacked in this master.jpg, if the pixel from image5.jpg is clicked then after the lasso is drawn …that section of the image from image5.jpg is brought forward and becomes the permanent part of the master.jpg. In this way we can patch any parts of the master image we do not like. Note the lasso image in this version is invisible since getting rid of the outline was difficult.

After holding ALT and clicking the mouse and dragging the program will try and blend two regions.  So for instance if the sky in image1 and image2 are different blues, one can draw between them holding the ALT key and it will blend the area for better transitions.

WHY IS THIS USEFUL: The idea is from my program creation in 2010 of a full GUI which was allot more complicated C++. The origin was trying to automate the Photoshop 'multiplicity' trend at the time making actors appear many times in the same image.

HOW USERS GET STARTED:  Double click the html file in the directory and it should show you in the GUI where to open your images.  It will say how many images you have selected in the GUI even before you click COMPOSE.  Compose button become not-gray after images are loaded.  Pushing compose makes the final mosaic of layered images.  Use CTRL and ALT key to clean up the images as desired.


WHERE USERS GET HELP WITH THIS IDEA: Email me at aquiline.photos@gmail.com for any comments or questions. It may take a while for a reply. Be patient.

MAINTAINED BY
Enjoy ! Mr. Tracy Rose
