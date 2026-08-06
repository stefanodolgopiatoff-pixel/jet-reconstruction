**REPOSITORY STRUCTURE**:
- main.py #python code used in google colab
- requirements.txt #librieries needed to run the project
- Dockerfile #Docker configuration to build and run the containerized environment
- README.md #project documentation

**EXECUTION**:
Open a computer terminal and use the following commands with Docker opened in background: 
1) git clone 
2) cd jet-reconstruction
3) docker build -t image_name_of_your_choice .
4) docker run --rm -v "%cd%:/app" image_name_of_your_choice

In the directory jet-reconstruction cloned from GitHub there will be after the execution also the charts obtained (accuracy/loss, confusion matrix and an example).

**PROJECT DESCRIPTION**: 
This project uses a deep learning solution for classifying images of LHC simulated proton collisions. The primary goal is to categorize these images into three distinct jet signal types: QCD, TTbar, and WJets. 
The workflow begins with downloading the 'Proton Collision 13TeV' dataset from Kaggle, followed by loading and pre-processing the images, which involves resizing them to 32x32 pixels and normalizing pixel values. Since the dataset contains almost 40 thousands images, an optimization using cache, shuffle and prefetch is needed to ensure reasonable training time. The dataset is already splitted in test and train datasets.
The project uses a Convolutional Neural Network model, designed with multiple Conv2D layers (using ReLU activation and He Normal initialization) for feature extraction, MaxPooling2D for downsampling, and Dropout layers for regularization, culminating in Dense layers for classification with a softmax activation. The model is compiled using the Adam optimizer and categorical_crossentropy loss.
Training is performed over 15 epochs, incorporating a ReduceLROnPlateau callback to dynamically adjust the learning rate, which helps in achieving better convergence on the train and test accuracy and loss (without it, the validation accuracy couldn't reach the train's one).
Then the model's performance is evaluated through visualization of training and test accuracy/loss curves, generation of a comprehensive classification report detailing precision, recall, and F1-score for each class, and a confusion matrix. 
Finally, the project includes a qualitative assessment by displaying predictions on 5 sample test images, highlighting correct and incorrect classifications.

**TRAINING PERFORMANCES**:
After training, the model achieved an overall test accuracy of around 60-65%. Looking closer at individual classes, the model performed particularly well at identifying TTbar collisions, achieving accuracy rates around 70-75%. However, it had more difficulty distinguishing between the QCD and WJets categories, where performance typically dropped to the 50-60% range.
The main classification issue comes from the visual similarity between QCD and WJets events in low-resolution images, leading the network to frequently confuse one for the other. Besides that, the training graphs show that the model learns consistently over 15 epochs, with the learning rate scheduler effectively helping stabilization during training.

**TO NOTE**: I used T4 GPU on Google Colab to optimize the training speed, with CPU the time needed increases.
