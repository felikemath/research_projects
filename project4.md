---
layout: default
mathjax: true
---

# <center><span style="color:darkblue">Mobile Application of AI-based Handwriting Recognition</span></center>

<br/>
## Project duration
August, 2021

## Introduction
In the Stanford Pre-Collegiate Summer Institutes for Artificial Intelligence program, I learnt the fundamentals of machine learning (ML) and deep learning (DL); in the _Tinovation Club_ of my high school, I learned how to build simple websites with HTML and CSS. Combining these skills, I was able to build an interesting demonstration that is educational and fun as well. In this project, I built several DL neuron network models for handwriting digit recognition and a webpage-based mobile application of these models, and compared accuracy performance between these models.

Click [**<span style="color:blue">here</span>**](#_results) to jump to see the result.

## Objectives 
The objectives of this projects include
*   building and training 4 neuron networks for recognition of handwriting digits, from basic to more advanced. 
*   building backend service that run the trained model for prediction and communicates with frontend interface for input and output.
*   building frontend webpage-based application that takes user’s handwriting and communicate with the backend service.
*   comparing the accuracy performance of these neuron network models.

## Methods
#### 1.	The neuron network part
##### _1.1 The models_
<p>There have been many good examples and tutorials online of using neuron networks for recognition of handwriting digits. In this project, I built 4 convolutional neuron networks, named Basic, Intermediate I, Intermediate II and Advanced, respectively and relatively, to represent different architecture complexity and techniques used in these networks (Figure 1). More specifically,</p>

*   The Basic network consists of only 2 convolution layers with 5x5 kernels and ReLU activator, each followed by a MaxPooling layer for down-sampling. After the convolution blocks, the network also includes a flatten layer, two Dense layers and a SoftMax layer to generate output. 
*   The Intermediate-I network adds BatchNormalization layers after the convolution layers and the 1st Dense layer on top of the Basic network.
*   The Intermediate-II network further adds DropOut layers on top of the Intermediate I network.
*   The Advanced network made the following changes on top of the Intermediate II network.
    *   Using two 3x3 convolutions to replace one 5x5 convolution with similar receptive field <br/>
    *   Replacing the MaxPooling layer (no trainable parameters) with a convolution layer (with trainable parameters); <br/>
    *   Increasing training dataset size by using the Data Augmentation with shift and rotation. Please note that horizontal flip and vertical flip are not applicable to recognition of digit in this project because digits shouldn’t be upside-down or left-right-mirroring. <br/>

<br/>


<p align="center">
 <img src="{{ "/assets/images/project4/arch_of_4_models.png" | relative_url }}" style="border:solid; color:gray" width="800"> 
<br>Figure 1 Architectures of the 4 neuron networks built in this projection. 
</p> 


##### _1.2 The training data_
<p>[MNIST database of handwritten digits](http://http://yann.lecun.com/exdb/mnist/), one of the most widely used database, was used to train the models. The 60,000 samples (image size of 28x28) in the training set are split into 42,000 for training and 18,000 for validation through the training process.</p>


##### _1.3 Implementation of building, training and saving the models_
<p>The neuron networks and all supporting functions were implemented using Keras in the Tensorflow framework. </p>

<p>Four functions, build_basic_model(…), build_intermediate_model1(…), build_intermediate_model2(…) and build_advanced_model(…) were defined to build the 4 models, respectively</p>

<p>The main() function is responsible for loading the MNIST database, preparing the training, initializing validation and testing datasets, and invoking the training and evaluation process. After training is done, it saves the trained model with the HDF5 format (*.5h) for future use in the mobile application. In the end, it plots the accuracy of the 4 models through the training process. </p>

#### 2.	The backend web service
<p>The backend was built using the Flask package for Python, one of the most popular (and micro) web frameworks, to mimic website service. Please see the source code here on GitHub. Three functions with Flask’s route() decorator were defined in this file. The route() decorator tells Flask which URL should trigger which function based on the action in the user’s browser.</p>

<p>The index() function renders and returns the index.html homepage that we want to display in the user’s browser when the user visit this website. </p>

{% highlight python %}
@app.route('/')
def index():
{% endhighlight %}

The changemodel() function sets which one of the 4 models to use for prediction when it receives the user’s request (transmitted via the POST method of http protocol) to use a different model. 

{% highlight python %}
@app.route('/changemodel/', methods=['POST'])
def changemodel():
{% endhighlight %}

The predict() function responds to the “predict” request (transmitted using the POST method of http protocol) when the user clicks the “Recognize” button the browser. The digit picture that the user draws in the browser is also transmitted together via the POST request, but encoded in byte string format and thus cannot be used directly by the model. Therefore, it calls a help function parseImageFromInternet(imgDataStr) to decode the data string and convert to the same format that was used for model training. The predicted output from the model will be transmitted back to the user’s browser.

{% highlight python %}
@app.route('/predict/', methods=['POST'])
def predict():
{% endhighlight %}

When this Python script is executed, first it loads the four pre-trained models from the previously saved HDF5 files. Then, it launches Flask application using

{% highlight python %}
app.run(host='192.168.1.100', port=8080)
{% endhighlight %}

The host IP address above is just an example and should be changed to the actual IP address of the server running Flask.

#### 3.	The frontend part of the mobile application
The GUI design of the mobile webpage is shown in Figure 2. It consists of a dropdown menu that allows the user to choose any one of the 4 pre-trained models and send the “changemodel” request to the server. It also consists of a slider that allows the user to choose the size of the drawing brush. In the center there is a square canvas where the user can hand-write a digit on the mobile screen. The Recognize button will send the “predict” request along with the digit picture data via the POST method and receives the result to display in the text box below. The Redraw button clears the canvas.

<p align="center">
 <img src="{{ "/assets/images/project4/Mobile_app.png" | relative_url }}" style="border:solid; color:gray" width="400"> 
<br>Figure 2 GUI design of the mobile web application. 
</p> 

<p>The functionalities of such features are implemented using JavaScript, including those in the client side (such as drawing on the canvas object) and those handling communication between the server and client (such as the button click function). Please see the html file and the JavaScript file here and here in GitHub, respectively.</p>


<button class="button button1"><a href="https://github.com/felikemath/P4_AI_handwriting_recog_on_mobile">View the Project on GitHub</a></button>


## <a name="_results"></a>Results and Discussions
#### 1.	Model accuracy
Please see comparison of the accuracy vs. epochs between the 4 models in Figure 3. 

*   For all models, the accuracy increases with epoch in the early stage of training, and stabilizes after 20 epochs in this project. All 4 models achieved accuracy greater than 0.99.
*   Among the 4 models, the accuracy increases from the Basic, to Intermediate-I, then Intermediate-II, and then Advanced. This indicates that appropriate use of BatchNormalization, DropOut, Convolution vs MaxPooling for Down-sampling, and Data Augmentation can help improve accuracy in this test.

<p align="center">
 <img src="{{ "/assets/images/project4/accuracy_of_4_models.png" | relative_url }}" style="border:solid; color:gray" width="760"> 
<br>Figure 3 Acurracy of the models. 
</p> 

#### 2.	Digit recognition results from the mobile web application
The following figures show comparisons of the digit recognition results between the Basic and Advanced models. In this test, the Basic model missed two cases: misrecognized 0 to 1 and 4 to 2. However, overall, all models worked very well. 
<div>
    <div class="row">
        <div class="column">
            <img src="{{ "/assets/images/project4/basic_0.png" | relative_url }}" alt="basic_0" style="width:100%; border:solid; color:#AAAAAA">
        </div>
        <div class="column">
            <img src="{{ "/assets/images/project4/advanced_0.png" | relative_url }}" alt="advanced_0" style="width:100%; border:solid; color:#AAAAAA">
        </div>  
        <div class="column">
            <img src="{{ "/assets/images/project4/basic_1.png" | relative_url }}" alt="basic_1" style="width:100%; border:solid; color:#AAAAAA">
        </div>
        <div class="column">
            <img src="{{ "/assets/images/project4/advanced_1.png" | relative_url }}" alt="advanced_1" style="width:100%; border:solid; color:#AAAAAA">
        </div>  
    </div> 
    <div class="row">
        <div class="column">
            <img src="{{ "/assets/images/project4/basic_2.png" | relative_url }}" alt="basic_0" style="width:100%; border:solid; color:#AAAAAA">
        </div>
        <div class="column">
            <img src="{{ "/assets/images/project4/advanced_2.png" | relative_url }}" alt="advanced_0" style="width:100%; border:solid; color:#AAAAAA">
        </div>  
        <div class="column">
            <img src="{{ "/assets/images/project4/basic_3.png" | relative_url }}" alt="basic_1" style="width:100%; border:solid; color:#AAAAAA">
        </div>
        <div class="column">
            <img src="{{ "/assets/images/project4/advanced_3.png" | relative_url }}" alt="advanced_1" style="width:100%; border:solid; color:#AAAAAA">
        </div>  
    </div> 
    <div class="row">
        <div class="column">
            <img src="{{ "/assets/images/project4/basic_4.png" | relative_url }}" alt="basic_0" style="width:100%; border:solid; color:#AAAAAA">
        </div>
        <div class="column">
            <img src="{{ "/assets/images/project4/advanced_4.png" | relative_url }}" alt="advanced_0" style="width:100%; border:solid; color:#AAAAAA">
        </div>  
        <div class="column">
            <img src="{{ "/assets/images/project4/basic_5.png" | relative_url }}" alt="basic_1" style="width:100%; border:solid; color:#AAAAAA">
        </div>
        <div class="column">
            <img src="{{ "/assets/images/project4/advanced_5.png" | relative_url }}" alt="advanced_1" style="width:100%; border:solid; color:#AAAAAA">
        </div>  
    </div> 
    <div class="row">
        <div class="column">
            <img src="{{ "/assets/images/project4/basic_6.png" | relative_url }}" alt="basic_0" style="width:100%; border:solid; color:#AAAAAA">
        </div>
        <div class="column">
            <img src="{{ "/assets/images/project4/advanced_6.png" | relative_url }}" alt="advanced_0" style="width:100%; border:solid; color:#AAAAAA">
        </div>  
        <div class="column">
            <img src="{{ "/assets/images/project4/basic_7.png" | relative_url }}" alt="basic_1" style="width:100%; border:solid; color:#AAAAAA">
        </div>
        <div class="column">
            <img src="{{ "/assets/images/project4/advanced_7.png" | relative_url }}" alt="advanced_1" style="width:100%; border:solid; color:#AAAAAA">
        </div>  
    </div> 
    <div class="row">
        <div class="column">
            <img src="{{ "/assets/images/project4/basic_8.png" | relative_url }}" alt="basic_0" style="width:100%; border:solid; color:#AAAAAA">
        </div>
        <div class="column">
            <img src="{{ "/assets/images/project4/advanced_8.png" | relative_url }}" alt="advanced_0" style="width:100%; border:solid; color:#AAAAAA">
        </div>  
        <div class="column">
            <img src="{{ "/assets/images/project4/basic_9.png" | relative_url }}" alt="basic_1" style="width:100%; border:solid; color:#AAAAAA">
        </div>
        <div class="column">
            <img src="{{ "/assets/images/project4/advanced_9.png" | relative_url }}" alt="advanced_1" style="width:100%; border:solid; color:#AAAAAA">
        </div>  
    </div> 
</div>

<br/>

## Summary
In this project, I developed a complete mobile application of an AI-based handwriting digit recognition, including building 4 models of different complexities, training and saving the models, building the backend micro-web-server, and writing the frontend mobile application. Evaluation of these models demonstrated how the modules and techniques (such as BatchNormalization, DropOut, Convolution, Data Augmentation) play roles in neuron networks.

<br/>


