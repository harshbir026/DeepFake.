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
└── README.txt

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
