# Pedestrian_detection
This is a small detection project I did when I was a undergraduate student.

# Brief Introduction of what I did.
![image](https://github.com/Demoom/Pedestrian_detection/tree/master/Image/result4.png)<br>

## Data
![image](https://github.com/Demoom/Pedestrian_detection/tree/master/Image/result1.png)<br>
I get 650 pictures like this above, most of them have one pedestrian and some of them have many pedestrians. Each picture has a matching HTML file, in which is the coordinate of pedestrian's true bounding box.<br>

 ## Three Models
The first model is VGG16, as my computer is not good enough to train such network which has 117,479,232 params, I download it from internet. This VGG16 model is used to get the features of each candidate box.<br>
![image](https://github.com/Demoom/Pedestrian_detection/tree/master/Image/VGG16.png)<br>
Second model is SVM, which is used to classify candidate boxes into box-have-pedestrian and box-no-pedestrian.<br>
Third model is Linear Regression. This model is used to fix box-have-pedestrian, make box can hold entire pedestrian not a part of him or her.<br>

## Steps
I use selective search to cut one picture into many different small pictures, some contain pedestrian some not, and some of them may contain a part of pedestrian. Compare these pictures with true bounding box by using IOU(Area of Intersection/Area of Union), if pictures have IOU large than 0.5 then put them into VGG16 to get features A, if pictures have IOU less than 0.3 then put them into VGG16 to get features B. Features A and B used to train SVM. In the meanwhile, use pictures that have IOU large than 0.5 and the true bounding box to train Linear Regression.<br>

After training SVM and Linear Regression, it's ready to detect pedestrian.<br>
Using selective search to get many random small pictures of one pictrue, put these pictures into VGG16 get features of each small pictures, use SVM to classify these features. The small picture who's features classfied into box-have-pedestrian will be the result of detecting. Finally use Linear Regression to improve the detection.<br>
And here is first result.<br>
![image](https://github.com/Demoom/Pedestrian_detection/tree/master/Image/result1.png)<br>
Here is no bounding box, because the selective search get too few small pictures and no small picture is classified to have-pedestrian.<br>
Improve it by increasing the number of the results of selective search.<br>
And here is second result.<br>
![image](https://github.com/Demoom/Pedestrian_detection/tree/master/Image/result2.png)<br>
Now, it can find where human is. But only a part of pedestrian is boxed, this is because not train SVM well. I changed condition of getting features A to if IOU large than 0.3 then put them into VGG16 to get features A. Run again.<br>
Get the results.<br>
![image](https://github.com/Demoom/Pedestrian_detection/tree/master/Image/result3.png)
![image](https://github.com/Demoom/Pedestrian_detection/tree/master/Image/result4.png)<br>
OK, it can find pedestrian well.<br>
Many parts of this project can be improved, such as changing selective search to a not random method, train SVM classification with more well detected boxes....<br>
