# Binary Shape Analysis Tool

A Python-based tool for analyzing and classifying shapes in binary images using custom K-Nearest Neighbors (KNN) implementation. This academic project demonstrates object-oriented design, algorithm implementation, and computer vision techniques.

## Project Overview

The project consists of three main components working together:
1. A custom KNN classifier implementation
2. A shape analysis and feature extraction system
3. A Qt-based GUI for visualization and interaction

## Core Components

### KlustrDataClassifier
The high-level interface that orchestrates the shape analysis process:
```python
from dev.src.knn.KlustrDataClassifier import KlustrDataClassifier

# Classify a shape from a QImage
features = KlustrDataClassifier.classify(qimage)
# Returns geometric features (isoperimetric_quotient, centroid_area_ratio, min_max_radius_ratio)
```

### Custom KNN Implementation
A flexible, reusable K-Nearest Neighbors implementation with several key features:

```python
from dev.src.knn.Knn import Knn

# Initialize with customizable parameters
knn = Knn(k=3, distance_max=0.5)

# Dynamic K-value optimization
optimal_k = knn.k_recommended  # Automatically calculated based on dataset
max_possible_k = knn.k_max    # Maximum valid K for the current dataset

# Flexible training data management
knn.training_data = initial_dataset
knn.set_training_data_chunk(new_examples)  # Add batch of examples
knn.set_training_data_single(single_example)  # Add individual example

# Classification with distance thresholding
result = knn.prediction(unknown_point)  # Returns "Unknown" if no close matches
```

Key Features of KNN Implementation:
- Lazy evaluation for performance optimization
- Distance-based outlier detection
- Dynamic K-value recommendations
- Tied-vote handling using average distances
- Support for incremental training data updates

## Technical Implementation Details

### Feature Extraction
The system extracts geometric features including:
- Isoperimetric quotient (circularity measure)
- Centroid-area ratio
- Min-max radius ratio from centroid

### Architecture
The project demonstrates several design patterns and principles:
- Lazy Evaluation: Cached calculations for performance
- Encapsulation: Clear separation between public interfaces and implementation details
- Composition: Components work together while maintaining independence
- Type Hints: Python type annotations for better code documentation

## Requirements

- Python 3.x
- NumPy: For efficient numerical computations
- PySide6: For the GUI implementation

## Project Structure

```
dev/src/
├── knn/
│   ├── KlustrDataClassifier.py   # High-level classification interface
│   ├── Knn.py                    # Custom KNN implementation
│   └── BinaryImageAnalyser.py    # Shape analysis implementation
├── widget/                       # GUI components
│   ├── QKnnApp.py               # Main application
│   ├── QKnnControlPannel.py     # Parameter controls
│   ├── QPreview.py              # Image visualization
│   └── QInfoPannel.py           # Results display
├── db/                          # Database utilities
└── main.py                      # Application entry point
```

## Running the Application

```bash
python dev/src/main.py
```

## Technical Challenges and Solutions

1. **Performance Optimization**
   - Implemented lazy evaluation for computationally expensive operations
   - Used NumPy vectorization for efficient calculations
   - Cached intermediate results

2. **Classification Robustness**
   - Implemented distance thresholding for outlier detection
   - Handled tied votes using average distances
   - Dynamic K-value recommendations based on dataset characteristics

3. **Maintainable Architecture**
   - Clear separation of concerns between components
   - Well-defined interfaces for each module
   - Type hints for better code documentation and maintenance

## Contact

For questions about this academic project:

Email: hello@juliencm.dev
