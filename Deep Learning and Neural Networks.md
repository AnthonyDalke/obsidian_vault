## 1. Linear Algebra (Vectors & Matrices)

- **System of Equations:** Multiple equations that must remain true simultaneously.
- **Vector Space:** A set of points available or under consideration.
- **Vectors vs. Scalars:**
  - **Scalars:** Contain magnitude only (length). Negative scalars flip the direction of vectors.
  - **Vectors:** Entail both direction and magnitude.
- **Vector Notation:**
  - Unit: $v = ai + bj + ck$ (first term: scalars, second term: axis $x, y, z$).
  - Matrix: $v = [a\ b\ c]$ or vertically $v = \begin{bmatrix} a \\ b \\ c \end{bmatrix}$.
  - Ordered set: $v = (a, b, c)$.
- **Vector Operations:**
  - **Addition:** Add magnitudes of like axes ($i$ to $i$, $j$ to $j$, $k$ to $k$).
  - **Scalar Multiplication:** Apply a scalar to each magnitude of a vector.
  - **Dot Product (Inner Product):** Multiply magnitudes of like axes (results in a scalar, unlike addition).
  - **Cross Product:** Results in a vector perpendicular to the multiplied vectors.
    - *Example:* For $v_1 = 7i + 2j + 3k$ and $v_2 = 1i - 5j + 4k$, the components evaluate as:
      - $2 * 4 - 3 * -5 = 23$
      - $7 * 4 - 3 * 1 = 25$
      - $7 * -5 - 2 * 1 = -37$
      - Result: $v = 23i - 25j - 37k$
- **Matrix Operations:**
  - **Addition:** Requires matrices of the same size/structure; perform element-wise addition.
  - **Scalar Multiplication:** Element-wise multiplication by the scalar value.
  - **Transposition:** "Flipping" a matrix so an $m \times n$ matrix becomes $n \times m$.
  - **Multiplication:**
    - The number of columns in the first matrix must match the number of rows in the second matrix.
    - The output matrix has the row count of the first matrix and the column count of the second ($m \times n$).
    - Calculated by finding the dot products of each row and column combination.
    - *Example:* Multiplying two $2 \times 3$ matrices evaluates row/column dot products across the structures.

## 2. Linear Regression & Residual Assumptions

Assumptions for residuals aim to ensure data comes from representative, unbiased samples:
- **Zero mean:** Not skewed.
- **Common variance:** Homoscedasticity (not skewed).
- **Independent of each other:** Prevents pollution of the relationship between $x$ and $y$.
- **Independent of the x-axis:** Not influenced by covariance.
- **Normally distributed:** Symmetric distribution of errors.

## 3. Neural Networks

- **Neurons:**
  - Evaluate functions, with weights stored in the "edges" linking neurons.
  - Weights get summed and represent **model parameters**.
  - Training a neural network finds optimal values for both weights ($W$) and bias ($b$).
- **Two Types of Functions in Neurons:**
  1. **Linear Transformation (Affine Transformation):**
     - Applies weights to inputs from the preceding layer and adds a bias.
     - Takes the form: $y = Wx + b$.
     - Feeds directly into the activation function.
  2. **Activation Function:**
     - Introduces non-linearity into the model.
     - Produces the output of the neuron, which feeds into the next layer via weights.
     - *Note:* When utilizing purely linear regression, the activation function becomes unnecessary due to the lack of non-linear requirements.
- **Examples of Activation Functions:**
  - **ReLU (Rectified Linear Unit):** Assigns $0$ to any value $< 0$. Boasts the advantage of potentially reducing training time.
  - **Logit (SoftMax):** Outputs probabilities; often used in the final layer.
  - **Tanh:** S-shaped curve mapping values between $-1$ and $1$.
  - **Step Function:** Binary output based on a threshold.
- **Training Dynamics:**
  - Epochs cover the entire training dataset, broken down into batches.
  - Training epochs consist of **forward passes** and **backpropagation**, demarcated by loss calculation.

## 4. Convolutional Neural Networks (CNNs)

- **Purpose:** Address shortcomings of dense neural nets when working with image data, specifically "parameter explosion" from high dimensionality and the incompatibility between spatial data structures and standard dense layers.
- **Characteristics of Images:**
  - Fundamentally involve grid-like data.
  - Require an iterative process of extracting data from localized fragments (subsets) and assembling them hierarchically.
- **Key Layers:**
  - **Convolutional Layer:** Kernels focus on specific areas of an image, multiplying parameter values by pixel values to aggregate into a **feature map**.
  - **Pooling Layer:** Summarizes or downsamples regions of an image using aggregate functions (e.g., max pooling, average pooling).
  - Convolutional and pooling layers typically alternate.

## 5. Recurrent Neural Networks (RNNs) & NLP

- **Recurrent Neural Networks (RNNs):**
  - Best suited for sequential or time-based data (unlike feed-forward networks, which assume independent data points).
  - Incorporate recurrent neurons that apply weightings to outputs of previous steps in a sequence alongside current inputs (forming a **hidden layer**).
  - Contain as many layers as time sequences (e.g., 10 time periods = 10 layers).
  - **LSTM (Long Short-Term Memory):** Expands the time horizons considered by hidden layers.
- **Methods for Encoding Words as Numbers:**
  - One-hot encoding
  - Count-vector encoding
  - TF-IDF (Term Frequency-Inverse Document Frequency)