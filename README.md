# Codeblooded
This project implements a semantic segmentation model for off-road desert environments using the dataset provided by Duality AI. The goal is to train a deep learning model that classifies each pixel in an image into terrain or object categories.
This task is important for autonomous navigation systems, where vehicles must understand terrain features such as rocks, bushes, logs, and ground surfaces.

Project Overview
The model was trained on a synthetic desert dataset generated using Duality AI's Falcon digital twin platform. The dataset contains RGB images and segmentation masks that label each pixel with a terrain category.

The trained model learns to:
Identify obstacles
Recognize terrain types
Segment scenes into semantic categories
Generalize to unseen desert environments

Dataset Classes
Class ID	Class Name
100	      Trees
200	      Lush Bushes
300	      Dry Grass
500	      Dry Bushes
550	      Ground Clutter
600	      Flowers
700	      Logs
800	      Rocks
7100	    Landscape
10000	    Sky

Model Architecture
Model Used: DeepLabV3+ with ResNet101 Backbone
Reasons for selection: High accuracy in semantic segmentation tasks 
                       Strong feature extraction
                       Good performance on outdoor scenes
                       Efficient inference

Dataset Verification
Before training, several checks were performed to ensure dataset integrity.
Dataset Count Check
Train images: 2857
Train masks: 2857
Validation images: 317
Validation masks: 317
This confirms that every image has a corresponding segmentation mask.

Dataset Verification Output
The verification confirms: No missing masks
                           No unreadable masks
Dataset ready for training

Image and Mask Structure
Each image has a corresponding segmentation mask.
Image shape:
(540, 960, 3)
Mask shape:
(540, 960, 3)
This confirms correct alignment between RGB images and segmentation masks.

Dataset Loading Validation
Batch loading test was performed to confirm proper dataset loading.
Validation results:
No broken files
Dataset loads correctly
Batch shapes verified

Image batch shape:
torch.Size([4, 3, 540, 960])
Mask batch shape:
torch.Size([4, 540, 960])
This confirms the dataset is ready for model training.

Project Structure
project/
│
├── train.py
├── test.py
├── dataset/
│   ├── train/
│   │   ├── Color_Images/
│   │   └── Segmentation/
│   │
│   ├── val/
│   │   ├── Color_Images/
│   │   └── Segmentation/
│
├── testImages/
│
├── models/
│   └── offroad_segmentation_model.pth
│
├── runs/
│   ├── training_logs
│   ├── predictions
│   └── loss_graphs
│
└── README.md
Environment Requirements

HardwareRecommended:
NVIDIA GPU
Minimum 8GB VRAM
16GB RAM
Training was performed using:
Google Colab GPU environment

Software Requirements
Python Version: Python 3.9+
Dependency Installation

Install dependencies using pip:
pip install torch torchvision
pip install numpy
pip install pandas
pip install matplotlib
pip install scikit-learn
pip install tqdm
pip install opencv-python
pip install pillow
pip install segmentation-models-pytorch

Alternatively:

pip install -r requirements.txt
Dataset Setup

Download the dataset from the Duality AI Falcon platform.
Place it in the following structure:
dataset/
   train/Color_Images
   train/Segmentation

   val/Color_Images
   val/Segmentation

Test images should be placed inside:

testImages/

Test images were not used during training.

Training the Model
To train the segmentation model run:
python train.py

The training pipeline performs:
Dataset loading
Data preprocessing
Model initialization
Forward pass
Loss computation
Backpropagation
Validation evaluation

Model checkpoint saving

The trained model will be saved as:
models/offroad_segmentation_model.pth

Testing the Model
To evaluate the trained model on unseen images run:
python test.py

Runs inference on test images
Generates segmentation predictions
Calculates evaluation metrics
Reproducing Final Results

To reproduce the results:

Step 1 – Install dependencies
pip install -r requirements.txt
Step 2 – Download dataset

Place dataset in project directory.

Step 3 – Train model
python train.py
Step 4 – Run evaluation
python test.py
Evaluation Metric

The model is evaluated using Intersection over Union (IoU).
IoU measures the overlap between predicted segmentation and ground truth.
IoU = Intersection / Union

Interpretation:

IoU Score	Performance
<0.3	Poor
0.3 – 0.5	Moderate
0.5 – 0.7	Good
>0.7	Excellent

output IoU - 0.86


After training and testing, the following outputs are generated.
Model Weights
models/offroad_segmentation_model.pth

Training Logs
Stored in:
runs/training_logs/

Includes:
training loss
validation loss
epoch statistics
Segmentation Predictions
Stored in:
runs/predictions/
Each output image is a predicted segmentation mask.
Interpretation of Segmentation Results
Each pixel in the predicted mask corresponds to a terrain category.
Green → vegetation
Brown → ground/landscape
Gray → rocks
Blue → sky
Dark regions → logs or bushes

These segmentation maps allow autonomous systems to understand terrain structure.

Challenges Encountered
Class imbalance
Some classes such as flowers and logs appear less frequently in the dataset.
Visual similarity
Some classes have similar textures:
dry grass vs dry bushes
rocks vs ground clutter
This can lead to occasional misclassification.

*Possible Improvements
Future work may include:
Data augmentation
Class balanced loss
Training with larger datasets
Transformer-based segmentation models (SegFormer)
Domain adaptation for real-world terrain*
