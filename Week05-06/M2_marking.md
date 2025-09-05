# Milestone 2: Marking
- [Evaluation](#evaluation)
- [Live demo marking steps](#live-demo-marking)
- [Live demo marking checklist](#marking-checklist)

---


## Evaluation
Your M2 score consists of two parts: the accuracy of your YOLO detector for classifying the type of a target object, and the accuracy of your estimated map containing the location of the 10 targets in the arena.

The performance of your YOLO detector worths 30pts. You'll demonstrate your trained YOLO model on a set of 10 testing images. The detector evaluation is run on your computer without using the robot (pass the set of marking images to your trained YOLO model and show a visualisation of the predicted bounding boxes and labels). Each image may contain up to 4 fruits/vegetables. Some are **targets**, and some are **distractors**.

The score for each image is determined as follows:

#### 3 points – An image is marked correct only if:
- All targets are detected with bounding boxes that clearly cover the majority of the object (at least two-thirds of it) and have the correct class labels.  *Some examples of what will be considered acceptable can be found below.*  
- No targets are missed.  
- No distractors are detected (i.e. nothing drawn around fruits/vegetables that are not in the target list).

#### 0 points – If there is any mistake in that image, including:
- A target is not detected  
- A target is detected but given the wrong label  
- A distractor is incorrectly detected  
- Any extra/false detections  

**Example:**  
If an image contains a pear (target), a lemon (target), and a lime (distractor), you will only receive 3 points if your detector produces bounding boxes with correct labels for both the pear and the lemon, and does not produce any detection for the lime.  

You will receive 0 points if the lime is detected, if either the pear or lemon is missed, if either is detected with the wrong label, or if any extra bounding box appears.

#### Examples of Correct vs Incorrect Bounding Box Sizes

Below are example outputs showing what is considered an acceptable bounding box size and placement. The **two leftmost image** are correct (3 points). All others are unacceptable (0 points).

<p align="center">
  <img src="Screenshots/bounding_box_good.png" alt="Correct bounding box" width="150"/>
  <img src="Screenshots/bounding_box_good_1.png" alt="Correct bounding box" width="150"/>
  <img src="Screenshots/bounding_box_bad_1.png" alt="Wrong bounding box 1" width="150"/>
  <img src="Screenshots/bounding_box_bad_2.png" alt="Wrong bounding box 2" width="150"/>
  <img src="Screenshots/bounding_box_bad_3.png" alt="Wrong bounding box 3" width="150"/>
  <img src="Screenshots/bounding_box_bad_4.png" alt="Wrong bounding box 4" width="150"/>
</p>

#### Dispute Resolution
All object detection results will be checked and marked during the lab.  
If you believe there is an issue with how your detections are assessed, you must raise it **on the spot** with the teaching staff. Disputes will not be reviewed afterwards, so make sure to clarify any concerns during your lab session.

~~~
detector_score = 3 x NumberOfCorrectPredictions
0 ≤ detector_score ≤ 30
~~~

[mapping_eval.py](mapping_eval.py) is used to evaluate performance of your target pose estimation. It requires both the SLAM map ```lab_output/slam.txt``` and the targets map ```lab_output/targets.txt```. Run 
```
python3 mapping_eval.py
```
This computes the Euclidean distance between each target's true location in "true_map.txt" and its closest estimation in "lab_output/targets.txt" (the estimation error). It also generates an estimation on your SLAM's performance as error in SLAM will impact your target pose estimation performance. The SLAM map is used to align the object pose estmation as well.

"targets.txt" should contain the poses of all 10 fruits and vegs in the arena. **Make sure your modified "TargetPoseEst.py" generates a "targets.txt" file that is in the same format as the [given example output](lab_output/targets.txt)**. Generating the estimation map in a wrong format **WILL** result in it not being compatible with the evaluation scripts and thus getting 0pt for M2 target_est_score.

Please note that [mapping_eval.py](mapping_eval.py) is case sensitive. All target labels in your generated estimation map should be in lower case as shown in the [example est map](lab_output/targets.txt) and the groundtruth maps on github, e.g., use "lemon" instead of "Lemon" or "LEMON". If you've made a typo when labelling your YOLO training dataset, please make sure to edit your TargetPoseEst.py so that the printed estimation map is in the correct format.

**[New] Note that the indices of the fruit and veg in the map do not matter in this script, it will attempt to find the minimum error where possible, however, if your map has too many of a type of target, an average will be used instead.**

For M2, the object mapping task will also have 3 different difficulty levels with 3 different marking scales. These are as follows:

- Level 1: You will map an arena of 10 Aruco Markers and 10 Objects (There will be repetitions) (Max 40/70)
- Level 2: You will map the same arena as Level 1, however, objects will be swapped with a different coloured version (e.g swapping a red apple for a green apple) (Max 50/70)
- Level 3: You will map the same arena as Level 2. however, additional objects outside of the defined training set will be included within the environment (e.g if the set of objects is apple, orange and potato, we might add a tomato into the arena). These additional objects do not need to be mapped and cannot be trained for by your model. Max (70/70)

Your object mapping score is calculated with the formula below:

~~~
target_accuracy_rating[object] = (0.5 - estimation_error[object])/(0.5-0.025)
target_est_score = (base^mean(target_accuracy_rating) - 1)/(base - 1) * level_scale - 5 x NumberOfCollisions
0 ≤ target_est_score ≤ level_scale
~~~

**Note:** If the target_accuracy_rating of an object goes above the upper bound 0.5, the rating will be 0. If the target_accuracy_rating value goes below the lower bound 0.025, the rating will be 1, i.e., resulting in 0 ≤ target_est_score ≤ lv_multiplier.

There is also a 5pt collision penalty for each object, ARUCO marker or wall that you collide with during a demo run, with a maximum of 3 collisions allowed in a run.

Your M2 score is the sum of the detector performance score and the target pose estimation performance score minus penalties:

~~~
M2_score = detector_score + target_est_score - 3 x number_of_collisions
0 ≤ M2_score ≤ 100
~~~

We will also be conducting a viva (a short interview), to confirm each team member's understanding of the project milestones. Each member of the team will be individually interviewed about what has been developed. You will be required to answer questions based primarily on the software components you personally worked on. However, you are also expected to demonstrate some understanding of the other components developed by the group.

It is therefore important to be thoroughly prepared to explain your own contributions and have a basic understanding of how the other parts of the code fit into the overall project.

Total project marks will be scaled based on the level of understanding demonstrated in the Viva, with the full marks being no change and a reduction as the category code drops (see the table below for the marking criteria). Additionally, there will be an ITP peer factor scale applied to your individual marks. Your total for M2 will then be:

**Final_M2_Mark = M2_Mark * viva * ITP_Factor**

If you miss (do not attend) your project interview, you may receive a 0.

Viva Marking Criteria
---------------------

| Category Description     | Detailed Description                                                                                                                                                  |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Complete Understanding   | The student is clearly prepared and can answer questions concisely and correctly with little to no prompting about the parts they personally worked on. They also show a reasonable understanding of the rest of the codebase and how it connects to their contribution. |
| Tolerable Understanding  | The student has prepared and can answer mostly correct responses about their own work, though some clarification or prompting may be needed. They demonstrate limited understanding of the other parts of the code. |
| Selective Understanding  | The student can answer questions about some parts of their own work, but is clearly unprepared for other areas, either within their contribution or the broader system. Their preparation is insufficient or incomplete. |
| Trivial Understanding    | The student demonstrates only vague or superficial knowledge of their contribution, and is unable to engage with questions meaningfully. There is little or no awareness of the rest of the team's code. |
| No Understanding         | The student appears completely unprepared, shows no knowledge of the code, and cannot answer basic questions, even with assistance. May indicate they have not reviewed the work at all. |
| Absent                   | The student did not attend the viva interview for the project.                                                                                                         |


---

## Live demo marking
You have a **20min time limit** for M2 live demo marking, this includes time taken to download and unzip your submissions, to demonstrate your detector on a set of marking images, to demonstrate your target pose estimation by driving the robot around a marking arena, and to submit the generate maps.

### Marking steps
#### Step 1:
**Do this BEFORE your lab session**
Zip your M2 implementation and submit to the Moodle. Each group only needs one submission. This submission is due by the starting time of the lab session, which means you should **submit your script BEFORE you come to the lab**:
1. Include ALL scripts required for performing the fruit/veg detection and pose estimation in the zip, including the trained YOLO .pt model
2. Please DO NOT submit your training dataset or the python venv. If your trained YOLO model file is too big to upload to Moodle, please upload it to your Google Drive and provide a link to it in your README.txt
3. You cannot change the submitted scripts when running the live demo, except for replacing the [calibrated wheel and camera parameters](../Week02-04/calibration/param/), so make sure you submitted the right implementation version.
4. Your code may take in command line inputs unrelated to the arena / objects / markers / robot status. For example, your code may take in a run ID for automatically renaming the generated slam.txt and targets.txt to make sure the pairs are aligned.
5. We may review your code or ask you to explain your implementation.

**Tips:** 
- You can write a loop for the YOLO detector to take in all images in a directory instead of manually changing the image file name to speed things up.
- You may also include a text file in the zip with a list of commands to use, if you don't know all the commands by heart.
- **Please practise** the marking steps (eg. unzipping your code and running it) to ensure there are no issues during marking.
- Make sure your robot is fully charged before coming to the lab session.


#### Step 2: 
**Do this BEFORE the demonstrator marks your team**

1. Close all the windows/applications in your development environment

2. Use any team member's account to log in Moodle and navigate to the M2 submission box, so that you are ready to download your submitted code when the demonstrator arrives

3. Please turn on your robot before the demonstrator comes to you. DO NOT connect to its hotspot yet. 

#### Step 3:
**During marking**
Note: within the 20min marking time limit, you may perform detection of the marking images or target pose estimation as many times as you want. The attempt with the highest score will be your final detector_score and target_est_score. 

1. The demonstrator will set up the marking arenas containing the 10 ARUCO markers and 10 target objects at the beginning of the session. Note that each lab session will get slightly different map layouts. A set of 10 detector marking images will also be provided (each image containing one target object, a different set will be used for each lab session). **You are not allowed near the marking arena unless it is your team's turn for marking**

2. When the demonstrator ask you to come to the marking arena, download your submitted zip file from Moodle and unzip its content to the "`~/LiveDemo`" folder.

3. Navigate to the "Week05-06" folder in your unzipped submission which contains the operate.py script

4. Demonstrate your object detector by running your YOLO detector with the set of 10 marking images and show a visualisation of the bounding box and object label of each image. The demonstrator will record the number of correctly classified images for the detector_score. You may rerun this step as many times as you want within your marking time limit.

5. Connect to the robot and run the script with ```python3 operate.py --ip 192.168.50.1 --port 8080```

6. Demonstrate target pose estimation by **strategically** driving the robot around arena to observe all 10 targets, and then run TargetPoseEst.py to generate a map based on the observations
    - You may stop a run at anytime 
    - You may rerun this step as many times as you want within your marking time limit. **Remember that the map submission has to be done within the time limit**, so make sure you leave enough time for the submission. The 20min marking timer also continues when you are getting ready in between runs (resetting the robot to the start location and resetting any markers or objects that may have moved due to collision).
    - A visible effort has to be made to try and locate all 10 objects.
    - **The maximum number of collision/out-of-bound allowed in a run is 3 times**. The fourth time your robot collides with a marker, an object or the arena wall you will be asked to terminate that run and restart a new run if time permits and if you want to
    - Note that the provided skeleton code saves the map under the same name (i.e., the later run would replace map generated by the earlier run), so you'll need to manually rename the maps in between runs, or modify the map-saving codes when developing your solution.
    - You are not allowed to change anything in the downloaded submission of your implementation, except for the camera and wheel calibration parameters. Your code can also take in arguments at the time of execution. However, you are NOT allowed to give inputs related to the arena setup or object locations/types as command line arguments, an extreme example would be typing in the whole map manually as command line arguments (please don't). 
    - Switching between levels will be included within your demo time, so try to limit level switches to 1 or 2 times maximum.

7. Submit the generated slam.txt and targets.txt maps (make sure SLAM and target maps are matching pairs for each run and that you only submit one pair per run) as a zip to the Moodle map submission box for target_est_score marking

8. Individual viva (short verbal assessment with the demonstrator) will be conducted, which will be used to scale your mark. See [example est map](../Week02-04/M1_marking_instructions.md) for more information. Furthermore, the same ITP across M2 and M3 will be used to scale your final M2 mark. Your total for M2 will be:

**Final_M2_Mark = M2_Mark * viva * itp_score**

---

### Marking checklist
**BEFORE the lab session**
- [ ] Submit your code to Moodle
- [ ] Charge the robot

**BEFORE the marking**
- [ ] Close all programs and folders
- [ ] Log in Moodle and navigate to the submission box
- [ ] Open an empty folder named "LiveDemo" (located at ```~/LiveDemo/```)
- [ ] Turn on the robot (DO NOT connect to its hotspot yet)

**During the marking** (20min time limit)
- [ ] Demonstrator will ask you to download your submission and unzip it to "LiveDemo"
- [ ] Demonstrate detector performance by running YOLO with the marking image set
- [ ] Connect to the robot
- [ ] Demonstrate target pose estimation (rename the ```lab_output/slam.txt``` and ```lab_output/targets.txt``` files by run ID, max 3 collisions/out-of-bound per run) and good luck!
- [ ] zip and submit the map(s) to Moodle
