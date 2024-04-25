# DL4SN Stop tone dectection

Yuhang Lei, 

link to github: https://github.com/zczqy80/Deep-learning-stop-tone

link to Edge Impulse: https://studio.edgeimpulse.com/studio/363567

## Introduction
In this project, based on the audio detection and the external physical enclosure containing the display screen and interactive buttons, the deep learning model realized the detection of the frequency of cohesive words and the stop tone in the speech during the speech.The detection output include pause tone detection and three common filler words. The overall appearance of the project is shown in the figure below：

<p align="center">
  <img width="450" alt="image" src="https://github.com/zczqy80/Deep-learning-stop-tone/assets/146266229/ad114cb5-8ca2-42db-9659-172653d3518d">
</p>

In the figure above, "how" represents "however," "know" stands for "you know," "Mean" corresponds to "I mean," and "Stop" denotes a stop tone. The inspiration for this project came from a discussion with the professor, where it was identified that during speeches, some speakers may exhibit extended pauses or frequently use certain filler words, resulting in a lack of fluency. Therefore, based on the audio training recognition deep learning models mentioned in lectures 6 (Wilson, 2024), an Arduino Nano 33 BLE microcontroller was used for audio sampling and recognition. The data was manual sampled and recognized on the Edge Impulse platform, where the model training and deployment were also completed.

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
As timeseries data, audio is often effectively processed by Recurrent Neural Networks (RNN) due to their capability for sequence learning and inherent memory. However, the model chosen for this project is a one-dimensional Convolutional Neural Network (1D-CNN). This decision was based on the nature of the audio being processed—four short-duration sounds with no logical or temporal interdependencies, which do not play to the strengths of RNNs. RNNs excel in applications where predictions rely on historical data continuity, possessing short-term memory to handle such tasks (Sak, Senior and Beaufays, 2014).

In contrast, although the traditional CNN models are generally preferred for image processing, under one-dimensional conditions, the convolutional kernel of 1D-CNN model moves along the time axis, making it well-suited for tasks like audio processing. Moreover, the recognition in this project primarily depends on the inherent characteristics of the data rather than sequential relationships. Compared to RNN models, a 1D-CNN has fewer parameters and offers a quicker response time (Li et al., 2019). Therefore, this project utilized the default 1D-CNN model provided by Edge Impulse.

In the process of model training, it can be found that with the gradual increase of sample types, the accuracy of the model is gradually decreasing, and the loss is gradually increasing. However, this trend is not obvious and still within an acceptable range，which has been shown as follows:

<p align="center">
  <img width=750" alt="image" src="https://github.com/zczqy80/Deep-learning-stop-tone/assets/146266229/babee73c-0fe8-457b-b1b0-ba3aee36e0f4">
</p>

It is also worth to point out that, in order to exclude the influence of environmental noise and background sound (Edge Impulse, 2024), this project refers to a part of the dataset in the teaching project provided by edge impulse to add the function of identifying noise and unknown to the model.

## Experiments

In order to explore how to achieve better training effects, two training parameters were modified during the training process to obtain comparative results. The first modification was the change in the number of neurons in the convolutional layers, with variations of 4, 8, and 16 neurons. The results are shown in the table below：

<p align="center">
  <img width=750" alt="image" src="https://github.com/zczqy80/Deep-learning-stop-tone/assets/146266229/cdce33b5-a0b4-4e28-ac9f-caecbbf71e16">
</p>

In this table, the vertical comparison unique optimal value is highlighted in green, and the unique worst value is highlighted in red. After comparison, it is evident that under the condition of having 4 neurons, the model achieves the fastest response time; however, the accuracy is significantly lower compared to the other two configurations. As the number of neurons increases, there is a gradual improvement in model accuracy, but at the cost of slower response times. After weighing the pros and cons, this project ultimately chose to use 8 neurons as the parameter. Compared to the maximum of 16 neurons, there is not much decline in the model's accuracy, but the response speed has been substantially improved.

The second parameter that was changed was Dropout during training. The table of record results is shown below:

<p align="center">
  <img width=750" alt="image" src="https://github.com/zczqy80/Deep-learning-stop-tone/assets/146266229/6976658d-c0ff-4654-8aa1-cf23629440cd">
</p>

From the above table, it can be seen that although there are differences among the three configurations, the majority of the numerical gaps are minimal, with the exception of the classification for "you know." It is evident that at a dropout rate of 0.25, the prediction accuracy for this category is over 10% higher than the other two models. Therefore, the dropout parameter was ultimately set to 0.25. The final parameter of this project model was 8 neurons and 0.25 dropout, the model behaves as follows:

<p align="center">
  <img width=500" alt="image" src="https://github.com/zczqy80/Deep-learning-stop-tone/assets/146266229/34b24f26-a392-4e00-8cf2-4ecce88966e7">
</p

The model is deployed on the Arduino Nano 33 BLE microcomputer and tested in Real world.

## Results and Observations

After the model is deployed, the data sent back to the port is displayed in the following format：

<p align="center">
  <img width=500" alt="image" src="https://github.com/zczqy80/Deep-learning-stop-tone/assets/146266229/efabe007-2fdb-49f6-a5ea-55d2ca5e7b9c">
</p

The output of the model is correct as "noise" or "unknown" in noisy environments or when no specific vocabulary is detected. On this basis, the author and other students have carried out the filler words: "However","You know" & "I mean" and stop tone recognition tests on the model, and the results are shown as follows:

<p align="center">
  <img width=750" alt="image" src="https://github.com/zczqy80/Deep-learning-stop-tone/assets/146266229/d62c6f87-546c-4273-9911-baf19bea5d07">
</p

The results from the table clearly demonstrate that the final recognition outcomes are heavily influenced by the acquisition strategies employed. In the case of the "Stop tone", which was collected from a wide range of samples, even students who did not participate in the training sample acquisition could be clearly identified. However, for "you know," where the training samples were polluted, the recognition rate was suboptimal under all condition. As for "I mean," which was solely sourced from the author, identification was only successful when the author deliberately replicated the intonation used during the training. Other volunteers were entirely unable to be recognized for "I mean." With "However," which had a variety of intonations but a single source, the author's samples could be easily identified, whereas other students had to mimic the author's intonation to be potentially recognized.

The testing results are in line with the measures taken during the initial sampling, which confirms that it is crucial to avoid contamination of data during the sampling process and to collect a variety of sound sources to expand the breadth of recognition.

Additionally, in the process of adjusting the model parameters, the author made the following conjecture: as the number of neurons increases, accuracy would gradually improve, but the trade-off would be slower response times. When selecting parameters, a balance should be found between the two. The dropout value might not have a significant relationship with the accuracy of normal data and the speed of the response. However, in cases where the data is polluted, an appropriate dropout value could mitigate the negative impact on accuracy.

## Bibliography
1. Edge Impulse, (2024). Keyword Spotting in Pre-built Datasets. [online] Available at: https://docs.edgeimpulse.com/docs/pre-built-datasets/keyword-spotting [Accessed 16 April 2024].

2. Li, Y., Baidoo, C., Cai, T. and Kusi, G.A., (2019). Speech Emotion Recognition Using 1D CNN with No Attention. 2019 23rd International Computer Science and Engineering Conference (ICSEC), Phuket, Thailand, pp. 351-356. [online] Available at: https://doi.org/10.1109/ICSEC47112.2019.8974716. (Accessed: 22 April 2024)

3. Sak, H., Senior, A.W. and Beaufays, F. (2014). Long short-term memory recurrent neural network architectures for large scale acoustic modeling. Proceedings of the 15th Annual Conference of the International Speech Communication Association (Interspeech 2014), [online] Available at: https://www.isca-archive.org/interspeech_2014/sak14_interspeech.pdf [Accessed 22 April 2024].

4. Wilson, D. (2024) 'DL4SN Week 6 Lecture slides: RPi CV + Edge Impulse + Brief', CASA0018: Deep Learning for Sensor Networks 23/24. University College London. [online] Available at: https://moodle.ucl.ac.uk/mod/resource/view.php?id=5418360 (Accessed: 22 April 2024)



## Declaration of Authorship

I, YUHANG LEI, confirm that the work presented in this assessment is my own. Where information has been derived from other sources, I confirm that this has been indicated in the work.


Yuhang lei

25/04/2024

Word count: 1636 (main text)
