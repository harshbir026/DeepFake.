Deepfake Detection in Images using Signature Analysis and Robust Adversarial Handling
====================================================================================

Course Project: CS-671: Deep Learning and its Applications

Project Statement:
Deepfake Detection in Images using Signature Analysis and Robust Adversarial Handling

------------------------------------------------------------------------------------

Team Members:

Name                        | Roll No. | Email
----------------------------|----------|-----------------------------------------------
Aditya Tayal                | B23243   | b23243@students.iitmandi.ac.in
Karanpreet Singh Dhaliwal  | B23138   | b23138@students.iitmandi.ac.in
Kinshuk Chauhan             | B23142   | b23142@students.iitmandi.ac.in
Yatin Gupta                 | B23186   | b23186@students.iitmandi.ac.in
Mayur Arora                 | B23213   | b23213@students.iitmandi.ac.in
Mankirat Singh Saini        | B23270   | b23270@students.iitmandi.ac.in

Mentors:
- Ms. Parul Chaudhary
- Dr. Arnav Bhavsar

------------------------------------------------------------------------------------

Problem Statement:
------------------
Develop a deepfake detection model that can accurately classify images as real or fake 
by leveraging unique generation signatures. The goal is strong generalization across 
both known and unseen deepfake models.

------------------------------------------------------------------------------------

Motivation:
-----------
Deepfake images are becoming alarmingly realistic and difficult to detect, posing 
significant threats such as:
- Misinformation
- Identity fraud
- Erosion of public trust

Most existing methods fail to generalize across different generators — our approach 
addresses this gap.

------------------------------------------------------------------------------------

Architecture & Approach:
------------------------

We leverage pretrained vision transformer models to extract rich feature embeddings 
from images. These embeddings are then used with SVM classifiers to classify images 
as real or fake.

Feature Extractors:
- CLIP ViT-L/14
- CLIP ViT-H/14
- DINOv2

These models are used as frozen encoders, without any fine-tuning.

Feature Mapping:
z = F(x) ∈ ℝ^d  where F is the encoder, and d ∈ {768, 1024}

------------------------------------------------------------------------------------

Classification Strategy:
------------------------

We use SVM Classifiers (with RBF kernels) to classify the extracted feature vectors.

- Loss Function: Hinge Loss
- Hyperparameters: Regularization (C=1), Kernel (RBF), Gamma (γ=scalar)
- Training Optimization: Grid Search and Cross-Validation

------------------------------------------------------------------------------------

Results Summary:
----------------

Best configuration: CLIP ViT-H/14 + SVM (RBF Kernel)
Achieved average accuracy of 83.5%
Generalized well to unseen generators

Per Generator Performance:
- ProGAN:    100%
- CycleGAN:  98.2%
- StyleGAN:  93.5%
- Glide/BigGAN: 78–94%

------------------------------------------------------------------------------------

Directory Structure:
--------------------

Due to GitHub file size limits, models and reports are stored externally:

📁 DINOv2 Folder: [Drive Link](https://drive.google.com/drive/folders/1o-rxIA8mBluSk5WyvsWYKBJafrtU19mP).

📁 CLIP ViT-H14 & L14 Folders:[Drive Link](https://drive.google.com/drive/folders/1HWMmCz8TIfiMe6svDLCtQCoTkJACb50E).

📁 Additional Files / Random Experiments:[Drive Link](https://drive.google.com/drive/folders/1cei3Wf9XndkQgJdc96IiPbgrm9lZCVYT).

📂 Repo Structure (with important files):

```
CS-671_Project/
├── Clip_VIT_h14/
│   ├── scalar
│   ├── svm_rbf_clip_vit_h14_model_cuml.pkl
│   └── classification_report/
├── Clip_VIT_l14/
│   ├── scalar
│   ├── svm_rbf_clip_vit_l14_model_cuml.pkl
│   └── classification_report/
├── DINOv2/
│   ├── scalar
│   ├── svm_rbf_dinov2_model_cuml.pkl
│   └── classification_report/
└── README.md
```

------------------------------------------------------------------------------------

Improvements & Experiments:
---------------------------

Before finalizing the CLIP-ViT + RBF-SVM pipeline, we explored and compared several other methods:

1. Handcrafted Augmentations (CNNDet)  
   • Applied blur, JPEG-compression and noise.  
   • Result: High accuracy on seen generators but very poor generalization.

2. Patch-Level Forensics  
   • Focused on localized visual inconsistencies.  
   • Result: Failed when generators produced globally consistent images.

3. CLIP-Based Embeddings with Other Classifiers (Ojha et al. variant)  
   • Tried linear SVM, polynomial SVM and k-NN.  
   • Result: RBF SVM clearly outperformed.

4. SigLIP L-16 Features  
   • Slightly lower average accuracy (~80%), weaker generalization.

5. Hyperparameter Grid Search  
   • Per-model tuning using cross-validation.  
   • RBF SVM with C=1 and tuned γ worked best.

Final Takeaway:
Transformer-based vision features (especially from CLIP ViT-H/14) combined with 
RBF SVM provided the best results in terms of accuracy and generalization.

------------------------------------------------------------------------------------

Future Work:
------------

Work is currently in progress on applying **few-shot learning & adversarial training** to adapt models 
to unseen deepfake generators quickly.

📽️ Few-Shot Learning & Adversarial Training Concept PPT: [Drive Link](https://drive.google.com/file/d/1bFFZ-0i3eJBwT7fuRwZECMxyfnmg406-/view?usp=drivesdk).

📽️ Final Project Presentation PPT: [Drive Link](https://drive.google.com/file/d/1bGOYsq3QnbITUGEotX1A_Ua9PC5SCV00/view?usp=drivesdk).

Other directions include:
- Reduce embedding dimensionality for efficiency.
- Add data from newer diffusion models (e.g., DALL·E, Stable Diffusion).
- Use ensemble models for increased robustness.

------------------------------------------------------------------------------------

Contact:
--------

For any queries, contact: [Aditya Tayal](mailto:adityatayal404@gmail.com)

------------------------------------------------------------------------------------

Note:
-----
Developed as part of coursework for CS-671: Deep Learning and Its Applications at IIT Mandi.
