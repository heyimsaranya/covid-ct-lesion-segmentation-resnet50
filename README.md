Project Overview

This project presents an automated deep learning framework for COVID-19 lung lesion segmentation from volumetric chest CT scans. The model is built using DeepLabV3 with a ResNet50 backbone and adapted for single-channel CT input. The objective is to accurately segment infection regions to enable quantitative disease assessment and support AI-assisted radiological analysis.

Dataset

Source: Radiopaedia COVID-19 Lung CT Segmentation Dataset https://medicalsegmentation.com/covid19/
Format: NIfTI (.nii) volumetric CT scans

Dataset Details:
9 volumetric CT scans
Total slices: 829
Each scan includes lung masks and infection (lesion) masks.

Preprocessing
Extracted 2D axial slices from 3D CT volumes.
Resized all slices to 256 × 256 pixels.
CT images: Bilinear interpolation
Masks: Nearest-neighbor interpolation
Applied min–max normalization per slice to scale intensities to [0,1].
Converted lesion masks to binary format (0 = background, 1 = lesion).
Saved processed data as NumPy arrays: images.npy, lung_masks.npy, lesion_masks.npy.

Data Splitting
The dataset was split slice-wise as follows:
Training: 70%
Validation: 15%
Test: 15%

Data Augmentation
To improve model generalization:
Horizontal flip
Random 90° rotation
Normalization (mean = 0.0, std = 1.0)


Model Architecture
Base model: DeepLabV3 with ResNet50 backbone (torchvision implementation).
Modifications:
First convolution layer adapted for single-channel CT input.
Backbone initialized using pretrained weights from a custom SimpleModel.
Number of output classes: 2 (background, lesion).

Training Configuration
Loss Function: CrossEntropyLoss
Optimizer: Adam
Epochs: 20
Batch Size: 4

Training Performance:
Training loss reduced from 0.2011 to 0.0076
Validation loss reduced from 0.0763 to 0.0067
Model saved as: deeplabv3_resnet50_trained.pth

Evaluation
Test Set Results:
Average Test Loss: 0.0086
Dice Score: 0.8773
IoU Score: 0.8215

Validation Set Performance:
Accuracy: 0.9979
Precision: 0.8419
Recall (Sensitivity): 0.8329
Specificity: 0.9990
F1-score: 0.8374
AUC-ROC: 0.9981

Visualization
The project includes visualization of CT slices, ground truth masks, and predicted masks, along with per-image Dice and IoU calculations.

Conclusion
This project demonstrates that DeepLabV3 with a ResNet50 backbone can effectively segment COVID-19 lung lesions from CT scans with high accuracy and strong generalization performance. The achieved Dice score of 0.8773 and IoU of 0.8215 indicate reliable lesion segmentation capability. This framework provides a foundation for automated quantitative assessment of pulmonary infections and future extensions toward multi-class and 3D volumetric segmentation models.
