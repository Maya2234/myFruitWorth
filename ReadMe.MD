#My Fruit Worth
Objective: pick all the fruits growing in your garden

Users can move forward, backward in the direction they are facing. Users can rotate with left and right keys
Users can restart the game with the R key. 

3 different graphic styles can be toggled via radio buttons.

When a user is close enough to a fruit object, they may pick it up by pressing the spacebar. The fruit will then be placed in their "basket". 
Once all the fruits have been collected by the player, a winning screen appears. 
The user may play again by pressing R.

Each object type used in the game (house, bush, fruit) are defined as a set of verticies, and edges, and faces made up of the original verticies. Instances of the objects are then created with details including position and scaling factor. Then objects are projected using the pinhole camera method: diving x and y by z to show depth.

##Level 1
First, I loop through each object skipping any picked fruit, and for each model apply the positioning and scaling and then projecting of all veritices. I sort for depth here make sure the smallest z in front of the camera gets drawn first by sorting depths from largest to smallest and starting with faces that are further away from the camera. To draw the faces, I used beginpath(), and then loop through all the verticies of each face with moveTo() before using closePath() and fill()

##Level 2
In level 2, first I initalize a grid of 320x200
Then, I loop through all the object instances to be drawn, skipping any picked fruit
For each object, I loop through all verticies, apply scaling and positing to the general model, and the project to the grid, and push to an array, skipping any behind camera. Next, I loop through the array of projected verticies and draw each edge, starting at (u1,v1), incrementing pixel by pixel on the x axis and adding the slope every incrementation to color in the pixels along the line.

##Level 3
In level 3, grid is again initialized and picked fruit are skipped. I apply positioning and scaling to each object instance and push the vertiices to an array. Then, for each object I loop through the object faces skipping any behind the camera. To fill in each triangle I take the bounding box of the 3 verticies and loop through every pixel, tessting with barycentric coordinates to only fill in pixels inside the verticie triangle.

Fixes and failures:
Unfortunately at the due date, my object collision method is not working ideally. It prevents users from crossing the "house" faces head on but at an angle (once camera position is rotated) it is not preventing the camera from moving through exisiting faces as it should. 

Future adjustments: 
Sun that sets (essentially game timer) and allow sky to darken as sun goes down
Weather + clouds
Basket visual -> can show filling up
Daily leaderboard 
