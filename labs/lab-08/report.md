# Lab 8: Testing and Continuous Integration

## Checkpoint 1: Getting Started
### 1. screenshot of the cmake-gui screen to your lab report
![checkone](https://user-images.githubusercontent.com/49171429/179628674-c51fec3c-6095-4def-b540-e716ee7416da.png)

## Checkpoint 2: Executing the Tests
### 2.1 Find the Nightly and Experimental sections and look at some of the submissions. How can you see what tests were run for a particular submission?

You can see what tests are run for each submission by clicking on the name of the build then clicking on the number of errors or passses in the table that appears on the next page to show every test that was ran.


### 2.2 Find a submission with errors. Can you see what the error condition was? How does this help you debug the failure?

The error condition on the two failures on the nightly-cmake-macos_arm64_xcode build were failed and timeout respectively which help with debugging since the first points towards a logical error introduced by the new build where expected output should be analyzed while the later suggests a timeout suggesting some operation took too long. These indicate good starting points to go back and fix your code along with the time elapsed for the test and the fact that the test completed and the program terminated.


### 2.3 Find a system that is close to your specific configuration in the Nightly, Nightly Expected or one of the Masters sections. How clean is the dashboard? Are there any errors that you need to be concerned with?

[[This system](https://open.cdash.org/build/8044394)] is close to mine in specs in the masters section. The dashboard is fairly clean and mimimal with only important information shown. There is one error of concern with the CompatibleInterface test failing a subsuite of boolean operations as it conflicts with a design requirement. This may be important if I was using this code's boolean objects as the output may violate their specifications.


### 2.4 Screenshot
![checktwo](https://user-images.githubusercontent.com/49171429/179632733-ff1c6eec-8186-4b52-8b52-32a0b791aaf5.png)

## Checkpoint 3: Failing/Passing a Test
### 3.1 Add a screenshot of your test submission with errors in the Experimental Dashboard or from the command window to your lab report.

![checkThree](https://user-images.githubusercontent.com/49171429/179634311-202152ab-327e-4a8d-b407-dbcb79d337f4.png)
The error can clearly be seen and the further debugging information reveals it fails a copyright text file resource check.


### 3.2 Now use what you learned to fix the error. Grab a screenshot to document the fix and the successful run.
![checkThree2](https://user-images.githubusercontent.com/49171429/179634835-bbcaf977-381c-43a9-be12-2f5b331d9355.png)

## Checkpoint 4: CI/CD


