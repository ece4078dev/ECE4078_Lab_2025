# Checkpoint 2: Integrated System (Final Demo Trial Run)
- [Introduction](#introduction)
- [Tips](#tips)
- Marking: see [C2_marking.md](C2_marking.md)

**Please note that all skeleton codes provided are **for references only** and are intended to get you started. They are not guaranteed to be bug-free either. To get better performance please make changes or write your own codes and test cases. As long as your codes perform the task and generate estimation maps that can be marked according to the evaluation schemes and scripts you are free to modify the skeleton codes.**

## Key Changes for Final Demo
With the release of the final demo, we just want to highlight some key changes in this document:
- The in-order requirement is now removed from level 2
- Restated 1 set of maps per run requirement

---
## Introduction
Checkpoint 2 (C2) is designed to give you time to integrate all of the modules you completed in the previous milestones and an opportunity to practice the final demo. It integrates your work from M1 to M3 so that the robot can create a map of the arena containing the estimated poses of 10 ArUco markers ([M1: SLAM](../Week02-04/)), 10 objects ([M2: Object Recognition and Localisation](../Week05-06/)), to then perform the grocery shopping task ([M3: navigation](../Week07-08/)). 

For **C2**, we will ask that you go through the whole marking process for the **final demo**, including download from Moodle and map upload, to ensure that your team has practice with the marking procedure for it. The procedure will not be marked or timed and is also designed as an opportunity to provide specific instruction on the logistics of the **Final Demo** and so will not involve proper attempts at the task. This will involve TAs viewing the file structure of your code submissions, the locations that the code is running in, how to name and submit your mapping files and any other logistics around the final demo. 

For the **Final Demo**, you will be given a shopping list of 5 targets, your task is to perform SLAM, localise objects and navigate to the given list of fruits&vegs, while avoiding obstacles along the way. The robot should attempt to stop within 0.3m radius of the intended target for 2 seconds before moving onto the next target. You need to indicate your intended target, via terminal or other means you have mentioned to the TA.
- **A true map will NOT be provided in the final demo**, only a shopping list will be provided indicating which 5 targets are to be reached and in which order if applicable
- You may teleoperate your robot (C1) to first generate a map of the arena with your own SLAM (M1) and detector (M2) before performing the navigation (M3), however you will be awarded more marks if you can map the arena autonomously (level 3).
- There will be 10 ArUco markers and 10 objects (5 as navigation targets, 5 as obstacles) in the arena. Similar to M3, the targets on the shopping list will be unique while the obstacles may contain duplicates.

For the final demo, the task will be separated into 3 levels. These levels are:
- Level 1: Manual Mapping and Fully-Autonomous Navigation
- Level 2: Manual Mapping and Fully-Autonomous Navigation with object displacement.
- Level 3: Fully-Autonomous Mapping and Navigation

For Levels 1 and 2, mapping and Navigation are treated as 2 separate tasks and you can attempt mapping and navigation runs in any order given a mapping run comes first. For level 3, mapping and navigation are considered a single combined task. An example order for the final demo could be to manually map once, attempt navigation twice, map again and then attempt simultaneous mapping and navigation (level 3) for a total of 5 runs (2 manual mapping runs, 2 autonomous navigation runs and 1 simultaneous mapping and navigation run). Inbetween any run, the arena will be reset (or rearranged in the case of displacing fruits/veg from level 2 navigation to any other task) for the current task. In the final demo, your score would then be the highest score of your:
- Highest scoring manually generated set of maps added with the highest scoring level 1/2 navigation run
or your:
- Highest scoring Level 3 attempt (slam_score + object_est_score + navigation score)
**The final demo will follow the same procedure** that C2 allows teams to practice the marking steps and also allow teams and TAS identify any potential logistical issues which teams could face.

**Important notes**:
- As usual, you are not allowed to use true poses of robot or objects during mapping, manually interfere with the robot or the arena, or teleoperate and provide waypoints to the robot during navigation during a demonstration
- You will not be allowed to run your code within any **cloud-based folders (e.g OneDrive, iCloud etc.)** due to potential issues with file permissions
- For the code submission of the final demo, you may be penalised if your submission does not **contain what is strictly necesssary to run your code**. For an idea of what is unnecessary, your submission should not include files/folders from the following non-exhaustive list:
    - Training Images
    - Old mapping outputs (slam.txt, targets.txt etc.)
    - Folders from prior milestones (e.g do not include Week00-01, Week02-04 etc.)
- For map submissions in the final demo, we will require you that you label and number your mapping output files as "slam_manual_{mapping_no}.txt" and "targets_manual_{mapping_no}.txt" for manually generated map pairs or as "slam_auto_{navigation_no}.txt" and "targets_{navigation_no}.txt" for autonomously generated map pairs. For example, if you perform two manual mapping runs, attempt Level 1 navigation and then a level 3 fully autonomous mapping and navigation run, in that order, the files would be labeled:
    - slam_manual_1.txt
    - slam_manual_2.txt
    - slam_auto_2.txt
    - targets_manual_1.txt
    - targets_manual_2.txt
    - targets_auto_2.txt
- You are only allowed to submit one slam.txt and one targets.txt per attempt. We take the best slams.txt and targets.txt from one attempt, and navigation score from another attempt and from the same level requirements. This means you cannot:
    - Mix a level 3 navigation score with a manual mapping (level 1/2) score.
    - Mix a level 3 mapping score with a level 1/2 navigation score.
    - Mix a level 3 navigation score with the mapping score of another level 3 attempt.
- We understand that this can be a lot to do during a short window of your Final Demo, which is why C2 is in place to give you a risk-free opportunity to practice the demonstration and submission process.
- **PLEASE COMMENT YOUR CODE**. We do perform spot checks and this allows us to identify if there are, or clear your team of, any potential academic integrity issues in your submission.

---
## Tips
Below are some suggestions on how you may improve your integrated system and live demo performance.

### General remarks
- In the testing and marking arenas for C2 and final demo, there will be 10 ArUco marker blocks and 10 objects. At the starting location (0, 0, 0) the robot will be able to see at least one marker.
- Perform SLAM and object recognition simultaneously, so that after manually driving the robot around the arena once (to save time), you will have both the estimated poses of ArUco markers and the estimated poses of objects
- Make sure you have included everything required to run your demo in the submission. If you can't run the demo from your downloaded submission we can't allow you to run from your local working directory or make changes to your codes.
- Practice the marking demo steps so that you are familiar with it. This includes downloading into an empty folder, practicing the Final Demo within this folder, renaming and numbering the slam and targets maps and zipping these maps in a single folder.
    - Further details on how you will be marked will be provided within the Final Demo page (Week11), however the setup process (e.g code download and demo runtime) will not significantly differ from prior assessments.
- Consider having a back-up driver and laptop in case the lead person running the demo has any kind of unexpected emergencies
- Ensure that your code is only referring to files within the local folder (i.e no absolute files paths)



### SLAM
- You can test your SLAM implementation with the [SLAM test case](test/)
- To calibrate the noise/covariance matrix of the pibot model, you should estimate the values based on what you observed from the tuning and testing phase. You can get a more accurate set of values by calculating the variance for each driving strategy that you use. For example, for driving straight, drive forward 1m for 10 times and record the variance and convert to tick/s. We have provided a [wheel test script](wheel_test.py) to help you tune the variances.
    ``` 
    if lv and rv == 0: # Stopped
        cov = 0
    elif lv == rv:  # Lower covariance since driving straight is consistent
        cov = 1
    else:
        cov = 2 # Higher covariance since turning is less consistent
    ```

- In [ekf.py](../Week02-04/slam/ekf.py#L129) the second expression in the process noise equation can be commented out since it may add too much noise to the model which accumulates even if the robot is idle. However, you can also add a condition to add this term only when the robot is moving or lower the noise.
    ```
    Q[0:3,0:3] = self.robot.covariance_drive(raw_drive_meas) #+ 0.01*np.eye(3)
    ```

- To test if you implemented derivative_drive and predict correctly, run slam in an empty map (without markers) and record the robot pose. If the robot pose is way off, your calculation is most likely to be wrong.
- To test if you implemented derivative_drive and predict correctly, run slam with markers and drive around. If RMSE is too high, the calculation for update is most likely to be wrong.

### Detector
- Consider making your own test cases to test your detector component without the influence of SLAM accuracy
- Improve your detector's ability to handle occlusion (e.g., an ArUco marker blocking an object)
- Improve your detector's ability to merge multiple observations of the same object vs. seeing duplicates in the obstacles

### Navigation
- During navigation, consider including opportunities for the robot to self-correct its path or reset its location in the arena to prevent errors from accumulating
- Make use of your SLAM component to continuously correct pose estimation and update the path planning
- Make use of visual information to improve the pose estimation and path planning. For example, keeping an object in the centre of the robot's view when driving towards it
