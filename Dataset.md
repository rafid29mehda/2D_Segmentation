The **BOston Neonatal Brain Injury Dataset for Hypoxic Ischemic Encephalopathy (BONBID-HIE)** is a specialized dataset for segmenting and analyzing neonatal brain injuries in MRI scans. Below is a detailed analysis and understanding of the dataset:
https://zenodo.org/records/10602767
---

### **Dataset Summary**

#### 1. Purpose
- The dataset focuses on **Hypoxic Ischemic Encephalopathy (HIE)**, a brain injury condition in neonates.
- It provides MRI data and lesion annotations to fuel the development of segmentation models for:
  - Identifying HIE-related lesions.
  - Predicting patient prognosis.
  - Evaluating treatment effects.

#### 2. Key Characteristics
- **Patient Data**: 133 neonatal patients born between 2001 and 2018.
- **Lesion Characteristics**:
  - Diffuse (multi-focal) and often small, with over half the patients having lesions occupying <1% of brain volume.
  - Segmentation of these lesions is challenging compared to tasks like brain tumor segmentation.

---

### **File Structure**

The dataset is organized into three main subfolders:

#### A. **BONBID2023_Train**
- Contains 85 volumes for training, divided into three subfolders:
  - **1ADC_ss**: Skull-stripped ADC (Apparent Diffusion Coefficient) maps.
    - Example filename: `MGHNICU_010-VISIT_01-ADC_ss.mha`.
  - **2Z_ADC**: Normalized ADC maps (`ZADC`), highlighting voxel intensities relative to healthy neonates.
    - Example filename: `Zmap_MGHNICU_010-VISIT_01-ADC_smooth2mm_clipped10.mha`.
  - **3LABEL**: Manual lesion annotations created by experts.
    - Example filename: `MGHNICU_010-VISIT_01_lesion.mha`.

#### B. **BONBID2023_Test**
- Contains test data organized in the same structure as the training set, for evaluating model performance.

#### C. **BONBID2023_Val**
- Contains validation data with the same structure as the training and test sets.

---

### **Data Pre-Processing**

#### 1. Input Data
- Each data point consists of:
  - **Skull-stripped ADC map (`xss`)**: Reflects diffusion within the brain.
  - **ZADC map (`xz`)**: Normalized map for highlighting voxel intensities relative to healthy controls.

#### 2. Normalization
- **Z-Score Normalization**:
  - Input maps are normalized, assigning the background a constant value of `-6`.
  - Normalized maps are represented as:
    - \( zss \): Normalized ADC map.
    - \( zz \): Normalized ZADC map.

#### 3. Input Dimensions
- The normalized maps \( zss \) and \( zz \) are concatenated to form a 2-channel input image \( x \in \mathbb{R}^{2 \times h \times w} \).
- Each image is resized to **256×256 pixels** before being fed to the model.

---

### **Dataset Files**

#### 1. Data Formats
- Files are stored in `.mha` format (MetaImage file format), which supports multi-dimensional medical images.

#### 2. Contents
- **1ADC_ss**: Raw diffusion MRI data, skull-stripped.
- **2Z_ADC**: Pre-processed ZADC maps highlighting lesion areas.
- **3LABEL**: Ground truth labels for lesion segmentation.

#### 3. Metadata
- Files are named systematically, providing patient identifiers, visit information, and modality type.

---

### **Challenges Addressed by the Dataset**
- **Diffuse Lesion Segmentation**:
  - Lesions are small and spread across multiple regions, making segmentation particularly challenging.
- **Medical Context**:
  - Supports research into understanding neonatal brain injuries and improving clinical outcomes.

---

### **Potential Use Cases**
- **Model Development**:
  - Train and test deep learning models for lesion segmentation in neonatal MRI scans.
- **Clinical Applications**:
  - Assist in predicting patient prognosis and evaluating treatment responses.
- **Research**:
  - Investigate the neurological basis of HIE and its impact on neonatal health.

---

### **How to Use the Dataset**
1. **Pre-processing**:
   - Normalize ADC and ZADC maps as described.
   - Resize the input to 256×256 pixels.

2. **Model Input**:
   - Use the concatenated 2-channel image \( x \) (ADC + ZADC) as input to segmentation models.

3. **Evaluation**:
   - Train on the `BONBID2023_Train` set.
   - Validate using `BONBID2023_Val`.
   - Evaluate model performance on `BONBID2023_Test`.

4. **Metrics**:
   - Use metrics like Dice Similarity Coefficient (DSC) or Intersection-over-Union (IoU) to evaluate segmentation accuracy.

Would you like guidance on implementing a segmentation pipeline, pre-processing the data, or analyzing specific aspects of the dataset?
