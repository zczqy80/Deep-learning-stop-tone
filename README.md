# DL4SN Stop tone dectection

Yuhang Lei, 

link to github: https://github.com/zczqy80/Deep-learning-stop-tone

link to Edge Impulse: https://studio.edgeimpulse.com/studio/363567

## Introduction
In this project, based on the audio detection and the external physical enclosure containing the display screen and interactive buttons, the deep learning model realized the detection of the frequency of cohesive words and the stop tone in the speech during the speech.The detection output include pause tone detection and three common filler words. The overall appearance of the project is shown in the figure below：

<p align="center">
  <img width="450" alt="image" src="https://github.com/zczqy80/Deep-learning-stop-tone/assets/146266229/ad114cb5-8ca2-42db-9659-172653d3518d">
</p>

In the figure above, "how" represents "however," "know" stands for "you know," "Mean" corresponds to "I mean," and "Stop" denotes a stop tone. The inspiration for this project came from a discussion with the professor, where it was identified that during speeches, some speakers may exhibit extended pauses or frequently use certain filler words, resulting in a lack of fluency. Therefore, based on the audio training recognition deep learning models mentioned in lectures 6 and 7, an Arduino Nano 33 BLE microcontroller was used for audio sampling and recognition. The data was manual sampled and recognized on the Edge Impulse platform, where the model training and deployment were also completed.

## Research Question
This project aims to assess the fluency of speeches or talks by detecting the frequency of stop tones and filler words in the speech, which can also be used to improve personal speaking habits.

## Application Overview
This project follows a workflow similar to most deep learning projects and can be divided into three block, which has been shown as follows in the order of step:

<p align="center">
  <img width=800" alt="image" src="https://github.com/zczqy80/Deep-learning-stop-tone/assets/146266229/1f396f8d-e43d-4e57-8d68-09445b980931">
</p>

1. Acquisition and classification of data: This project needs to sample and label the audio required for classification, and store it in the dataset.
2. Model training and adjustment parameters: Most of the data in the dataset will be used to train the model, while the rest will be used to validate the model. In this process, the training parameters of the model will be constantly adjusted to get the best training results.
3. Hardware deployment and testing: The model trained on edge impulse will be deployed to the microcontroller, and the microcontroller's microphone will be used for audio sampling and recognition, and then combined with different usage scenarios and codes to output the results. The details of this process are as follows:

<p align="center">
  <img width=800" alt="image" src="https://github.com/zczqy80/Deep-learning-stop-tone/assets/146266229/1a0275ff-9644-45e1-a337-3e16a94b6397">
</p>

During deployment, screens were added to the hardware to visualize the recognition results and count. Two external buttons have also been added, allowing the user to pause the detection at any time or return the count to zero. This is for the convenience of the user, to switch target recount in different conversations, or to pause detection. The design makes the application easy to use.

## Data
This project is designed to classify and detect three common filler words: "however," "I mean," "you know," as well as stop tone like "umm," "ahh," and "en," amounting to a total of four classes to be recognized. For each label, 125 audio samples were collected, with 100 used for the training set and 25 for the test set. Additionally, to verify the impact of different sampling methods on the detection results, different acquisition strategy were used for all four labels.

Stop tone

The acquisition of "stop tone" is carried out in the whole class, which includes various types of stop tones from multiple students. Its feature extraction distribution is relatively wide, as shown in the figure below:

<p align="center">
  <img width=500" alt="image" src="https://github.com/zczqy80/Deep-learning-stop-tone/assets/146266229/050eff27-d49b-4320-bb44-698dde21c615">
</p>

You know

For the audio dataset for "you know", similar to "stop tone", is also collected across the class. However, in order to verify the influence of bad samples on the recognition results, background noise is mixed in the acquisition process or the tone is deliberately strange. The distribution of its characteristics is relatively concentrated, but the mixed bad samples appear more prominent:

<p align="center">
  <img width=500" alt="image" src="https://github.com/zczqy80/Deep-learning-stop-tone/assets/146266229/278f02db-33bc-4fe4-8bda-819f0aa125ce">
</p>

I mean

Unlike the previous two, the audio for "I mean" comes solely from the author. Additionally, the intonation and voice were kept consistent throughout the sampling process. As a result, the feature distribution under this label is extremely concentrated:

<p align="center">
  <img width=500" alt="image" src="https://github.com/zczqy80/Deep-learning-stop-tone/assets/146266229/363c9d1d-4f15-464c-aedf-ce19d63027f6">
</p>

However

The sampling of "However" is also done by the author alone, but in the sampling process, the author uses a variety of different mood and intonation, and the result is that the feature distribution of the label is differentiated:

<p align="center">
  <img width=500" alt="image" src="https://github.com/zczqy80/Deep-learning-stop-tone/assets/146266229/9aabe917-a79c-4dc3-9cb3-cfb84649aa58">
</p>

After comparison, it is found that the features of the four label audio are significantly different, so it is speculated that high accuracy training results can be obtained:

<p align="center">
  <img width=750" alt="image" src="https://github.com/zczqy80/Deep-learning-stop-tone/assets/146266229/dc2d71c2-1f23-4067-b790-34cf860d88d5">
</p>

## Model
This is a Deep Learning project! What model architecture did you use? Did you try different ones? Why did you choose the ones you did?

*Tip: probably ~200 words and a diagram is usually good to describe your model!*

## Experiments
What experiments did you run to test your project? What parameters did you change? How did you measure performance? Did you write any scripts to evaluate performance? Did you use any tools to evaluate performance? Do you have graphs of results? 

*Tip: probably ~300 words and graphs and tables are usually good to convey your results!*

## Results and Observations
Synthesis the main results and observations you made from building the project. Did it work perfectly? Why not? What worked and what didn't? Why? What would you do next if you had more time?  

*Tip: probably ~300 words and remember images and diagrams bring results to life!*

## Bibliography
*If you added any references then add them in here using this format:*

1. Last name, First initial. (Year published). Title. Edition. (Only include the edition if it is not the first edition) City published: Publisher, Page(s). http://google.com

2. Last name, First initial. (Year published). Title. Edition. (Only include the edition if it is not the first edition) City published: Publisher, Page(s). http://google.com

*Tip: we use [https://www.citethisforme.com](https://www.citethisforme.com) to make this task even easier.* 

----

## Declaration of Authorship

I, AUTHORS NAME HERE, confirm that the work presented in this assessment is my own. Where information has been derived from other sources, I confirm that this has been indicated in the work.


*Digitally Sign by typing your name here*

ASSESSMENT DATE

Word count: 
