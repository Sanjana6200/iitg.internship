# Underwater Image Enhancement Using U-Net

A deep learning based image enhancement system for improving the visual quality of degraded underwater images using a supervised U-Net architecture.

---

## 1. Project Overview

Underwater images often suffer from poor visibility, haze, color distortion, low contrast, and loss of fine details due to the absorption and scattering of light underwater.

This project investigates a learning-based approach for enhancing such images using a U-Net image-to-image model.

The model learns a mapping between a degraded underwater input image and its corresponding reference target image.

### Project Pipeline

Input Underwater Image
          ↓
     Preprocessing
          ↓
       U-Net Model
          ↓
    Enhanced Image
          ↓
   Quality Evaluation
          ↓
      Final Output

      2. Objectives

The main objectives of this project are:

Enhance the visibility of underwater images.
Improve contrast and reduce visual degradation.
Reduce underwater color distortion.
Preserve important edges and spatial details.
Compare classical enhancement methods with a deep learning approach.
Evaluate the quality of enhanced images using quantitative metrics.
Study the robustness of the trained model under different input conditions.
3. Dataset

The project uses a paired underwater image dataset containing Input, Target, and Generated images.

Image Type	Description
Input	Degraded underwater image provided to the model
Target	Reference image used for supervised learning
Generated	Existing generated image available in the dataset

The project uses the paired Input-Target data for supervised image-to-image learning.

Dataset V1

The final frozen dataset contains:

Split	Samples
Training	863
Validation	184
Testing	186
Total	1231

The train, validation, and test split is frozen throughout the experiments to ensure fair comparisons and reduce the risk of data leakage.

4. Data Preprocessing

Before training, the dataset undergoes a preprocessing pipeline.

Resizing

Images are resized to:

256 × 256 pixels
Normalization

Image pixel values are converted from:

0 – 255

to:

0 – 1

using:

normalized_pixel = pixel / 255

This provides a consistent numerical range for model training.

5. U-Net Architecture

The primary model used in this project is U-Net.

U-Net is an encoder-decoder convolutional neural network designed for image-to-image tasks.

The architecture consists of:

Encoder
Bottleneck
Decoder
Skip connections
Architecture Configuration
Stage	Channels
Input	3
Down 1	32
Down 2	64
Down 3	128
Bottleneck	256
Up 3	128
Up 2	64
Up 1	32
Output	3

The input and output contain three channels corresponding to RGB.

Encoder

The encoder extracts increasingly complex image features while gradually reducing spatial resolution.

256 × 256
    ↓
128 × 128
    ↓
64 × 64
    ↓
32 × 32
Bottleneck

The bottleneck represents the deepest feature representation of the network.

It contains high-level features extracted by the encoder before the decoder reconstructs the image.

Decoder

The decoder gradually restores the spatial resolution of the feature representation and reconstructs the enhanced image.

Skip Connections

Skip connections directly transfer feature information from the encoder to the corresponding decoder stages.

They help preserve:

Fine details
Edges
Spatial information
Object boundaries

This is particularly important for image enhancement, where excessive loss of spatial information can reduce image quality.

6. Training Process

The model is trained using supervised image-to-image learning.

Input Image
     ↓
    U-Net
     ↓
Prediction
     ↓
Compare with Target
     ↓
Calculate Loss
     ↓
Backpropagation
     ↓
Calculate Gradients
     ↓
Update Weights

The target image is not passed through the U-Net to generate the prediction.

Instead, it is used as the reference for calculating the loss.

7. Training Configuration
Parameter	Configuration
Model	U-Net
Framework	PyTorch
Loss Function	L1 Loss
Optimizer	Adam
Image Size	256 × 256
Input	RGB
Output	RGB
Dataset	Frozen Dataset V1
Learning Rate Experiments

Two learning rates were evaluated during model refinement:

0.001
0.0001

The validation performance was used to select the better configuration.

The test set was not used for model selection.

8. Classical Enhancement Methods

Classical image enhancement methods were considered as baseline approaches for comparison with the learning-based model.

CLAHE

Contrast Limited Adaptive Histogram Equalization improves local image contrast while limiting excessive contrast amplification.

Gamma Correction

Gamma correction adjusts image brightness using a nonlinear intensity transformation.

White Balance

White balance attempts to correct color distortion by adjusting the relative contribution of different color channels.

These methods provide traditional image-processing baselines against which the U-Net approach can be compared.

9. Evaluation

The enhancement results are evaluated using image-quality measures.

PSNR

Peak Signal-to-Noise Ratio measures the similarity between the enhanced image and the reference target.

In general:

Higher PSNR → Better reconstruction quality
SSIM

Structural Similarity Index Measure evaluates similarity in terms of image structure, brightness, and contrast.

In general:

Higher SSIM → Better structural similarity
Edge Preservation

Edge information is also considered to determine whether important boundaries and fine details are retained after enhancement.

10. Robustness and Ablation Study

A robustness study is used to observe how the model behaves under different image conditions, including changes in brightness and contrast.

An ablation study is also performed by comparing:

Full U-Net
     vs
U-Net without Skip Connections

The purpose of the ablation study is to investigate the contribution of skip connections to spatial-detail preservation.

The comparison is performed using the validation set.

The held-out test set is not used for this experiment.

11. Data Leakage Prevention

Data leakage occurs when information from validation or test data unintentionally influences model training or model selection.

To reduce this risk:

Dataset V1 is frozen.
Train, validation, and test assignments remain unchanged.
Validation data is used for model development and configuration selection.
Test data is reserved for final evaluation.
The final frozen model is not modified after freezing.
12. Project Structure
Underwater-Image-Enhancement/
│
├── Dataset/
│
├── Notebooks/
│
├── Results/
│
├── Models/
│
├── Final_Frozen_Model/
│   ├── final_unet_model.pth
│   ├── final_config.json
│   └── FREEZE_RECORD.json
│
├── Day20_Results/
│
└── README.md
13. Technologies Used
Technology	Purpose
Python	Programming
PyTorch	Deep Learning
NumPy	Numerical Processing
PIL	Image Processing
Matplotlib	Visualization
Google Colab	Model Development and Training
Google Drive	Dataset and Model Storage
GitHub	Version Control
14. Reproducibility

The project maintains a frozen dataset split and stores the final model configuration separately.

Important project artifacts include:

Dataset_V1_frozen_split.json
final_unet_model.pth
final_config.json
FREEZE_RECORD.json

These files help preserve the experimental configuration and trained model.

15. Key Concepts Demonstrated

This project covers several concepts in computer vision and deep learning:

Convolutional Neural Networks
Image-to-image learning
U-Net architecture
Encoder-decoder networks
Skip connections
Convolution and feature extraction
Pooling
ReLU activation
Sigmoid activation
Image normalization
L1 Loss
Backpropagation
Gradient-based optimization
Adam optimizer
Learning-rate experiments
Train-validation-test splitting
Data leakage prevention
Classical image enhancement
Robustness analysis
Ablation studies
PSNR
SSIM
16. Conclusion

This project investigates underwater image enhancement using a supervised U-Net image-to-image model.

The system uses paired degraded and reference images to learn how to generate enhanced underwater images while preserving important spatial details.

The experimental workflow includes dataset auditing, preprocessing, frozen dataset splitting, classical enhancement baselines, U-Net training, model refinement, robustness analysis, and ablation testing.

The final model and configuration are preserved separately to support reproducibility and final evaluation.

Project Information

Project: Underwater Image Enhancement Using U-Net
Domain: Computer Vision and Deep Learning
Model: U-Net
Framework: PyTorch
Platform: Google Colab
Dataset: Paired Underwater Image Dataset


This is the version I'd use for your repository. It looks like a **proper technical project README**, while still being readable instead of turning into a thesis-shaped brick.
