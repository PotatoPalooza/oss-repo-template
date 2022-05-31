# Lab 01 Report - Introduction to Open Source Software
## 1. Join the Discord if you haven't already 
  ![discord](https://user-images.githubusercontent.com/49171429/170727491-d9d611ce-8d28-4046-9fb4-125aab9dcc6a.PNG)
  
## 2. Reading assignments - make sure to reflect on these in your lab report 
### Two additional suggestions on how to answer questions in a helpful way:

#### Avoid linking external resources as part of your answer without any context.
Often answers to challaning technical problems require background on the topic that can be hard to summurize quickly and so linking external resources can be helpful. However, it should be assumed that eventually these links will fail eventually and so with each link there should be included a breif summary of what the link contained so a user can find that information even if the link is broken. Many times I have found answers to questions that rely heavily on linked disussions or background where the links have failed rendering the answer hard to understand and useless.

#### Summarize the source of the confusion/question in your answer. (Restate the problem)
On discussion forums many questions start in a relativly simple place but evolve into more complex questions with many sub parts. It is important when answering questions in these long public forums to specifically address the question you are answering and summerize the problem up until that point. This will ensure that your answer can be understood without the context of reading the entire discussion, making it easier for people with similar questions to find and learn from.

### Paragraph on Free Culture (8-10 sentances)
Chapter Three of Free Culture revealed the weight of copyright laws and their failure to evolve into the digital age. Because open source software and the sharing of digital media including music has been so prevalent in the time that I have grown up, a 15 million dollar lawsuit for creating a search engine that just happens to have a music files index seems absurd. The Recording Industry Association of America RIAA playing off of strict intellectual property laws, were able to bully multiple college students to the sum of $100 billion dollars in claimed damages. In the case of Jesse this lawsuit wasn't even for explicitly pirating music, setting up servers to host pirated music, or profit in any way from stolen music. This combined with the fact that it was known that pirating music in the early 2000s was extremely easy as it is today makes it obvious that these large legal teams unable to halt the distribution of their copyrighted materials sought to profit as much as possible from the inconsequential targets they could find. Asking for the net worth of the RPI student Jesse before demanding that money as settlement is outright extortion and it reveals the dark side of copyright laws. Similar to patent trolls these goliaths of industry can sit on mountains of intellectual property and weaponize them with large legal teams to penalize anyone that accidentally steps anywhere near being involved with stealing their content. With the modern music industry far more reliant on shows and merchandise for profit and less on actual album sales it begs the question of would the RIAA continue these extreme lawsuits if there was still a major profit incentive? And what can we do to prevent situations like this from ever happening again? Hopefully stories like this can remain reminders of a history we do not want to repeat and inspire thoughtful nuanced intellectual property laws in the future.

## 3. Linux
![tree](https://user-images.githubusercontent.com/49171429/170733559-3930034d-2463-41ce-9d1f-65367b93dc14.PNG)

## 4. Regex
### 7 Practive problems
```
1) [-\d\,]*[\.]?[e\d]*[^p]$
2) ([\d]{3})
3) (\w+\.?\w+)[\+]?\w*\@
4) \<(\w+)\>?
5) (.*)\.((jpg|png|gif))$
6) \s+(.*)
7) (\w*)\((\w*.\w*):(\d+)
```
Picture of solution for 7:
![upload](https://user-images.githubusercontent.com/49171429/171056427-e1800b63-a6d6-4bf6-b845-574aa1dbdb21.PNG)
### Four beginner level crosswords
![b1](https://user-images.githubusercontent.com/49171429/171066153-6b2fe8d2-77c6-4834-8ce4-67acb69571d7.PNG)
![b2](https://user-images.githubusercontent.com/49171429/171066158-4505ce88-a110-46d3-ab02-aa9776c8fb43.PNG)
![b3 pn](https://user-images.githubusercontent.com/49171429/171066160-cc4b90dd-b578-42f3-bbf2-baff2081536b.PNG)
![b4](https://user-images.githubusercontent.com/49171429/171066164-d81a814b-177c-460e-94a4-02f98561366e.PNG)

### (Optional) problem 11 in adventofcode 2015

## 5. Play with [Snap](http://snap.berkeley.edu/) or [Blockly](https://blockly-games.appspot.com/)
Maze 10 solved with
![blocku](https://user-images.githubusercontent.com/49171429/170736409-f1a64664-6723-4f09-98ed-2d9b5846cb91.PNG)

## 6. Reflection
### How I am looking for Open Source Projects
I am primarily interested in creating some open source project around research so I am using the site https://paperswithcode.com/ to do the research for the project I want to work on. Often researchers don’t have the time or resources to make the source code for their projects fully open source and I want to join the team of volunteers that bring these paper’s ideas to the masses. With more interest then ever in computer science research, especially in machine learning, I am hoping to help document and create demos for an a published ML research paper. Right now I’m looking into Neural Radiance Fields for View Synthesis NeRF https://github.com/bmild/nerf which enable the creation of novel camera perspectives on a scene from a set of images. Specifically I’m looking into the theasibility of doing a project to bring Mip-NeRF 360: Unbounded Anti-Aliased Neural Radiance Fields https://jonbarron.info/mipnerf360/ into an easy to use demo. I’m looking into what a minimum viable product for a demo of this technology would look like. My current concerns are surrounding project complexity and computational resources to execute this project however I’m hopeful I can pitch this project and find a team soon. 
