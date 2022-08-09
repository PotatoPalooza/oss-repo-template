# Lab 11: Tensorflow

## Checkpoint 1: Verify Your TensorFlow

After installing the docker image and running the code I get the following figure. Note this figure had to be saved to a file to view due to no GUI within the container.

![checkpointone](https://user-images.githubusercontent.com/49171429/183103975-47e89082-fa9e-4a1d-95e4-39addb887fbb.png)

## Checkpoint 2: Run a TensorFlow classification
The output of running the model for the 15 images from 9000-9014 is:
![final](https://user-images.githubusercontent.com/49171429/183111611-3c61d2f0-d413-40f3-b1f8-f5491135255f.png)


## Checkpoint 3: Curate some data
Here are the following four examples I decided to pass through the my model.
Original:

![ashoulder_bag](https://user-images.githubusercontent.com/49171429/183118770-e3aaaebf-747e-453b-97df-4da46813e428.png)

Downsized:

![out_ashoulder_bag](https://user-images.githubusercontent.com/49171429/183119036-3eafe43d-32a7-45e3-a9cf-0b5f88418b51.png)

Classification:

```
[0.06879142 0.00369584 0.09380084 0.04549885 0.02254954 0.12847194
 0.07633305 0.0661352  0.4929482  0.0017752 ] 8          Class: Bag
 ```

Original:

![blue_shirt](https://user-images.githubusercontent.com/49171429/183118829-c4598efa-9d43-43f1-aadb-1cbffb5a6dd6.png)

Downsized:

![out_blue_shirt](https://user-images.githubusercontent.com/49171429/183119049-8a9d8406-054d-4d40-a6a5-2a51b06126b0.png)

Classification:

```
[9.9025410e-01 1.7775224e-06 7.0537993e-07 1.4465537e-06 9.7336569e-11
 3.8550687e-11 9.7419759e-03 1.0183596e-18 3.0113648e-10 7.2549871e-13] 0        Class: T-shirt/top
 ```
Original:

![prada](https://user-images.githubusercontent.com/49171429/183118855-29317b11-5d3c-4180-9ead-d0fffc145d13.png)

Downsized: 

![out_prada](https://user-images.githubusercontent.com/49171429/183119058-f7ce6b1b-9708-49bd-bde0-e8896e383b20.png)

Classification:

```
[0.02046585 0.00271327 0.00172926 0.08506423 0.00699847 0.01531549
 0.00659363 0.5077198  0.35179064 0.00160933] 7          Class: Sneaker
 ```
Original:

![running_shoes](https://user-images.githubusercontent.com/49171429/183118864-e33d3501-e2e1-4207-bacd-63e0fce567b8.png)

Downsized:

![out_running_shoes](https://user-images.githubusercontent.com/49171429/183119071-286e6810-4cb0-40f0-a7bf-65a975b1cf64.png)

Classification:
```
[3.6196147e-06 3.7598608e-10 8.4186701e-07 1.0642475e-07 1.2848091e-05
 9.9947029e-01 6.8332042e-07 4.5446324e-04 5.6543089e-05 6.1116140e-07] 5        Class: Sandal
```

Combined results Plotted:

![CheckpointThree](https://user-images.githubusercontent.com/49171429/183118998-220e2d45-f56c-4901-bb3f-cc4a7948f367.png)

Overall:
Overall the model seems to perform well when the input closely matches the training data. In the prada bag and shoes example the images are slightly further back and at different angles then the model has seen and thus the predictions are not correct. I chose these examples to demonstrate when the model works well and when it fails althouh even in the failure cases the correct class is similar visually or a runner up class such as bag being the second prediction for the prada bag example.

### Blog and project progress have been updated in my wiki.
