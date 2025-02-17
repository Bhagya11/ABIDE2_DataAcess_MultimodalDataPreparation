DataLink: https://huggingface.co/datasets/Bhagya11/ASD_3D_Images2

# 🧠 **NIfTI Image Processing Data Extaraction (ABIDE11_DataAccess)**

This script processes **NIfTI (.nii/.nii.gz) medical images**, extracts **axial, sagittal, and coronal slices**, and saves them as grayscale PNG images.
## 🚀 Steps to Run the Script

1. **Install Dependencies**  
   Ensure Python (>=3.7) is installed, then run:  
   ```sh
   pip install nibabel pandas numpy matplotlib
   ```

2. **Prepare Dataset**  
   - Place **NIfTI** files in `D:\RawData` (or update script paths).  
   - Ensure `ABIDEII_Composite_Phenotypic.csv` exists for metadata.  

3. **Run the Script**  
   ```sh
   python process_nifti.py
   ```

4. **How It Works**  
   - Reads metadata (`SUB_ID` → `DX_GROUP`, `SITE_ID`).  
   - Finds **NIfTI** files in `D:\RawData\sub-XXXX\ses-XXX\anat\`.  
   - Extracts middle **axial, sagittal, coronal** slices.  
   - Saves them in `output/ABIDEII-SITEID_SUBID/` as:  
     - `ABIDEII-SITEID_SUBID_axial.png`  
     - `ABIDEII-SITEID_SUBID_sagittal.png`  
     - `ABIDEII-SITEID_SUBID_coronal.png`  
   - Prints success or error messages.  

5. **Verify Output**  
   Processed images appear in:  
   ```
   output/
   │── ABIDEII-OILH_2_28728/
   │   ├── ABIDEII-OILH_2_28728_axial.png
   │   ├── ABIDEII-OILH_2_28728_sagittal.png
   │   ├── ABIDEII-OILH_2_28728_coronal.png
   ```

---

# 🏥** Patient Data generation using OpenAI API (LLM_Data_ABIDE11)**

This script analyzes **patient metadata** using an OpenAI-compatible API and formats it into a **single English sentence** response.


## 🚀 Steps to Run the Script

1. **Install Dependencies**  
   Ensure Python (>=3.7) is installed, then install OpenAI’s API library:
   ```sh
   pip install openai
   ```

2. **Set Up API Connection**  
   - Default API base: `http://localhost:1234/v1` (modify if needed).
   - API key is set as `"not-needed"` by default for local deployments.

3. **Run the Script**  
   ```sh
   python analyze_patient.py
   ```

4. **How It Works**  
   - Reads patient metadata (Age, SEX, FIQ, Target) from a dictionary.
   - Sends the data to an OpenAI-compatible model.
   - Formats the response into a single English sentence.
   - Returns or prints the analyzed response.

5. **Example Input & Output**  
   ```python
   sample_data = {"Age": 55, "SEX": "Male", "FIQ": 126, "Target": "Treatment for Autism"}  
   response = analyze_patient_data(sample_data)
   print(response)
   ```
   **Output Example:**  
   _"A 55-year-old male with an FIQ of 126 is receiving treatment for autism."_


# **🧠 Autism Classification Dataset Preparation** (allslices_ABIDE11)

This script processes **3D brain scan slices** (axial, coronal, sagittal) for Autism classification and uploads them as a **Hugging Face dataset**.

---
## 🚀 Steps to Run the Script

### 1️⃣ **Install Dependencies**
Ensure Python (>=3.7) is installed, then install required libraries:
\

### 2️⃣ **Set Up Dataset Paths**
Modify the script to ensure paths to your dataset and metadata CSV (`abide2_label.csv`) are correct:
```python
root_dirs = {
    "Autism": r"D:\\ABIDE11_3Slices\\Autism",
    "NonAutism": r"D:\\ABIDE11_3Slices\\Non_Autism"
}
metadata_csv_path = "abide2_label.csv"
```


### 3 **Generated Files**
- **`updated_dataset.csv`**: Processed dataset with cleaned metadata.
- **Hugging Face dataset**: Uploaded automatically if `push_to_hub` is enabled.

---

### 📝 **Metadata Processing**
- Reads patient metadata from `abide2_label.csv`.
- Cleans column names and extracts numeric `SUB_ID`.
- Matches patients using `SUB_ID` and retrieves metadata fields like:
  - `Age`, `Sex`, `FIQ`, `HANDEDNESS_CATEGORY`, `Caption`.

### 📸 **Image Processing**
- Reads **axial, coronal, sagittal** MRI slices from patient folders.
- Ensures all three views are present before adding the patient.
- Stores image paths in the dataset.

### 📊 **Dataset Conversion**
- Converts processed data to a **Hugging Face Dataset**.
- Defines dataset features including images, labels, and metadata.

### 🚀 **Upload to Hugging Face** (Optional)
If enabled, the dataset is pushed to **Hugging Face Hub**:






