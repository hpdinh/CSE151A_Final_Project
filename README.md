## Milestone 2 <br>
We observed inconsistencies in file extensions across the images, with some using uppercase letters (e.g., "JPG" instead of "jpg") and others varying in format (png, jpeg, jpg), so we need to standardize all file extensions to lowercase. The dataset contains 400 images across four classes: Bus, Car, Motorcycle, and Truck, with unique image dimensions per class as follows: Bus – 82, Car – 71, Motorcycle – 74, and Truck – 78. For preprocessing, we will first resize all images to a consistent dimension, ensuring uniformity across the dataset. The target dimensions will be decided based on our approach, whether using a pre-trained neural network or developing a custom model. If resizing alters the desired aspect ratios, we will apply zero padding to center the resized images on a blank canvas, preserving their original proportions. Additionally, we will implement data augmentation techniques to enhance the dataset’s variability, such as rotation, flipping, and scaling, which will help improve the robustness of our model. These preprocessing and augmentation steps will ensure a well-structured, versatile dataset ready for analysis and model training.
<br>
<br>
## Milestone 3 <br>
*Note*: You may have to refresh the page if the ``milestone_3.ipynb`` notebook can't render (it'll load eventually). The notebook contains all major and finalized preprocessing, feature extraction, and our baseline model. <br>

1: **Finish Major Preprocessing & Data Augmentation**
- Scaling: Applied standardization to images into 224x224 dimensions
- Grayscaling: Applied grayscaling to already-scaled images, also used for data augmentation
- Rotating: Applied varying rotation degrees to images (from 15 to 75 degrees), also used for data augmentation
- Horizontal Flipping: Applied horizontal flipping to images, also used for data augmentation
<br>

2: **Train Our First Model** <br>
Our first model was a Multi-Class Support Vector Machine (SVM), where we performed the following:
- Feature Extraction: Turned images into embeddings using ResNet50, a pretrained CNN used for image classification.
- Baseline / First Model Settings: Linear Kernel, no specified C value (defaults to C=1), decision function shape set to OVR (One-vs-Rest for Multi-Class Classification)
- Hyperparameter Tuning: Utilized Grid Search Cross-Validation to optimize the C parameter and kernel.
<br>

3: **Evaluate initial model and compare training vs. test error**<br>
- Accuracy from Training Set: 100% accuracy
- Training Error: 1 - 1 = 0 (can view in notebook)

- Accuracy from Testing Set: 98.54% accuracy
- Testing Error: 1 - 0.9854 = 0.0146 (can view in notebook)
<br>

Based on our initial model, it seemed to do really well in training and testing. However, we decided to test different models with different hyperparameters, and plot the respective model's training and test error based on the model's complexity. This is where we utilized Grid Search Cross-Validation to optimize the C parameter and kernel, and see which models tend to underfit or overfit. (can view in notebook)<br>

4: **Answer the questions: Where does your model fit in the fitting graph? and What are the next models you are thinking of and why?** 
<br>
![image](https://github.com/user-attachments/assets/05fdfb65-82c2-4c94-940d-bcfe6d3889d3)
<br>
Our model seems to fit nicely when the model's hyperparameters are set to C=1 and kernel=linear. These hyperparameters have direct influence on the model's complexity. We especially found that models with a kernel set to RBF and a growing C value tend to overfit on the data, as it performs well with little to no error on our training data, but does worse on our testing data, meaning that these hyperparameters do a bad job generalizing to our unseen testing data.
<br>
<br>
Despite this model working really well on the given dataset, we want to try state-of-the-art, cutting-edge solutions. That is, we plan on using Convolutional Neural Networks (CNNs) for our vehicle classification use case. CNNs typically work well for image classification tasks and should theoretically improve the model’s ability to capture the different structures of features / spatial hierarchies that may be in the data. <br>

5: **Update your README.md to include your new work and updates you have all added. Make sure to upload all code and notebooks. Provide links in your README.md**
- README.md is updated (as you can see)
- New work for milestone 3 has been added to ``milestone_3.ipynb`` in this repository. It continues from milestone 2.
- Take a look at the notebook here (you might have to refresh a couple times for it to render):
  [Milestone 3 Notebook](https://github.com/SadracSantacruz/CSE151A_Final_Project/blob/Milestone3/milestone_3.ipynb)

6: **Conclusion section: What is the conclusion of your 1st model? What can be done to possibly improve it?**
<br>
Our first model, a Multi-Class Support Vector Machine (SVM), showed strong performance with 100% accuracy on the training set and 98.54% accuracy on the testing set. While the model performed well overall, the slight discrepancy between training and testing accuracy suggests marginal overfitting, where the model might be too specialized to the training data.
<br>
<br>
Given that hyperparameter tuning was already applied using Grid Search Cross-Validation to optimize the C parameter and kernel, further improvements could focus on: <br>
- Model Complexity: Even with hyperparameter tuning, SVMs might still be prone to overfitting, especially when using certain kernel types or regularization values. We can explore other architectures such as neural networks (specifically CNNs), which could better capture spatial hierarchies in the data.<br>
- Data Augmentation: Although some augmentation was applied (e.g., rotation, flipping), we could potentially expand this to include additional transformations like random cropping or color jitter. This could increase the diversity of training samples and improve generalization.<br>
- Alternative Models: As mentioned, we can test different machine learning algorithms and deep learning architectures, more notably CNNs. Leveraging different approaches could help mitigate the marginal overfitting we are getting.
<br>
<br>
The next step would be to transition to CNNs, which are typically better suited for image classification tasks and can more effectively capture complex, hierarchical features in the data, potentially leading to improved testing accuracy and model robustness.
<br>
<br>

## Milestone 4 <br>
1: **Training Second Model (found in Milestone 4 Notebook)** <br>
For our second model, we decided to implement K-Nearest Neighbors (KNN), as it differs significantly from the previous SVM model. In the Milestone 4 Notebook, you'll find that we fine-tuned the model using grid search to optimize hyperparameters. The best hyperparameters were:
- k = 3 (num. neighbors)
- distance metric: Euclidean
- weighting: distsance-based
- algorithm: auto

2: **Evaluating Model and Comparing Training vs. Test Error (also found in MS4 notebook)** <br>
We will be using the results of the fine-tuned KNN model.
- Training Accuracy: 100%
  - Training Error: 0%
  - Training error suggests the KNN model fits the training data perfectly but may indicate potential overfitting on the training set
- Testing Accuracy: 94.38%
  - Testing error = roughly 5.6%, which is slightly higher than our baseline SVM model from MS3, which was around 1%
- Performance Metrics on Test Set for KNN:
  - Precision and recall for all classes are high, and F1-scores are above 0.89.
  - It's important to note that **Class 2: Truck** had the lowest recall at roughly 84%, indicating a tendency for false negatives in this class.

3: **Where Does Our Model Fit in the Fitting Graph? What Are Some Other Models We Are Thinking Of and Why?**
<br>
![image](https://github.com/user-attachments/assets/6f1bbb09-a27f-49ad-aea4-78029e9872f6)
<br>
