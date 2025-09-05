# AutoDegree-PolyReg

![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

A Python implementation of polynomial regression, built from scratch with NumPy, that automatically selects the optimal model degree.

## About The Project

Standard polynomial regression requires the user to manually specify the degree of the polynomial. This can be a tedious process of trial and error, often leading to models that are either too simple (**underfitting**) or too complex (**overfitting**).

This project solves that problem by implementing a model selection wrapper that automatically tests a range of degrees and selects the one that performs best on unseen data.

### Key Features 🎯

* **Automatic Degree Selection**: No more guessing! The model finds the best polynomial degree by evaluating performance on a validation set.
* **Built from Scratch**: The core gradient descent algorithm is implemented using only **NumPy** for numerical operations, making the logic transparent and easy to understand.
* **Visualization**: Generates a plot of validation error vs. polynomial degree, giving you a clear view of why the optimal degree was chosen.

---

## How It Works 🧠

The model selection process follows a standard cross-validation methodology:

1.  **Shuffle & Split**: The input data is first shuffled and then split into a training set (80%) and a validation set (20%).
2.  **Iterate & Train**: The algorithm iterates through a range of specified degrees (e.g., 1 to 10). In each iteration, a new polynomial regression model is trained *only on the training data*.
3.  **Evaluate**: Each trained model's performance is then measured on the unseen **validation set**. The resulting error (cost) is recorded.
4.  **Select & Retrain**: The degree that yielded the lowest validation error is selected as the optimal degree. A final model is then trained on the **entire dataset** using this best degree to ensure it learns from all available data.

---

## Getting Started

To get a local copy up and running, follow these simple steps.

### Prerequisites

You'll need Python 3 and the following libraries:

* numpy
* matplotlib

You can install them via pip:
```sh
pip install numpy matplotlib
```

### Usage

1.  Clone the repo:
    ```sh
    git clone [https://github.com/your_username/AutoDegree-PolyReg.git](https://github.com/your_username/AutoDegree-PolyReg.git)
    ```
2.  Run the `main.py` file or integrate the functions into your own project.

Here's a quick example of how to use the main function:

```python
import numpy as np
from model import find_best_degree # Assuming you save the code in model.py

# Data with a clear quadratic trend
data = [
    [1, 10.5], [2, 19.8], [3, 37.2], [4, 61.1], [5, 94.5], [6, 137],
    [1.5, 14], [2.5, 27], [3.5, 45], [4.5, 75]
]

# Set the learning rate and kick off the process
alpha = 0.0001
find_best_degree(data, alpha, max_degree_to_test=8)

```

---

## Example Output

The script will print the validation cost for each tested degree and conclude with the best one found.

```
Testing degrees 1 through 8...

Degree 1: Validation Cost = 259.9812
Degree 2: Validation Cost = 0.6714
Degree 3: Validation Cost = 0.7321
Degree 4: Validation Cost = 0.8145
...

------------------------------------------
✅ Best degree found: 2
------------------------------------------

Training final model on all data with the best degree...

--- FINAL MODEL ---
Optimal Degree: 2
Weights (w): [2.951 2.011]
Bias (b): 5.432
```

Finally, it will display a plot showing how the validation error changes with the model's complexity, making it easy to see the optimal trade-off point.



---

## License

Distributed under the MIT License. See `LICENSE` for more information.
