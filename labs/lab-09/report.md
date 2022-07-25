# Lab 9: Virtualization and Docker
## Example 0
After installing docker and running it on the sample container with the command `docker run docker/whalesay cowsay boo` I get the following result:

![checkone](https://user-images.githubusercontent.com/49171429/180876295-e17301fe-93a9-4ef3-903b-b62b5fa0bb6d.png)

A scary whale!


## Example 1
After installing and running the ubuntu instance I installed vim and used it to write hello in a file called `test.txt` seen here:

![check1 1](https://user-images.githubusercontent.com/49171429/180878116-ea12e6d3-1e1d-445f-80af-5f2119441533.png)

Then I installed cowsay and run it with the input "moo!" here:

![check1 2](https://user-images.githubusercontent.com/49171429/180878130-d6c3220d-5046-412e-a310-8036b028cb2d.png)

## Example 2
After running the mongodb server and the rocketchat app I get this result at `localhost:3000`

![check2](https://user-images.githubusercontent.com/49171429/180886383-19b084fd-4713-48d2-9c6a-4588b1f6c8b3.PNG)

## Example 3
After creating, building, and running the demo server I get the following result on `localhost:5000`

![ex3](https://user-images.githubusercontent.com/49171429/180887592-53d56b36-6e2e-4c0b-a324-77ce0e2ba469.PNG)

## Example 4
Running the docker file alone does not work as the mongoDB server is missing however after creating the `docker-compose.yml` and adding a dockerignore I was able to run the application using `docker-compose build` and `docker-compose up`. The following terminal and browser outputs were then generated:

Running the application
![ex4](https://user-images.githubusercontent.com/49171429/180893799-7d4f7608-ad5f-4a6f-ad84-0a62fd8b8485.PNG)

Terminal
![ex4 1](https://user-images.githubusercontent.com/49171429/180893808-7dc3786f-75b4-4718-9836-6b75e3b9741c.PNG)


