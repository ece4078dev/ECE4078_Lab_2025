# Final Demo

## Introduction
The [task](../Week09-10/README.md#introduction) for the final demo is the same as stated in C2.

## Marking procedure
The final demo marking [procedure](../Week09-10/C2_marking.md#marking-steps) and [rules](../Week09-10/C2_marking.md#4-rules) is the same as your trial run in C2. However please look at the key changes in [C2_marking.md](../Week09-10/C2_marking.md#key-changes-for-final-demo) and the [README.md](../Week09-10/README.md#key-changes-for-final-demo) in Week09-10.

---

## Final Demo marking scheme

### 1. Demo duration
- The total duration of your Final Demo will be 30 minutes.  
- The marking schedule will be published to the [Scheduling sheet](https://docs.google.com/spreadsheets/d/1X3cr0gBKZy2VaotczIgovOc5Q4cgQa3NROwMl_u-cKw/edit?usp=sharing), similar to previous milestones.  
- All teams will need to submit their codes on [Moodle](https://learning.monash.edu/mod/assign/view.php?id=4245868) before the start of the live demo marking lab session, and submit their generated maps on [Moodle](https://learning.monash.edu/mod/assign/view.php?id=4245867) at the end of their Final Demo.  
- Within this 30 minutes, you need to perform the demo, reset the arena in between runs if needed, and submit your generated SLAM and targets maps with the required format and file names.  
  - You will be given time prior to the start of your demonstration to download and setup your code

## 2. Final Demo Levels
The final demo is separated into three levels, these levels are:
- Level 1: Manual Mapping and Fully-Autonomous Navigation as separate tasks
	- The robot can be teleoperated for the Mapping task
	- The robot must navigate around the arena autonomously
	- You must navigate to targets on the shopping list in the specified order
- Level 2: Manual Mapping and Fully-Autonomous Navigation with Swapped Objects as separate tasks
	- The robot can be teleoperated for the Mapping task
	- The robot must navigate around the arena autonomously
	- After mapping occurs, target and/or obstacles objects will change locations
    - For location changes the following can occur:
      - Shifting object locations around the original location
      - Swapping locations of different objects in the environment
    - You may navigate to objects in any order. Shopping list information and the robot's intention from level 3 is applied here too.
- Level 3: Fully-Autonomous Mapping and Navigation
	- The robot performs simultaneous mapping and navigation around the arena autonomously as a single task
	- You may navigate to objects in any order
	- You are still provided a shopping list, but you do not need to navigate to the targets in the same order as the list. Due to the removal of shopping list order, you must clearly indicate if the robot is stopping for an object by printing the label of the specified object to terminal and notifying the TA of the robot's intention to stop at the specific target. 

For Levels 1 and 2, mapping and Navigation are treated as 2 separate tasks and you can attempt mapping and navigation runs in any order given a mapping run comes first. For level 3, mapping and navigation are considered a single combined task. An example order for the final demo could be to manually map once, attempt navigation twice, map again and then attempt simultaneous mapping and navigation (level 3) for a total of 5 runs (2 manual mapping runs, 2 autonomous navigation runs and 1 simultaneous mapping and navigation run). Inbetween any run, the arena will be reset (or rearranged in the case of displacing fruits/veg from level 2 navigation to any other task) for the current task.

### 3. Marking scheme breakdown
The Final Demonstration contributes 60% of the overall unit grade. This is divided into the following components with the mark breakdown out of 100%:

1. SLAM (M1) – 15/100:
  * Assessed using scaled [marking formula](../Week02-04/M1_marking_instructions.md#Evaluation-scheme) from Milestone 1:
    * slam_rating = ((0.2 - Aligned_RMSE)/(0.2 - 0.02))
    * slam_score = (base^slam_rating - 1)/(base -1) * 15, where base = 16

2. Target List (M2) – 15/100:
  * Assessed using scaled [marking formula](../Week05-06/M2_marking.md#Evaluation) from Milestone 2:  
    * target_accuracy_rating[object] = (0.5 - estimation_error[object])/(0.5-0.025)
    * target_est_score = (base^mean(target_accuracy_rating) - 1)/(base - 1) * level_scale - 5 x NumberOfCollisions
    * 0 ≤ target_est_score ≤ level_scale

3. Navigation – 70/100:  
   * The following marks are allocated for qualified runs and successful collections. Note that there are some small changes to the definition for a qualified run described in [Section 4](#4-qualified-navigation-run-and-penalty-scheme-changes).

   - Level 1  
     + 15 marks awarded for a qualified run.  
     + Each successful collection (within 0.3 m, in the correct shopping list order) is worth 5 marks.  
     + Maximum contribution: 40% of 70%.  

   - Level 2  
     + 25 marks awarded for a qualified run.  
     + Each successful collection (within 0.3 m, in any order) is worth 5 marks.  
     + Maximum contribution: 50% of 70%.  

   - Level 3  
     + 30 marks awarded for a qualified run.  
     + Each successful collection (within 0.3 m, in any order) is worth 8 marks.  
     + Maximum contribution: 100% of the Navigation mark (i.e. full 70%).  
     
4. Overall Mark = (slam_score + targets_score + navigation_score) * Viva_Factor * ITP_Factor
  * **Note that students that do not fill in the Viva will have their ITP factor capped at 0.9**

### 4. Qualified navigation run and penalty scheme changes

- For Level 1, a qualified navigation run requires 3 **valid navigation attempts** to targets in the order specified in the shopping list.  
- For Level 2/3, a qualified navigation run requires 3 or 4 (respectively) **valid navigation attempts** to targets in the shopping list in any order.  
- For each target a **valid navigation attempt** is defined by the whole robot stopping within 0.5m of the center of the object. Marks are only awarded if the robot stops within 0.3 m of the target.  

- Stopping the run  
  * After meeting the qualification threshold (3 or 4 targets, depending on level), the run may be stopped at any time, either manually or when the program ends, and the marks earned so far will be retained.  
  * For example, in a Level 1 run, if the robot successfully navigates to the first two targets (within 0.3 m) but only stops within 0.5 m of the third, the run still qualifies. The score would be 15 points for a qualified run plus 6 points for each of the two successful targets, totalling 27 points.  
- Similarly to M3, qualification marks cannot be effected by penalties.

- Collision rules and penalties  
  * The same collision rules and penalties as in M3 will apply.  
  * Manual resetting of the robot or arena during any run (e.g. moving a marker block) is prohibited.  
  * For Levels 1 and 2 mapping runs:  
    - Penalties do not apply to mapping runs, however you cannot reset the arena during a mapping run.  
  * For Level 3 and Level 1/2 Navigation runs:   
    - Any manual interference with program execution after the run is launched with a single command will immediately terminate that run.  

### 5. Individual contributions to team and mark scaling
- The 3rd and last ITP survey will be open from 10am 27 Oct to 6pm 31 Oct. The results will be used to inform the individual scaling factors applied to thr Final Demo's team scores. **Failure to complete this will result in your mark being capped to 0.9.** 
- We will conduct individual vivas and code reviews as part of the final assessment to understand an individual's contribution to the team. The viva results will be used to adjust the individual scaling factor. The vivas will be scheduled during your final demo session.  

### 6. Other
- The Final Demo will be video recorded. We may record the arena, the robot's behaviours inside the arena, your computer screens or keyboard actions. We will not record any people or faces. Any accidental recordings of personal information irrelevant to the Final Demo or the unit will be deleted.  
- We will prepare a small number of back-up robots with calibrated wheel and camera parameters ready to use with them. During the Final Demo, if a team has unexpected hardware issues they may switch to use these back-up robots. While switching and reconnecting to the back-up robot the demo timer will be paused.  

---

## Further clarifications and FAQs

Below are issues that we have seen during teams' C2 runs which may be helpful to address:

1. Have a back-up plan. For example, implement a command line argument for switching between running semi or full auto navigation in case the full auto navigation crashes on the day. Also have a back-up driver and laptop.  
2. Parameter tuning: check your wheel and camera parameters, YOLO confidence, SLAM covariance, radius around markers and objects for creating occupancy map, etc. We recommend recalibrating the wheel and camera during the Week 11 labs and check to make sure that your calibrated parameters are close to the [default parameters](../Week02-04/calibration/param/).  
3. Try different map layouts and pay attention to when collisions might happen due to path finding not optimised or occupancy map radius not being able to handle inaccurate maps.  
4. Make sure to submit the right version of your codes containing all required components. Test to ensure that the codes work as expected.  
5. We are still seeing map syntax and naming errors in the submitted 'slam.txt' and 'targets.txt' which might result in 0pt mapping scores. Please make sure to check the maps generated and submit the generated maps that you want to be marked on.  
6. Check if your EKF is correctly integrated and that your SLAM is correctly implemented.  
7. Some groups had their generated SLAM map rotated or flipped on the x/y axis, please check this with practice arenas. With the robot's camera facing left when positioned in the middle of an arena, the left half of the arena will have positive x coordinates, and the bottom half of the arena will have positive y coordinates.  
8. Practice your runs and discuss driving strategies with your teammates to reduce operator errors (e.g., pressing wrong buttons or giving wrong commands).  
9. In a navigation run, distance of the 0.3 m radius for successful navigation and 0.5 m radius for qualified navigation is measured from the centre of the target, and the entire robot has to be within this radius.  
10. For Levels 2 and 3, an object can only be collected if the robot both stops close enough to it and the code explicitly indicates that the robot recognises it as the correct target. For example, if the robot is mapping and approaches a pear (which is on the shopping list), the program must output that it is stopping for a pear. If the robot simply stops near the pear without this clear indication from the code, the collection will not be counted.


