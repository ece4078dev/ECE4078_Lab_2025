# SLAM Unit Test
Credit Tin Tran

## Usage
* This unit test is used to evaluate your `robot.py` and `EKF.py`. You might find this useful for the initial setup of M1.
* Successfully passing the unit test will give you a good indication that you have implemented the SLAM correctly, that is asked of you. This is only testing for vanilla SLAM (ie. no additional modifications)
* Otherwise, the test report will report which part you of your SLAM might be, **but not necessarily**, incorrect.
* **NOTE:** These unit tests are only accurate if you only implemented the functionality you have been asked to fill, in the template. If you have implemented additional checks, functionality, etc. to finetune and improve your SLAM performance, it is likely the test results suggest you did not implement SLAM correctly even though it may be "correct"

## Preparation
1. Copy from your `Week02-04` folder into this folder, `SLAM_unit_test`, the following files and folders:
    * `calibration`
    * `util`
    * `pics`

2. Replace the following [TODOs] in the skeleton codes with your own implementations:
    * In [operate.py](./operate.py), [line 200](./operate.py#L200) to [line 213](./operate.py#L213).
    * In [robot.py](./slam/robot.py), [line 79](./slam/robot.py#L79) and [line 127](./slam/robot.py#L127)
    * In [ekf.py](./slam/ekf.py), [line 93](./slam/ekf.py#L93) and [line 117](./slam/ekf.py#L117)

    [NOTE] It is important that you keep everything else in the skeleton codes the same!

3. Replace your baseline and scale with the provided [baseline.txt](./baseline.txt) and [scale.txt](./scale.txt).

4. Activate your virtual environment.

5. Install package `pytest` using
```
python -m pip install pytest
```
## Run test
From this folder, `SLAM_unit_test`, run the following command

```
pytest test -r s
```

If you want a succinct output, run
```
pytest --tb=line test -r s
```
Have a look at your outputs to check if your SLAM is correct, or what function you need to look into. Your results should look something like this.

![Example test results](./media/Example_results.png)
