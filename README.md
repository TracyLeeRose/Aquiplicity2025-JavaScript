# Aquiplicity2025
Aquiplicity 2025 JavaScript

Aquiplicity (multiplicity image stacker)

This is a JavaScript version of Aquiplicity full GUI and browser ran of course
Note all testing was done in Chrome browser.

WHAT PROJECT DOES: 
Program takes images and stacks them, bringing attributes of all images to a master image and combining them. The first image is a baseline called image0.jpg such as an empty picture of a landscape. The other images have an actor like a woman in the same exact landscape image (tripod taken for registration of pixels and exactness) but the woman is in different locations on each image. The program stacks these images.

----- MANUAL ----

How-to Use Aquiplicity 2025: Your Friendly Guide to Image Magic

Code idea initally written by Tracy Rose with earliest concept in 2010 for the desktop app, but now this browser-based tool lets you transform a bunch of images into something totally new and exciting—all with just a few clicks and some creative flair. Whether you’re a beginner or a seasoned image tinkerer, this guide will walk you through every step to make the most of Aquiplicity’s unique features. Let’s dive in and start creating!

Getting Started
What You’ll Need
•	A modern web browser (Chrome, Firefox, Edge, etc.).
•	A few images (JPEGs, PNGs—anything your browser can handle).
•	A sense of adventure!

Opening Aquiplicity
1.	Load the Program: Open the Aquiplicity HTML file in your browser. You’ll see a clean interface with a control panel at the top, a thumbnail strip on the left, and a big working area with a canvas on the right.
2.	Check the Layout: 
o	Top Panel: Buttons and sliders for uploading images and tweaking settings.
o	Left Strip: Where your image thumbnails will appear.
o	Right Canvas: Your creative playground where the magic happens.
o	Status Bar: A little helper that tells you what’s going on.
Tip: If the page doesn’t load right, refresh it—sometimes browsers need a nudge!

Step 1: Upload Your Images
Let’s Get Those Pictures In!
1.	Find the Upload Button: At the top-left of the control panel, click the "Choose Files" button next to "Upload images to begin" (it’s an <input> field, but it looks like a button).
2.	Pick Your Images: 
o	Select multiple images from your computer (hold Ctrl or CMD to pick more than one).
o	You can upload as many as you like, but only the first 15 will show as thumbnails.
3.	Watch Them Load: The status bar will say "Loading X image(s)…" (X is how many you picked). You’ll see thumbnails pop up in the left strip, each 150x112 pixels, labeled "Image 1," "Image 2," etc.
What’s Happening?
The first image you upload sets the size for your canvas (scaled to fit your screen), and all others adjust to match. They’re stored as pixel data, ready for action.
Tip: Start with 2-5 images to keep things simple—think of them as ingredients for your visual recipe!

Step 2: Compose Your Master Image
Mix It Up with Thresholds
1.	Enable the Compose Button: Once your images load, the "Compose!" button (next to the upload field) lights up—click it!
2.	Tweak the Sliders (Optional):
o	You’ll see three sliders labeled T1, T2, and T3, set to 0.10, 0.12, and 0.13 by default.
o	Slide them between 0.01 and 1.0 to control how much each image blends into the first one (lower = less change, higher = more mixing).
o	The numbers next to each slider update as you move them—fun to watch!
3.	See the Magic: 
o	The status changes to "Composing images at multiple thresholds…".
o	Aquiplicity compares every pixel across your many images, picks the ones that differ enough (based on your thresholds), and blends them into a single master image.
o	After a moment, your canvas displays the result!
What’s Happening?
The software creates three versions of your composite (one for each threshold), then averages them into one smooth image. It’s like baking a cake with layers of flavor from every picture.
Tip: Try the "By Mr. Tracy Rose" button (bottom-right) to set all sliders to 0.13—a preset that gives an auto preset balanced mix!

Step 3: Edit with Patches and Lassos
Make It Your Own
Now that you’ve got a master image, let’s refine it with some cool tools: patching and lassoing.
Option 1: Quick Patch (Click)
1.	Pick a Spot: Click anywhere on the canvas.
2.	Patch It Up: A 5x5 pixel square around your click gets replaced with a chunk from one of your other images—the one that’s least like the spot you clicked.
3.	Check the Status: It’ll say something like "Patch (5x5) applied at X,Y" (X and Y are the coordinates).
What’s Happening?
Aquiplicity finds the image that’s most different at that exact pixel and swaps in a little 5x5 piece. It’s like patching a quilt with a surprise fabric!
Tip: Click around to swap in bits and pieces— which is great for fixing small flaws or adding quirky details.
Option 2: Patch with Invisible Lasso (Ctrl+Click)
1.	Start Drawing: Hold Ctrl (or CMD on Mac) and click on the canvas to begin a lasso.
2.	Trace Your Shape: Move your mouse to draw an outline (no visible line yet—just imagine it!). Release Ctrl when you’re done (or connect back to the start).
3.	Apply the Patch: If your lasso has at least 3 points, Aquiplicity picks the image that’s most different in that whole region and replaces it entirely within your shape.
What’s Happening?
It calculates the average color difference across the lassoed area and grabs a matching chunk from another image. Think of it as transplanting a big patch of “skin” from one picture to another.
Tip: Draw a big lasso over something like a sky or face to swap it out—perfect for bold changes!
Option 3: Blend Lasso (Alt+Click)
1.	Start Blending: Hold Alt and click to start your lasso.
2.	Draw Away: Move the mouse to outline an area, then release Alt to finish.
3.	Blend It In: The region inside your lasso gets averaged across all your images, creating a soft, dreamy mix.
What’s Happening?
Every pixel in the lasso becomes a blend of the same spot from every image—like mixing paint colors into a new shade.
Tip: Use this for smooth transitions, like blending a face into a surreal combo of all your portraits.
Note: If your lasso is too small (less than 3 points) or you let go of Ctrl/Alt early, it cancels—no harm done! The status will let you know.

Step 4: Save Your Creation
Keep Your Masterpiece
1.	Finish Up: Happy with your image? Click "Save Master Image" (below the canvas).
2.	Download It: A file named "combined_master.png" downloads to your computer—no lasso lines or temporary stuff, just your polished result.
3.	Check the Status: It’ll say "Combined master image saved (without lasso lines)".
What’s Happening?
Aquiplicity creates a clean copy of your canvas and turns it into a PNG file. It’s ready to share or print!
Tip: Save often if you’re experimenting—each save captures your latest version.

Step 5: Start Over (Optional)
Fresh Canvas, Fresh Ideas
1.	Hit Reset: Click the red "Reset" button at the top.
2.	Back to Basics: Everything clears—canvas, thumbnails, sliders (back to 0.10, 0.12, 0.13)—and the status says "Upload images to begin".
3.	Start Again: Upload new images and dive back in!
What’s Happening?
The slate’s wiped clean, ready for your next project. It’s like hitting the restart button on a video game.
Tip: Reset if you want to try a totally different set of images or if things get too wild!

Extra Tips and Tricks
•	Experiment with Thresholds: Low values (e.g., 0.05) keep more of your first image; high values (e.g., 0.50) mix in more from the others.
•	Use the Console: If you’re techy, open your browser’s developer tools (F12) and watch the console logs—they tell you exactly what’s happening (e.g., "Patch applied at: X,Y").
•	Combine Tools: Patch a spot, then blend over it with a lasso for a layered effect.
•	Image Choices: Try photos with strong contrasts (e.g., a bright beach and a dark forest) for dramatic results.

Troubleshooting
•	Compose Button Won’t Click? Make sure you’ve uploaded at least one image.
•	Canvas Looks Blank? Refresh the page—it might need a repaint nudge.
•	Lasso Not Working? Hold Ctrl or Alt the whole time you’re drawing, and make a shape with at least 3 points.
•	Images Won’t Load? Check they’re valid formats (JPEG, PNG) and not corrupted.

Why Aquiplicity Rocks
Aquiplicity isn’t just another photo editor—it’s a playground where your images become something new. With its threshold mixing, patch swaps, and blend-lassos, you can turn a family photo, a sunset, and a doodle into a wild, one-of-a-kind creation. It’s all in your browser, super-fast, and totally yours to play with.
Have Fun!

This manual provides a friendly, detailed walkthrough of Aquiplicity 2025’s features, tailored for users of all levels. Let me know if you’d like to tweak the tone or add more sections!

----



WHERE USERS GET HELP WITH THIS IDEA: 
Email me at aquiline.photos@gmail.com for any comments or questions. It may take a while for a reply. Be patient.

MAINTAINED BY
Enjoy ! Mr. Tracy Rose
