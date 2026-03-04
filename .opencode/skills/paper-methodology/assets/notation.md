# Symbol & Notation Conventions

> Conventions extracted from 9 reference papers in geotechnical AI.
> Use these as defaults; override with project-specific definitions when needed.

---

## 1. Subscript System (Geotechnical)

| Subscript | Meaning | Example |
|-----------|---------|---------|
| w | wall / retaining structure | delta_w (wall displacement) |
| s | soil / surface | delta_s (soil displacement), E_s (soil modulus) |
| p | pipeline / pipe | delta_p (pipeline displacement) |
| h | horizontal | delta_h (horizontal displacement) |
| v | vertical | delta_v (vertical displacement) |
| max | maximum value | delta_max (maximum displacement) |
| i, j | spatial indices (node/point) | x_i (feature at node i) |
| t | time step index | h_t (hidden state at time t) |
| k | layer index | W^(k) (weight matrix at layer k) |
| l | l-th element / level | z_l (l-th stratum) |

---

## 2. Common Symbols

### 2.1 Geotechnical Parameters

| Symbol | Description | Unit |
|--------|-------------|------|
| H | Excavation depth / tunnel depth | m |
| D | Tunnel diameter | m |
| L | Length (wall, segment, etc.) | m |
| E_s | Soil elastic modulus | MPa / kPa |
| nu | Poisson's ratio | - |
| phi | Internal friction angle | degrees |
| c | Cohesion | kPa |
| gamma | Unit weight of soil | kN/m^3 |
| K_0 | Coefficient of earth pressure at rest | - |
| p | Earth pressure / applied pressure | kPa |
| delta | Displacement / deformation | mm |
| sigma | Stress | kPa / MPa |
| epsilon | Strain | - |

### 2.2 Neural Network Symbols

| Symbol | Description |
|--------|-------------|
| X | Input feature matrix |
| Y | Target / label matrix |
| Y_hat | Predicted output |
| W | Weight matrix |
| b | Bias vector |
| h | Hidden state |
| z | Latent representation |
| A | Adjacency matrix |
| D | Degree matrix |
| L | Laplacian matrix (or Loss) |
| sigma() | Activation function |
| theta | Learnable parameters |
| alpha | Attention weight / learning rate |
| N | Number of samples / nodes |
| T | Number of time steps |
| d | Feature dimension |
| K | Number of Chebyshev polynomial orders / heads |

### 2.3 GAN-Specific Symbols

| Symbol | Description |
|--------|-------------|
| G | Generator network |
| D | Discriminator network |
| z | Noise vector / latent input |
| x | Real sample |
| G(z) | Generated sample |
| L_G | Generator loss |
| L_D | Discriminator loss |
| L_adv | Adversarial loss |
| L_rec | Reconstruction loss |
| lambda | Loss weighting coefficient |

### 2.4 Evaluation Metrics

| Symbol | Description | Formula sketch |
|--------|-------------|---------------|
| RMSE | Root mean squared error | sqrt(mean((y - y_hat)^2)) |
| MAE | Mean absolute error | mean(|y - y_hat|) |
| MAPE | Mean absolute percentage error | mean(|y - y_hat| / |y|) * 100% |
| R^2 | Coefficient of determination | 1 - SS_res / SS_tot |

---

## 3. Notation Rules

### 3.1 Matrices and Vectors
- Matrices: bold uppercase (X, W, A)
- Vectors: bold lowercase (x, h, b)
- Scalars: italic lowercase (n, t, d)
- Sets: calligraphic uppercase (V for node set, E for edge set)

### 3.2 Functions and Operations
- Element-wise multiplication: circle-dot or Hadamard product symbol
- Matrix multiplication: no symbol (implied)
- Concatenation: [a; b] or [a || b]
- Softmax, ReLU, sigmoid: written as function names

### 3.3 Index Conventions
- Spatial index: i, j (nodes/points)
- Temporal index: t (time step)
- Layer index: k or l (network layer)
- Feature index: d or f (dimension)
- Batch index: n (sample in batch)
