# Stop tone dectection project build guideline

In this project, the Arduino Nano 33 BLE microcontroller is required as the physical endpoint device. Additionally, the Edge Impulse platform is used for sampling and training the model.

<p align="center">
  <img width=600" alt="image" src="https://github.com/zczqy80/Deep-learning-stop-tone/assets/146266229/120a4f97-afd9-43c0-b728-ec5ea3165135">
</p

The deep learning model try to realize the detection of the frequency of cohesive wordsand the stop tone in the speech during the speech which could be diviede into:"However", "I mean", "You know" and "Stop tone"(just like Umm, Ahh, enn).

## 1. Data acquisition and dataset

After completing the account registration on the Edge Impulse platform, choose to create a new project, and then select to collect new data. By scanning the QR code with a smartphone and granting permissions, you can proceed with audio sampling.
If you have any questions about how to start an audio capture project, please refer to this page: https://docs.edgeimpulse.com/docs/tutorials/end-to-end-tutorials/audio-classification.

Please pay attention to the data collection process, make sure that the ratio of training set to test set is 80% and 20%:

<p align="center">
  <img width=400" alt="image" src="https://github.com/zczqy80/Deep-learning-stop-tone/assets/146266229/3ab6d9f1-2098-4219-a882-f9025cf43c53">
</p

After the audio sampling is completed, in order to increase the influence of noise and environmental background depth after model training, an external data set about noise can be added to participate in the training:
https://docs.edgeimpulse.com/docs/pre-built-datasets/keyword-spotting

<p align="center">
  <img width=600" alt="image" src="https://github.com/zczqy80/Deep-learning-stop-tone/assets/146266229/6fdcbd5f-c24e-4810-9ea3-d656cc83a97a">
</p

In this project, the above four kinds of audio that need to be identified were sampled and mixed with noise and environmental background audio samples. The file is now on github.

## 2. Model training

Set the window time and resolution type in impulse design, and the settings are as follows:

<p align="center">
  <img width=600" alt="image" src="https://github.com/zczqy80/Deep-learning-stop-tone/assets/146266229/0bccef5c-6c62-4ed3-8da9-aff9bf939caf">
</p

On the next page, the feature extraction of the data is completed, and then the parameters of the trained model are selected as:

<p align="center">
  <img width=600" alt="image" src="https://github.com/zczqy80/Deep-learning-stop-tone/assets/146266229/dda28c75-9a62-4e56-b47e-9b39211f2361">
</p

The details and result of the selection of parameter are explained in the readme file.

## 3. Deployment and Hardware

After the model is trained, the deployment of the model can be found in this web page:https://docs.edgeimpulse.com/docs/edge-impulse-studio/deployment. The trained model of this project has been upload.

A sample run of the model exported from the tutorial and added to the arduino library should look like this:

<p align="center">
  <img width=600" alt="image" src="https://github.com/zczqy80/Deep-learning-stop-tone/assets/146266229/efabe007-2fdb-49f6-a5ea-55d2ca5e7b9c">
</p

At this point, the training and deployment of the ai model were completed. It detects the presence of specific fillers and stop tone. But it can't count the number of times, so add a part of the code in the arduino, and an lcd display and two buttons. It realizes the statistics and zero of The Times, and the opening and closing of the detection function. the code has been upload. 

The wire connecting between arduino and other hardware is shown as follows:

<p align="center">
  <img width=800" alt="image" src="https://github.com/zczqy80/Deep-learning-stop-tone/assets/146266229/2b77d3ae-c7d6-44c5-b9d4-f4e6f2a7471e">
</p

If you are interested in how these two works or want to learn more about them, you can check out the author's other github project: https://github.com/zczqy80/Watch-dog, where they are explained in detail. In addition, the model file of the wooden outer packaging has also been uploaded.The final finished product of the project is shown in the following figure:

<p align="center">
  <img width="400" alt="image" src="https://github.com/zczqy80/Deep-learning-stop-tone/assets/146266229/ad114cb5-8ca2-42db-9659-172653d3518d">
</p>
