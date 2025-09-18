# M3 Evaluation and Marking Instructions 

The arena will contain 10 ArUco markers and 10 fruits&vegs. The full, partial, and minimal true maps and the shopping list of the 5 targets will be given to you at the start of each lab. The marking arena in each lab session will be slightly different and will be different from the practice arena.

Each team will have a **STRICT** time limit of 15min for the live demo marking, according to this [marking schedule](https://docs.google.com/spreadsheets/d/1X3cr0gBKZy2VaotczIgovOc5Q4cgQa3NROwMl_u-cKw/edit?gid=0#gid=0).

You should first demonstrate the level you are confident with before attempting a more challenging level. You may demonstrate any levels as many times as you want within the 15min live demo time limit. In most cases, students only do 2-3 attempts. You may switch levels during the 15-minute run but the timer will continue to count as you make that decision.

- [Evaluation](#evaluation)
	- [Level 1: Semi-auto navigation using waypoints](#level-1-semi-auto-navigation-using-waypoints)
	- [Level 2: Autonomous navigation with a known map](#level-2-autonomous-navigation-with-a-known-map)
	- [Level 3: Autonomous navigation with a partially known map](#level-3-autonomous-navigation-with-a-partially-known-map)
    - [Level 4: Autonomous navigation with a minimally known map](#level-4-autonomous-navigation-with-a-minimally-known-map)
- [Marking steps](#marking-steps)
- [Marking checklist](#marking-checklist)

---

## Evaluation
We have divided M3 into 4 levels based on the 4 main components which you could attempt. These levels are:
- Level 1: Semi-autonomous navigation using waypoints (50 pts)
	- The full ground truth of the arena is provided
	- You may only control the robot by providing waypoints (No Teleoperation in this demo!)
	- You must navigate to targets on the shopping list in the specified order
	- **Note waypoint navigation will not be available for the final demo**
- Level 2: Fully-autonomous navigation with a known map (20 pts)
	- The full ground truth of the arena is provided
	- The robot navigates around the arena autonomously
	- You must navigate to targets on the shopping list in the specified order
- Level 3: Fully-autonomous navigation with a partially known map (15 pts)
	- A partial ground truth of the arena is provided
	- The map only contains the locations of the ArUco markers and the shopping list objects
	- The robot navigates around the arena autonomously
	- You must navigate to targets on the shopping list in the specified order
- Level 4: Fully-autonomous navigation without any known fruit/veg locations (15 pts)
	- A ground truth map of only the ArUco markers is provided
	- The robot navigates around the arena autonomously
	- You may navigate to objects in any order
	- You are still provided a shopping list, but you do not need to navigate to the targets in the same order as the list. Due to the removal of shopping list order, you must clearly indicate if the robot is stopping for an object by printing the label of the specified object to terminal and notifying the TA of the robot's intention to stop at the specific target. 

For each level in M3, you will receive all the potints allocated to lower levels if you can achieve a [qualified navigation run](Week07-08/M3_marking.md#evaluation)

**IMPORTANT!!** The following rules apply:
1. Penalty of -5pts for each fruit/veg that the robot collides with

2. Penalty of -5pts for each ArUco marker that the robot collides with

3. Penalty of -5pts each time the robot touches the arena boundary 

4. If you have received 5 penalties (any of the penalties listed above) during a run, your run must stop.

5. The **condition** to be eligible to gain points for your run is determined by achieving a **qualified** run. For a **qualified** run we define stopping within a 0.3m radius qualifies navigation as a **success** and stopping within a 0.5m radius qualifies a navigation as a **valid attempt**. A run is deemed **qualified** if it has at least any number of **successes** and/or **valid attempts**  equal to the attempted level + 1 (e.g levels 2/3/4 require 3/4/5 **successes** or **valid attempts**). After a **qualified run** is declared you will receive at all points allocated to the lower level/s. Additionally, **valid attempts** only apply in order navigation for levels 2 and 3.
	- For all levels except level 4, points for navigating successfully to a target will only be given for **successful** navigation to targets navigated within the correct order.  	
	- Penalties will only apply to successful navigation points (i.e if a level 2 run is **qualified** with 4 **successes** and 4 penalties, you will still receive 50 points)
	- You may stop/cancel a run at any point, however if the robot is stopped (also by the robot itself or by having recived 5th penalty) before a run is **qualified**, you will receive zero points for that run. 
 	- Once the run is stopped, your mark for the run is finalised.

6.  In the case of a **success** or a **valid attempt** the **entire** robot has to stop for approximately 2 seconds within the specified radius of the target, measured from the center of the target, to be considered as a successful navigation or valid attempt respectively.

7. You will not receive any points for targets navigated out of order in levels 1-3. For example, Successful navigation in the following order, 1,3,2,4,5, will only result in points for 4 successful navigations. 

8. We will review your code to see if you have implemented appropriate algorithms for the levels you have attempted. To gain credit for level 2-4, we must find evidence of path planning, or obstacle detection and avoidance (respectively) in your code. Successfully navigating to targets and/or avoiding collisions at these levels by luck will not grant you those points by default

9. The best run/attempt will be considered as your M3 score

10. If you are performing semi-automatic navigation (Level 1), the waypoints you can provide are x,y coordinates. You can't specify driving instructions, such as distance / time to drive, or turning angles

11. The robot must start at the origin (0,0,0). You can't teleoperate or manually place the robot next to the first target when starting the navigation.

### Level 1: Semi-auto navigation using waypoints
To attempt Level 1, the locations of all the objects in the arena will be given to you in the full groundtruth map. The search order of the target fruits is given in the shopping list.

You are **not allowed to teleoperate** the robot. You can only enter coordinate of the waypoints as input, or you may choose to do so via a GUI. You can input as many waypoints as you want to get to the targets. 

The entire robot needs to be within 0.3m of the target and stop for 2s to indicate that it has found a target fruit/veg before moving onto the next target. You will get 0pt for a target if the robot is not within 0.3m of the target. You should confirm with the demonstrator to check whether the robot is close enough to the target. You will also need to reach the end condition (see above) for a run to qualify for marks.

Each target that you successfully navigate to will give you 10pt if you decide to perform Level 1:
``` 
level1_score = 10 x NumberOfSuccessNav - 5 x NumOfPenalty
0 ≤ level1_score ≤ 50
```

### Level 2: Autonomous navigation with a known map
To attempt Level 2, the locations of all the objects in the arena will be given to you in the full groundtruth map. The search order of the targets is given in the shopping list. You are only allowed to enter a **single command** to launch the navigation program and the robot should perform the task autonomously. 

If you decide to perform Level 2 and achieve a **qualified run**, you will inherit all of Level 1 points, and for each target you have successfully navigated to in Level 2 receive an additional 4pts:
``` 
level2_score = 50 + 4 x NumberOfSuccessNav - 5 x NumOfPenalty
50 ≤ level2_score ≤70
```

### Level 3: Autonomous navigation with a partially known map
To attempt Level 3, the locations of all 10 markers and the 5 targets in the arena will be given to you in the **partially known** groundtruth map. The search order of the targets is given in the shopping list. The locations of the other 5 objects will **not** be provided in this partial map and you are not allowed to use the full groundtruth map in any part of the implementation to attempt Level 3. If you are found to use the full groundtruth map in your Level 3 implementation you will receive 0pt for M3. You are only allowed to enter a **single command** to launch the navigation program and the robot should perform the task autonomously. 

If you decide to perform Level 3 and achieve a **qualified run**, you will inherit all of Level 1 and Level 2 points, and for each target you have successfully navigated to in Level 3 receive an additional 3pts:
``` 
level3_score = 70 + 3 x NumberOfSuccessNav - 5 x NumOfPenalty
70 ≤ level3_score ≤ 85
```

### Level 4: Autonomous navigation with a minimally known map
To attempt Level 4, the locations of only the 10 markers in the arena will be given to you in the **minimally known** groundtruth map. You do not need to search in any specific order. The locations of the all target or obstacle objects will **not** be provided in this partial map and you are not allowed to use the full groundtruth map in any part of the implementation to attempt Level 4. If you are found to use a map in your Level 4 implementation which contains any of the target or obstacle objects you will receive 0pt for M3 and a case of breaching academic integrity will be submitted. You are only allowed to enter a **single command** to launch the navigation program and the robot should perform the task autonomously. 

If you decide to perform Level 4 and achieve a **qualified run**, you will inherit all of Level 1, Level 2 and Level 3 points, and for each target you have successfully navigated to in Level 4 receive an additional 3pts:
``` 
level3_score = 85 + 3 x NumberOfSuccessNav - 5 x NumOfPenalty
85 ≤ level3_score ≤ 100
```

### Penalties
Note that any penalty will incur -5 pts but will only apply to points gained through successful navigation (e.g if a level 2 run is **qualified** with 4 **successes** and 4 penalties, you will still receive 50 marks)
---

### Marking instructions
You may open up the marking checklist during the live demo marking, which is a simplified version of the following steps to remind yourself of the marking procedures. 

You MUST follow all the evaluation rules outlined [above](#evaluation), make sure you check out all the rules and understand all of them. 


### Marking steps
#### Step 1:
**Do this BEFORE your lab session**

Zip your implementation and submit via the Moodle submission box (include all scripts that are relevant, such as the wheel and camera calibration parameters, your SLAM component, your trained YOLO detector, custom GUI for waypoint selection, etc). Each group only needs one submission. This submission is due by the starting time of the lab session, which means you should **submit your script BEFORE you come to the lab**. 

**Tips:** 
- You may also include a text file in the zip with a list of commands to use, if you don't know all the commands by heart.
- Practise the marking steps (e.g. unzipping your code and running it) to ensure there are no issues during marking.
- You may update the wheel and camera calibration parameters in the submission at the time of marking. All other scripts in your submission will need to be used as-is.

**Important reminders:**
- The code submission is due **before the start** of your marking lab session (NOT before you run your live demo), e.g., for the Thu 3pm lab session the code submission deadline will be Thu 3pm. You will NOT be allowed to perform the live demo marking if you didn't submit your codes on time, unless a special consideration has been granted. Don't wait until the last minute and cut your submission too close.
- You will NOT be able to change the codes after submission, except for the calibrated wheel and camera parameters (baselin.txt, scale.txt, intrinsic.txt, distCoeffs.txt). You will NOT be allowed to fix any typos, target label naming errors, generated maps formatting issues, indentation errors, missing files, scripts with wrong names, wrong implementation versions, wrong model weight files etc. in your submission at the time of live demo and will have to **run your downloaded code submission AS IS**.

#### Step 2: 
**Do this BEFORE the demonstrator come to mark your team**

1. Close all the windows/applications

2. Use any team member's account to log in Moodle and navigate to the M3 submission box, so that you are ready to download your submitted code when it's your group's turn to run the live demo

3. Calibrate your robot if needed (you can replace the wheel and camera calibration parameters in the downloaded submission)

4. Connect to eduroam/internet so that you are ready to download your submission from Moodle. Don't connect to the physical robot just yet

#### Step 3:
**During marking**

**Note**: You may attempt any level you want, and you should make it clear to the demonstrator which level you are attempting. Within the 15min marking time limit, you may have as many attempts as you want. The attempt with the highest score will be your final M3 score. 

1. The demonstrator will release the full, partial, and minimal true maps and the shopping list for each marking arena via Slack at the beginning of each lab session. Note that each lab session will have slightly different marking maps, and the marking maps are different from the practice map provided in the repo. Make sure that the correct true map is used when running your M3 demo

2. When it's your group's turn, go to the marking arena, download your submitted zip file from Moodle and unzip its content to the "`~/LiveDemo`" folder. 

3. Place the true map of your marking arena inside your unzipped submission folder. 
    
4. Connect to the robot.

5. Open a terminal, or a new tab in the existing terminal, navigate to the submission folder and run your M3 script by running [auto_fruit_search.py](auto_fruit_search.py) or whichever script(s) you need for the your chosen level to attempt
    - you may take the full or partial true map and the shopping list as the input files, depending on the level that you are attempting
    - note that [auto_fruit_search.py](auto_fruit_search.py) takes in command line arguments so that you can use the "--map" flag to specify the name of the map file that it uses. If you have implemented your own navigation scripts please make sure that it also uses a command line argument to specify the map to be used.

6. For Level 1, you may enter as many waypoints as you want. For Level 2 or 3, you can only input a single command to start the autonomous navigation program
    - We will review your code and you will receive 0pt for M3 if we find that you are teleoperating the robot or used the full true map in Level 3

7. Repeat any level as many times as you want until the time limit

8. Individual viva (short verbal assessment with the demonstrator) will be conducted, which will be used to scale your mark. See [example est map](../Week02-04/M1_marking_instructions.md) for more information. Furthermore, the same ITP across M2 and M3 will be used to scale your final M3 mark. Your total for M3 will be:

**Final_M3_Mark = M3_Mark * viva * itp_score**

---

### Marking checklist
**BEFORE the lab session**
- [ ] Submit your code to Moodle

**BEFORE the marking**
- [ ] Close all programs and folders
- [ ] Login Moodle and navigate to the submission box
- [ ] Open the folder named "LiveDemo"
- [ ] Calibrate the robot if needed
- [ ] Connect your Wifi to eduroam/internet so you are ready to download the submission

**During the marking** (15min time limit)
- [ ] True maps and shopping list for your session will be released
- [ ] Demonstrator will ask you to download your submission and unzip it to "LiveDemo"
- [ ] Copy the true maps (and the calibration files if you re-calibrated)
- [ ] Connect to robot
- [ ] Run your navigation program, announce to the demonstrator which level you are attempting
- [ ] Enter as many waypoint as you want for level 1, but only a single command for levels 2, 3, or 4
- [ ] Run navigation as many times as you want and good luck!

