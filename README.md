# medical-image-annotation-guidelines
Open SOP, QC checklist, edge-case log and inter-annotator agreement templates for building high-quality medical imaging datasets for AI.

![License: CC BY 4.0](https://img.shields.io/badge/license-CC%20BY%204.0-blue)
![Status](https://img.shields.io/badge/status-active-brightgreen)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-orange)

**Open templates for building high-quality, AI-ready medical imaging datasets.**

Write an annotation SOP, run quality control, log edge cases, and measure inter-annotator agreement, all with plain Markdown files you can copy and adapt.

> A model is only as reliable as the labels it learns from. Consistent labels start with clear written rules.

---

## Contents

| File | Purpose |
|---|---|
| [`sop-template.md`](sop-template.md) | Annotation SOP with inclusion/exclusion criteria and labeling rules |
| [`qc-checklist.md`](qc-checklist.md) | Multi-level quality control checklist |
| [`edge-cases.md`](edge-cases.md) | Log for ambiguous findings and the decisions made |
| [`iaa-guide.md`](iaa-guide.md) | Measuring inter-annotator agreement (Dice, IoU, Cohen's kappa) |

## Who this is for

- ML engineers and data scientists preparing training data
- AI product teams working in radiology, cardiology, neurology, ophthalmology, dental, and other specialties
- Annotation team leads and clinical reviewers
- Researchers who need reproducible labeling protocols

## Recommended workflow

```text
Dataset intake -> SOP drafting -> Pilot annotation -> Agreement check
      -> SOP revision -> Full annotation -> QC and release
```

1. **Dataset intake:** confirm modality, volume, file format (DICOM, NIfTI, PNG), and de-identification status.
2. **SOP drafting:** copy `sop-template.md` and complete it with your clinical lead.
3. **Pilot:** have 2 to 3 annotators label the same 20 to 50 cases.
4. **Agreement check:** measure with `iaa-guide.md`. Low agreement usually points to an unclear SOP, not careless annotators.
5. **Revise and train:** update the SOP, log edge cases, retrain annotators.
6. **Production annotation:** label at scale with periodic QC sampling.
7. **Release:** run the final checks in `qc-checklist.md` before delivery.

## Quick start

```bash
git clone https://github.com/<your-username>/medical-image-annotation-guidelines.git
cd medical-image-annotation-guidelines
cp sop-template.md my-project-sop.md
```

Open `my-project-sop.md` and replace every `[PLACEHOLDER]`.

## Supported modalities

CT · MRI · X-ray · Ultrasound · Fundus / OCT · Endoscopy · Dental radiographs (OPG, CBCT) · Histopathology (adaptable)

## Annotation types covered

Classification · Bounding box · Polygon · Pixel-level segmentation · 3D volumetric segmentation · Landmarks / keypoints · Measurements

## Example: agreement check in Python

```python
import numpy as np

def dice(a, b, eps=1e-8):
    a, b = a.astype(bool), b.astype(bool)
    inter = np.logical_and(a, b).sum()
    return 2 * inter / (a.sum() + b.sum() + eps)
```

See [`iaa-guide.md`](iaa-guide.md) for IoU, kappa, and how to interpret scores.

## Privacy and compliance

These are **process documents only**. Never commit patient data, DICOM files with identifiers, or any protected health information (PHI) to this repository. Follow the laws and ethics requirements that apply to you (HIPAA, GDPR, India's DPDP Act, etc.).

## Disclaimer

These templates support dataset creation workflows. They are not medical advice and not a substitute for clinical judgment or regulatory guidance.

## Contributing

Contributions are welcome:

- Modality-specific checklists (breast ultrasound, prostate MRI, chest CT, and more)
- Translations
- Additional agreement metrics
- Corrections and clarifications

Please open an issue to discuss your idea, then submit a pull request.

## License

Released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). You may use and adapt these templates with attribution.

## About

Maintained by **Pareidolia Systems LLP**, a Kolkata-based team providing medical image segmentation, annotation, quality control, and 3D model creation for healthcare AI.

- Website: https://pareidolia.in/
- Contact: contact@pareidolia.in
- Learn more: [Inter-Annotator Agreement in Medical Imaging](https://pareidolia.in/inter-annotator-agreement-in-medical-imaging/)

If this repo helps your project, consider giving it a star ⭐
