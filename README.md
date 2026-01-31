# Probability-density-function-using-GAN
Learning probability density functions using GAN (data only)


📌 Project Overview

This project focuses on learning the probability density function (PDF) of a transformed random variable using only data samples, without assuming any analytical or parametric form of the distribution.

A Generative Adversarial Network (GAN) is used to implicitly model the unknown probability distribution of the transformed variable. The generator learns to produce samples that resemble the real data distribution, and the learned PDF is approximated using histogram-based density estimation.

All steps — data preprocessing, transformation, GAN training, and PDF approximation — are implemented in a single Jupyter Notebook to ensure clarity, reproducibility, and ease of experimentation.

🎯 Project Objectives

Learn an unknown probability density function from data samples only

Apply a non-linear transformation to real-world data

Design a simple GAN suitable for 1-D distribution learning

Generate samples from the trained generator

Approximate and visualize the learned PDF

Analyze training behavior and quality of generated distribution

📂 Repository Structure
Learning-PDF-using-GAN/
│
├── gan_pdf_learning.ipynb      # Complete implementation
├── README.md                   # Project documentation

🔄 Overall Workflow

The project follows a structured pipeline from raw data to PDF estimation.

🧭 Complete Experiment Flow
flowchart TD
    A[Load Air Quality Dataset] --> B[Extract NO2 Values]
    B --> C[Apply Non-Linear Transformation]
    C --> D[Obtain Transformed Variable z]
    D --> E[Train GAN on z Samples]
    E --> F[Generate Samples from Generator]
    F --> G[Estimate PDF using Histogram]
    G --> H[Analyze Results]

⚖️ Dataset Description

The dataset contains air quality measurements collected across India

The NO₂ (Nitrogen Dioxide) concentration is used as the input feature

Only raw NO₂ values are used — no labels or additional attributes

The dataset serves as a real-world continuous random variable

🔁 Step 1: Data Transformation

To introduce non-linearity and make the distribution unknown, each NO₂ value x is transformed using:

𝑧
=
𝑥
+
𝑎
𝑟
sin
⁡
(
𝑏
𝑟
𝑥
)
z=x+a
r
	​

sin(b
r
	​

x)

Where:

𝑎
𝑟
=
0.5
×
(
𝑟
 
m
o
d
 
7
)
a
r
	​

=0.5×(rmod7)

𝑏
𝑟
=
0.3
×
(
(
𝑟
 
m
o
d
 
5
)
+
1
)
b
r
	​

=0.3×((rmod5)+1)

𝑟
r is the university roll number

This transformation produces a new random variable z, whose probability distribution is unknown and non-parametric.

🤖 Step 2: PDF Estimation using GAN

A Generative Adversarial Network (GAN) is used to learn the distribution of the transformed variable z.

🔧 GAN Architecture
Generator

Input: 1-D noise sampled from N(0,1)

Architecture: Fully connected layers with ReLU activation

Output: A single scalar value (fake z sample)

Discriminator

Input: A single scalar value (real or fake z)

Architecture: Fully connected layers

Output: Probability (real vs fake) using Sigmoid activation

🧠 GAN Training Flow
flowchart LR
    A[Noise ~ N(0,1)] --> B[Generator]
    B --> C[Fake z Samples]
    D[Real z Samples] --> E[Discriminator]
    C --> E
    E --> F[Loss Computation]
    F --> B

🔑 Key Properties

The GAN learns only from samples of z

No parametric PDF (Gaussian, Exponential, etc.) is assumed

The generator implicitly models the PDF through sample generation

📊 Step 3: PDF Approximation from Generator Samples

After GAN training:

A large number of samples are generated using the trained generator

These samples represent the learned distribution

The probability density function 
𝑝
ℎ
(
𝑧
)
p
h
	​

(z) is approximated using:

Histogram Density Estimation

📈 PDF Estimation Flow
flowchart TD
    A[Trained Generator] --> B[Generate Large z_f Samples]
    B --> C[Histogram Density Estimation]
    C --> D[Approximate PDF Plot]

📉 Results and Visualization

The histogram of generated samples provides a smooth approximation of the PDF

The generated distribution closely follows the shape of the real transformed data

Increasing the number of generated samples improves PDF smoothness

(Plots are generated directly in the notebook.)

🧠 Observations
🔹 Mode Coverage

The generator successfully captures the dominant regions of the transformed data distribution. Major modes of the real data are reflected in the generated samples.

🔹 Training Stability

After sufficient epochs, both generator and discriminator losses stabilize. No major oscillations or divergence are observed, indicating stable GAN training.

🔹 Quality of Generated Distribution

The generated samples closely resemble the real transformed variable in terms of spread and shape. Minor discrepancies exist, which are expected in GAN-based density estimation.

✅ Conclusion

GANs can effectively learn unknown probability density functions using data alone

A simple fully connected GAN is sufficient for 1-D distribution learning

Histogram-based estimation provides a clear visualization of the learned PDF

The approach avoids any parametric assumptions and relies purely on data-driven learning

🚀 How to Use This Repository

Clone the repository

Open gan_pdf_learning.ipynb

Run all cells sequentially

Modify GAN parameters or transformation constants if required

Observe how the learned PDF changes

This repository can be used as:

📘 Academic assignment submission

🧪 Learning reference for GAN-based density estimation

🔁 Reproducible experimentation template

📌 Author Note

This project emphasizes conceptual clarity, non-parametric learning, and reproducibility.
It demonstrates how generative models can be used beyond images — to learn probability distributions directly from data.
