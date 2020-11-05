# Assignment 6: Virtual Locomotion

**Due: Wednesday, November 18, 10:00pm CDT**

The purpose of this assignment is to gain experiencing with common virtual locomotion techniques.  The template code includes implementations of the view-directed steering, hand-directed steering, and teleportation from [Lecture 16](https://github.com/CSCI-5619-Fall-2020/Lecture-16).  You will extend these simple techniques with more advanced functionality.

## Submission Information

You should fill out this information before submitting your assignment.  Make sure to document the name and source of any third party assets such as 3D models, textures, or any other content used that was not solely written by you.  Include sufficient detail for the instructor or TA to easily find them, such as asset store or download links.

Name: 

UMN Email:

Build URL:

Third Party Assets:

Part 8 Instructions:

Bonus Challenge Instructions (if applicable):

## Rubric

Graded out of 20 points.  

1. Create a virtual obstacle course that will serve as a locomotion testbed.  The environment can be anything you want (indoor or outdoor), as long as it is large enough that the user will need to use virtual locomotion techniques.  The environment should also contain multiple obstacles that the user must navigate around.  You should actually plan out the environment; in other words, don't just randomly spawn MeshBuilder objects like the example code in Lecture 16.  (1)

2. Add a target object that follows a predefined path through the environment. The path should not just be a straight line, and should involve turning and moving around obstacles.  There are multiple ways to implement this, but the easiest way will probably be to use a [keyframe animation](https://doc.babylonjs.com/babylon101/animations).  The object should take at least one minute to complete the path.  When the target reaches a final destination, provide some sort of effect (visual and/or sound) to notify the user that they have won the game. (1)

3.  The user's task will be to "chase" the target object and avoid getting too far away. the user has to "chase" through the environment.  You should experiment with different object speeds to make the test moderately difficult, but not impossible to complete. (1)

4. When the user gets too far away from the target, teleport  both the user and target back to their starting positions.  The game then restarts. Experiment with different maximum difficulty thresholds until you find a reasonable difficulty balance. (1)

5. The current steering techniques allow flying up and down. Add a "fly mode" toggle using the controller B button.  When fly mode is toggled off, the locomotion should be restricted to the XZ plane. Make sure that the speed is also computed correctly. This toggle should apply to both the view-directed and hand-directed steering techniques. (2)

6. The current steering techniques implement rotation using a [smooth turn](https://xinreality.com/wiki/Smooth_Turn), which some users may find uncomfortable.  Convert this into a [snap turn](https://xinreality.com/wiki/Snap_Turn). This will apply a large, discrete rotation whenever the user moves the thumbstick left or right over a certain threshold.  The user must then return the thumbstick to the center position before another snap turn can be applied.  You should experiment with different thumbstick thresholds and discrete turn angles until you determine values that work well.  The snap turn should replace smooth turn for both the view-directed and hand-directed steering techniques. (2)

7. For the teleportation mode, a laser pointer is displayed when the user ray casts into a ground mesh.  Add a visual indicator at the teleportation target point to visualize the user's position and forward direction after the teleport. (2)

8. Add the ability for the user to modify their forward direction after the teleport.  This manipulation requires only one degree of freedom, which corresponds to rotation about the Y axis (yaw). You can use any method of controlling the direction that you want, as long as it is *spatial*. In other words, no controller thumbstick allowed! Possibilities include mapping the rotation of the controller around a specific axis to the intended direction or bimanual techniques that utilize the relationship between the two controllers. Make sure to include instructions for how to use this technique in the readme documentation above. (4)

9. Add a new teleportation mode that replaces the visual indicator from Part 7 with a visualization of the physical workspace around the user. An example of this can be found in Figure 4 (a) of this recently published [paper](https://canvas.umn.edu/files/16531915/download?download_frd=1).  For the purposes of this assignment, you can either assume a square rectangular workspace of 3m x 3m, or you can manually resize it to fit the estimated dimensions of the physical room you are working in.  This should be added as a fourth locomotion mode; do not replace the original teleportation technique. (4)

   *Note: You do not need to worry about setting the direction of the user in this teleport mode.  Although you can optionally add this functionality if you want, the new teleport mode only needs to change position for full credit.*

10. Add a mesh object that represents the position and orientation of the user within the workspace, as shown in Figure 4 (b) of the [paper](https://canvas.umn.edu/files/16531915/download?download_frd=1) cited in Part 9. (2)

    *Hint: You can access the transform of the headset tracker relative to the origin of the physical workspace with the following ridiculously long line of code:*

    `this.xrSessionManager!.currentFrame?.getViewerPose(this.xrSessionManager!.baseReferenceSpace)?.transform`

**Bonus Challenge:** The current teleportation implementation only works when a ray cast intersects a ground mesh.  Extend this functionality so that you can teleport using a parabolic arc when a straight line teleport is not possible, similar to the default teleportation in Babylon. Note that this is technically challenging, and there are multiple ways to implement a parabolic arc.  For example, you could try using a [Curve3](https://doc.babylonjs.com/how_to/how_to_use_curve3) to generate intermediate points for multiple ray casts, or you can try to replicate the implementation in [WebXRControllerTeleportation](https://github.com/BabylonJS/Babylon.js/blob/master/src/XR/features/WebXRControllerTeleportation.ts). (2 points)

Make sure to document all third party assets. ***Be aware that points will be deducted for using third party assets that are not properly documented.***

## Submission

You will need to check out and submit the project through GitHub classroom.  The project folder should contain just the additions to the sample project that are needed to implement the project.  Do not add extra files, and do not remove the `.gitignore` file (we do not want the "node_modules" directory in your repository.)

**Do not change the names** of the existing files.  The TA needs to be able to test your program as follows:

1. cd into the directory and run ```npm install```
2. start a local web server and compile by running ```npm run start``` and pointing the browser at your ```index.html```

Please test that your submission meets these requirements.  For example, after you check in your final version of the assignment to GitHub, check it out again to a new directory and make sure everything builds and runs correctly.

## Local Development 

After checking out the project, you need to initialize by pulling the dependencies with:

```
npm install
```

After that, you can compile and run a server with:

```
npm run start
```

Under the hood, we are using the `npx` command to both build the project (with webpack) and run a local http webserver on your machine.  The included ```package.json``` file is set up to do this automatically.  You do not have to run ```tsc``` to compile the .js files from the .ts files;  ```npx``` builds them on the fly as part of running webpack.

You can run the program by pointing your web browser at ```https://your-local-ip-address:8080```.  

## Build and Deployment

After you have finished the assignment, you can build a distribution version of your program with:

```
npm run build
```

Make sure to include your assets in the `dist` directory.  The debug layer should be disabled in your final build.  Upload it to your public `.www` directory, and make sure to set the permissions so that it loads correctly in a web browser.  You should include this URL in submission information section of your `README.md` file. 

This project also includes a `deploy.sh` script that can automate the process of copying your assets to the `dist` directory, deploying your build to the web server, and setting public permissions.  To use the script, you will need to use a Unix shell and have`rsync` installed.  If you are running Windows 10, then you can use the [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10).  Note that you will need to fill in the missing values in the script before it will work.

## License

Material for [CSCI 5619 Fall 2020](https://canvas.umn.edu/courses/194179) by [Evan Suma Rosenberg](https://illusioneering.umn.edu/) is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-nc-sa/4.0/).

The intent of choosing CC BY-NC-SA 4.0 is to allow individuals and instructors at non-profit entities to use this content.  This includes not-for-profit schools (K-12 and post-secondary). For-profit entities (or people creating courses for those sites) may not use this content without permission (this includes, but is not limited to, for-profit schools and universities and commercial education sites such as Coursera, Udacity, LinkedIn Learning, and other similar sites).   

## Acknowledgments

This assignment was partially based upon content from the [3D User Interfaces Fall 2020](https://github.blairmacintyre.me/3dui-class-f20) course by Blair MacIntyre.



