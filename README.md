# Cignal Public Safety Dataset (CPSD) Bug Reporting

This repository is dedicated to collecting bug reports and issues for CPSD datasets and benchmarks.

**Please DO NOT submit pull requests to this repository.** This repository is for issue tracking only.

## How to Report a Bug

If you encounter a bug or an unexpected behavior in the Cignal Scan Viewer, please open a new issue here. When reporting a bug, please include:

1.  A clear and concise description of the bug.
2.  Steps to reproduce the behavior.
3.  Expected behavior.
4.  Screenshots or videos (if applicable).
5.  Your operating system and browser information.

## The Cignal Stream of Commerce CT (Cignal-SoC-CT) Dataset

**Identifier:** `Cignal-SoC-CT-2.0mm-v1.0.0`  
**Version:** 1.0.0  
**Last Modified:** 2025-09-24  
**Request Access:** [https://huggingface.co/cignal-ai](https://huggingface.co/cignal-ai)  
**Origin:** Cignal, LLC.  

## Abstract

This dataset contains a collection of synthetic Computed Tomography (CT) scans of Stream of Commerce (SoC) items.  The SoC designation indicates that this public release consists exclusively of benign, non-threat items and materials.  It is released under the Cignal Public Safety License (https://github.com/cignal-ai/cignal-public-safety?tab=License-1-ov-file) to support a shared mission of advancing public safety and promoting security innovation. The data is intended for the development, training, and evaluation of automated threat detection algorithms, and to facilitate negative testing of threat detection systems to evaluate false alarm rates. **The synthetic nature of this dataset is specifically designed to empower researchers to experiment, validate new approaches, and publish results openly, while acknowledging the inherent scope and limitations of AI-generated data.** 

This initial release (`v1.0.0`) comprises 250 distinct scans generated using Cignal Engine v1.0.0, a patented physics-based neural renderer that uses Artificial Intelligence (AI) and physics-based simulation to generate synthetic data. Use of this dataset is strictly governed by the ethical principles outlined in its license, which are designed to prevent misuse and ensure all developments contribute positively to public safety and security.

## Data Description and Organization

The dataset is organized as a collection of directories, where each directory represents a single synthetic CT scan.

### Directory Structure
The top-level directory is named according to the dataset's identifier. Each scan has a dedicated subdirectory containing the DICOM file and a metadata manifest.

```
/CSOC-CT-2.0mm-v1.0.0/
    ├── SCAN_0001/
    │   ├── SCAN_0001.dcm
    │   └── manifest.json
    ├── SCAN_0002/
    │   ├── SCAN_0002.dcm
    │   └── manifest.json
    ...
    └── SCAN_0250/
        ├── SCAN_0250.dcm
        └── manifest.json
```

### File Formats
* **CT Scans:** Volumetric data is provided in the **DICOM (`.dcm`)** format.
* **Metadata:** Each scan includes a corresponding `manifest.json` file containing annotations and descriptive metadata.

### Metadata Schema (`manifest.json`)
The `manifest.json` file contains information about the primary scanned item and bounding box annotations for all objects within the volume. The schema for this file may be extended in future releases. The following fields are present in version `1.0.0`:

* `scan_id`: (String) A unique identifier that matches the parent directory name.
* `object_class`: (String) A high-level category for the primary scanned item (e.g., `"Backpack"`, `"Duffel Bag"`).
* `annotations`: (Array of Objects) A list containing information for each discrete object identified within the scan.
    * `object_label`: (String) The specific class of the annotated object (e.g., `"Laptop"`, `"Water Bottle"`, `"Shampoo"`).
    * `bounding_box`: (Array) An array of 6 floats representing the `[x, y, z]` min/max coordinates of a 3D bounding box.

## Technical Specifications and Limitations

### Acquisition and Generation
All CT volumes are synthetically generated using **Cignal Engine (v1.0.0)**, a proprietary physics-based neural renderer. The engine's default CT pipeline is designed to produce CT numbers, represented in Hounsfield Units (HU), that **emulate the material attenuation properties typically observed in commercial security screening systems**.

Rather than simulating a specific X-ray tube voltage (kVp), the model directly generates realistic HU values based on the physical properties and material definitions of the simulated objects.

### Technical Specifications
* **Voxel Resolution:** `2.0mm x 2.0mm x 2.0mm` (Isotropic)
* **Image Dimensions:** `256 x 256 x 375` voxels
* **Voxel Values:** Hounsfield Units (HU) with a **+1024 offset** applied to ensure all values are positive. Data is stored as 16-bit **unsigned** integers. To recover the original HU value, subtract 1024 from the voxel value.

### Known Limitations
* **Absence of Threat Items:** This public dataset consists exclusively of benign, non-threat items and materials.
* **Synthetic Nature:** As the data is entirely synthetic, it may not model certain artifacts found in physical scans, such as those from belt/gantry motion, severe beam hardening, model/OEM-specific noise and artifacts, or specific detector imperfections.
* **Material Fidelity:** The accuracy of the HU values is dependent on the material definitions within the Cignal Engine library. While extensive, this library may not capture the full variance of all real-world materials.
* **Scope:** This dataset represents a specific set of Stream of Commerce items and may not be fully representative of all possible items or configurations.
* **Z-effective data:** This release does not contain Z-effective (effective atomic number) data. This information may or may not be included in a future release.

## Intended Use and Usage Restrictions

This dataset is provided to support the shared mission of advancing public safety. All usage is governed by the principles outlined in the Cignal Public Safety License.  **Any legal use case not explicitly covered by the 'Intended Applications' below may require a separate commercial license. Please contact `security.datasets@cignalai.com` to inquire.**

### Intended Applications
The dataset is intended exclusively for the following beneficial purposes:  
1.  **Research and Development:** Training, validating, and testing algorithms for automated threat detection in a non-operational capacity.  
2.  **Negative Testing (False Alarm Rate Evaluation):** Measuring false alarm rates for threat detection systems.  
3.  **Benchmarking:** Performance evaluation and non-commercial benchmarking of security screening technologies.  
4.  **Publication:** Publishing research findings and sharing insights or models developed from this dataset openly with the community, in the spirit of collective advancement.  

### Prohibited Uses
Use of this dataset for the following purposes is strictly prohibited:  
* Any application that is **illegal, harmful, unethical, or contrary to human rights**.  
* The development or training of generative models for **any purpose**.  
* Applications designed to unlawfully **infringe upon civil liberties, conduct unlawful surveillance, or discriminate** against any individual or group.  
* This dataset **shall not** be used for any operational, real-world security screening, diagnostic, or law enforcement purposes. It is for research, education, and evaluation **only**.  

## Support and Commercial Inquiries

This public dataset is provided as a community resource on an 'as-is' basis without any warranty. Cignal does not offer free technical support, assistance with implementation, or troubleshooting for this public release.

For inquiries regarding **commercial licensing** of the Cignal Engine platform, **higher fidelity datasets** (including **higher-resolution scans** or precision annotations with **segmentation masks**), or **dedicated technical support and consulting services**, please visit `cignalai.com`.

## License

This dataset is distributed under the **Cignal Public Safety License**. By downloading, accessing, or using the dataset, you agree to be bound by the terms of this license.

The full license text is available at:
[https://github.com/cignal-ai/cignal-public-safety?tab=License-1-ov-file](https://cignalai.com/licenses/cignal_public_safety.html)

## Intellectual Property

### Copyright
Copyright © 2026 Cignal LLC. All Rights Reserved.

The images and all associated metadata contained within this dataset are the exclusive intellectual property of Cignal LLC.

### Trademarks
Cignal® is a registered trademark of Cignal LLC.

### Patents
The technology used to generate this dataset, Cignal Engine, is protected by U.S. Patent Nos. 11,893,088 and 12,361,099. Additional patents are pending.

## Citation

If you use this dataset in your research, publication, or software, please cite it as follows:

**Plain Text:**
> Cignal LLC. (2025). *The Cignal Stream of Commerce CT (Cignal-SoC-CT) Dataset* (Version 1.0.0) [Data set]. Retrieved from https://datasets.cignalai.com/cignal-soc-ct

**BibTeX:**

```bibtex
@misc{cignal_csoc_2025,
  author       = {Cignal LLC},
  title        = {The Cignal Stream of Commerce CT (Cignal-SoC-CT) Dataset},
  year         = {2025},
  publisher    = {Cignal LLC},
  version      = {1.0.0},
  howpublished = {\url{[https://datasets.cignalai.com/cignal-soc-ct](https://datasets.cignalai.com/cignal-soc-ct)}}
}
```

## Acknowledgements and Funding

Development of this data set was funded by the Department of Homeland Security, Science and Technology Directorate under Award Number 70RSAT24T00000023. The content is solely the responsibility of the authors and does not necessarily represent the official views of the Department of Homeland Security.






