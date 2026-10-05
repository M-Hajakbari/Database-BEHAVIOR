# MoBe: A Dual-Camera Benchmark for Motorcycle Detection under Dense Urban Traffic Conditions

## Overview
MoBe is a motorcycle-centred, dual-camera dataset and benchmark for motorcycle detection under dense urban traffic conditions. It comprises manually annotated traffic imagery acquired from two fixed roadside cameras at a busy signalized urban intersection.

The complete MoBe corpus contains **19 video clips, 49,775 annotated frames, 303,389 motorcycle bounding boxes, and 1,193 unique motorcycle IDs**.

## Data Collection

### Source
- **Provider**: Crisis Management Headquarters of Qom Municipality
- **Acquisition setting**: Busy signalized urban intersection
- **Cameras**: Two fixed roadside cameras providing complementary views
- **Conditions**: Daylight under naturally occurring urban traffic conditions

### Camera Setup

**Camera 1**
- Resolution: **800 × 450 pixels**
- Clips: **V1–V12** (12 clips)
- Frames: **35,209**
- Bounding boxes: **217,532**
- Unique motorcycle IDs: **767**

**Camera 2**
- Resolution: **1920 × 1080 pixels**
- Clips: **V13–V19** (7 clips)
- Frames: **14,566**
- Bounding boxes: **85,857**
- Unique motorcycle IDs: **426**

## Dataset Statistics

| Parameter | Camera 1 | Camera 2 | Total |
|---|---:|---:|---:|
| **Clips** | 12 | 7 | **19** |
| **Frames** | 35,209 | 14,566 | **49,775** |
| **Bounding Boxes** | 217,532 | 85,857 | **303,389** |
| **Unique Motorcycle IDs** | 767 | 426 | **1,193** |
| **Resolution** | 800 × 450 | 1920 × 1080 | — |

A unique motorcycle ID is maintained across consecutive frames for as long as the motorcycle can be followed reliably. Persistent identities form an annotation layer in addition to the bounding boxes used for object detection.

## Dataset Partitioning
The 19 clips are assigned to mutually exclusive training, validation, and test partitions at the **video-clip level**. All frames, bounding boxes, and motorcycle identity annotations from a clip remain within the same subset.

| Partition | Clips | Frames | Bounding Boxes | Unique Motorcycle IDs |
|---|---:|---:|---:|---:|
| Training | 10 | 26,399 | 159,750 | 653 |
| Validation | 5 | 13,031 | 77,948 | 307 |
| Test | 4 | 10,345 | 65,691 | 233 |
| **Total** | **19** | **49,775** | **303,389** | **1,193** |

### Clip Assignments
- **Training**: V1, V3, V5, V7, V9, V11, V13, V15, V17, V19
- **Validation**: V2, V6, V10, V14, V18
- **Test**: V4, V8, V12, V16

Camera 1 comprises **V1–V12**, and Camera 2 comprises **V13–V19**. In particular, **V12 belongs to Camera 1 and the test partition**.

## Challenge Characteristics

### Traffic Density
Frame-level motorcycle density is defined as:
- **Sparse**: ≤2 motorcycles per frame
- **Moderate**: 3–5 motorcycles per frame
- **Dense**: ≥6 motorcycles per frame

Across the complete MoBe dataset:
- Sparse: **4,223 frames (8.48%)**
- Moderate: **19,254 frames (38.68%)**
- Dense: **26,298 frames (52.83%)**

The value **56.30% Dense** applies specifically to the held-out test partition, not to the complete dataset.

### Object Scale
Instance-level object scale is defined using ground-truth bounding-box area in the native image coordinate system:
- **Small**: area < 32² pixels
- **Medium**: 32² ≤ area < 96² pixels
- **Large**: area ≥ 96² pixels

Across all **303,389** annotated motorcycle instances:
- Small: **147,416 (48.59%)**
- Medium: **154,548 (50.94%)**
- Large: **1,425 (0.47%)**

## Annotation Methodology

### Annotation Policy
All visible motorcycles are considered annotation targets irrespective of motion state. Moving, temporarily stopped in traffic, parked or stationary motorcycles, and motorcycles visible without a rider are retained when their boundaries can be identified reliably.

Partially occluded motorcycles are retained whenever the visible portion provides sufficient visual evidence for reliable localization. Bounding boxes are defined with respect to the visible motorcycle extent rather than extrapolating extensively through unobservable regions. Fully occluded instances and objects for which motorcycle identity cannot be determined reliably are not annotated. Small and distant motorcycles are retained when they remain visually identifiable; object size alone is not used as an exclusion criterion.

Annotation was performed manually using Label Studio by multiple annotators following a common annotation policy. Detection annotations were exported in **YOLO-compatible text format**, while richer **JSON records** preserve persistent motorcycle identifiers.

### YOLO Detection Format
Each line follows:

`class_id center_x center_y width height`

The detection task contains one class: **motorcycle**.

## Repository Contents

### Current Availability
This repository is the author-controlled project repository for MoBe. A **representative subset of the MoBe dataset, together with sample annotations and documentation**, is intended to be publicly available through the project repository.

The complete dataset should not be inferred from the files currently present in this repository. The authoritative clip convention is:
- **V1–V12: Camera 1**
- **V13–V19: Camera 2**

## Full Dataset Availability
A representative subset of the MoBe dataset, together with sample annotations and documentation, is publicly available at the project repository.

The complete dataset comprises **19 video clips, 49,775 annotated frames, 303,389 motorcycle bounding boxes, and 1,193 persistent motorcycle identities**. The complete dataset is **planned for archival release through Zenodo with a persistent DOI**. During peer review, access to the complete dataset can be provided to editors and reviewers upon request for verification purposes.

## Code Availability
Implementation and evaluation resources associated with this study are available through the project repository. Additional materials required for reproducing the reported experiments can be provided for peer-review purposes upon request.

## Citation
If you use MoBe in your research, please cite the associated manuscript when bibliographic details become available:

**MoBe: A Dual-Camera Benchmark for Motorcycle Detection under Dense Urban Traffic Conditions**

Citation details will be added upon publication.

## Contact
- **Corresponding Author**: Maryam Sadat Hajakbari
- **Email**: m.hajakbari@iau.ac.ir
- **Affiliation**: Department of Computer Engineering, Qo.C., Islamic Azad University, Qom, Iran.

## Acknowledgments
The authors thank the Crisis Management Headquarters of Qom Municipality for providing access to the surveillance footage used to construct the MoBe dataset.
