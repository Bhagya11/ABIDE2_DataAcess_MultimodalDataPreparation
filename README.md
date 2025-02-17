# 🧠 NIfTI Image Processing Pipeline

This script processes **NIfTI (.nii/.nii.gz) medical images**, extracts **axial, sagittal, and coronal slices**, and saves them as grayscale PNG images.

---

## 📂 Directory Structure

```
D:\RawData
│── ABIDEII_Composite_Phenotypic.csv  # Metadata file
│── output/                            # Processed images will be saved here
│── process_nifti.py                   # Main script
```

---

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

## 🛠 Troubleshooting

| Issue | Solution |
|--------|----------|
| `❌ Error loading .nii file` | Check file paths and ensure valid NIfTI files. |
| `⚠️ Skipping SUB_ID` | Subject missing metadata in the CSV. |
| Images not appearing | Check the `output/` folder and set correct permissions. |

---

## 📜 License
This project is licensed under the **MIT License**.

---

## 🤝 Contributing
1. Fork the repo.  
2. Create a new branch (`git checkout -b feature-branch`).  
3. Commit changes (`git commit -m "Added feature X"`).  
4. Push to branch (`git push origin feature-branch`).  
5. Open a **Pull Request**.  

---

## 📧 Contact  
For queries, reach out to **[Your Name]** at [your.email@example.com](mailto:your.email@example.com).

