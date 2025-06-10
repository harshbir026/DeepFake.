Deepfake Detection in Images using Signature Analysis and Robust Adversarial Handling
====================================================================================

Course Project — CS-671: Deep Learning and its Applications
Indian Institute of Technology (IIT) Mandi

Project Statement 25 (PS 25):
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
Improvements & Experiments:
---------------------------

Before finalizing the CLIP-ViT + RBF-SVM pipeline, we explored and compared several other methods:

1. **Handcrafted Augmentations (CNNDet)**  
   • Applied blur, JPEG-compression and noise augmentations.  
   • Result: High accuracy on seen generators but very poor generalization to unseen models.

2. **Patch-Level Forensics**  
   • Focused on localized inconsistencies in small image patches.  
   • Result: Good at detecting superficial artifacts but failed when generators produced globally consistent images.

3. **CLIP-Based Embeddings with Other Classifiers (Ojha et al. variant)**  
   • Tried CLIP ViT-L/14 embeddings with linear SVM, polynomial SVM and k-NN.  
   • Result: Linear SVM was too simplistic, polynomial SVM improved margins but still trailed the RBF kernel; k-NN suffered from high variability.

4. **SigLIP L-16 Features**  
   • Tested embeddings from SigLIP L-16 as an alternative frozen encoder.  
   • Result: Slightly lower average accuracy (~80%) and less robust on unseen diffusion models.

5. **Hyperparameter Grid Search**  
   • For each model + classifier pair, ran cross-validation grid search over C, γ (for RBF), and degree/coef0 (for polynomial).  
   • Observed that RBF SVM with C=1 and γ tuned per-model consistently outperformed others.

**Final Takeaway:**  
Transformer-based vision embeddings (especially CLIP ViT-H/14) combined with an RBF SVM provided the **best balance** of per-generator accuracy and strong generalization to completely unseen deepfake methods.

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

Key Takeaways:
--------------

- Vision Transformer embeddings capture deepfake generation patterns effectively.
- Combining frozen features with SVM classifiers provides strong generalization.
- Transformer + RBF SVM is a powerful combo for image authenticity detection.

------------------------------------------------------------------------------------

Future Work:
------------

- Reduce embedding dimensions for performance
- Extend to diffusion-based models (e.g. Stable Diffusion, DALL·E)
- Explore few-shot learning for fast adaptation
- Add adversarial training for evasion resistance
- Ensemble multiple encoders for higher robustness

------------------------------------------------------------------------------------

Contact:
--------

For any queries, contact:
Aditya Tayal — b23243@students.iitmandi.ac.in

------------------------------------------------------------------------------------

Note:
-----

Developed as part of coursework for CS-671: Deep Learning and Its Applications at IIT Mandi.
