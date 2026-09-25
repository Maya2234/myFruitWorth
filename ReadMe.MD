# My Fruit Worth

**Objective:** Pick all the fruits growing in your garden.

## Controls & Gameplay

* **Movement:** Move forward or backward in the direction you are facing. Rotate using the **Left** and **Right** arrow keys.
* **Interaction:** When close enough to a fruit object, press **Spacebar** to pick it up and place it in your basket.
* **Restart:** Press **R** to restart the game at any time.
* **Graphics:** Toggle between 3 different visual styles via radio buttons.
* **Winning Condition:** A victory screen appears once all fruits have been collected. You can press **R** to play again.

## Technical Overview

Each object type used in the game (`house`, `bush`, `fruit`) is defined as a set of vertices, edges, and faces constructed from the original vertices. 

Object instances are created with specific position and scaling parameters, then projected using the **pinhole camera method** (dividing $x$ and $y$ by $z$ to project depth).

---

## Graphics Pipeline Levels

### Level 1

1. Loop through each object instance (skipping any collected fruit).
2. Apply positioning, scaling, and vertex projection for each model.
3. **Depth Sorting:** Sort depths from largest to smallest $z$-value so that geometry furthest from the camera is drawn first (ensuring the smallest $z$ in front of the camera draws last/on top).
4. **Rendering:** Draw faces using HTML5 Canvas methods: `beginPath()`, step through face vertices with `moveTo()`, then finish with `closePath()` and `fill()`.

### Level 2

1. Initialize a grid of $320 \times 200$.
2. Loop through all object instances (skipping collected fruit).
3. Apply scaling, positioning, and projection to the grid for all vertices, pushing valid points to an array (skipping geometry behind the camera).
4. Loop through projected vertices and draw each edge starting at $(u_1, v_1)$, stepping pixel-by-pixel along the X-axis and adding the slope on each increment to color the line.

### Level 3

1. Initialize the grid and skip collected fruit.
2. Apply positioning and scaling to object instances and store projected vertices.
3. For each object, loop through visible faces (clipping geometry behind the camera).
4. **Triangle Rasterization:** Calculate the bounding box for the 3 vertices of each face, then evaluate every pixel using **barycentric coordinates** to fill only pixels contained inside the triangle.

---

## Known Issues & Failures

* **Collision Detection:** Object collisions are not fully functional. While collision prevention works when approaching house faces head-on, approaching at an angle (after rotating the camera) allows the player to pass through solid faces.

---

## Future Improvements

* **Dynamic Day/Night Cycle:** Add a setting sun that acts as a game timer, causing the sky to gradually darken.
* **Weather System:** Introduce dynamic weather and clouds.
* **Basket UI:** Add a visual basket HUD element that fills up as fruits are collected.
* **Social Features:** Implement a daily leaderboard.
