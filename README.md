

# Linear Optical Scheme for Heralded Dual-Rail Photonic W-State Generation

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This repository contains the complete circuit implementation data for the paper:

> **"Linear optical scheme for the heralded generation of dual-rail photonic W states"**  
> Authors  ....
> [Journal], [Year] ....

## Overview

We present an optimization-based approach for heralded preparation of dual-rail encoded W-states using linear optical circuits. Using Riemannian conjugate gradient optimization on the unitary manifold U(9), we achieve:

- **Ultra-high fidelity:** F = 99.9999%
- **Success probability:** P_succ = 0.069%
- **Resource efficiency:** 6 photons, 9 modes
- **Optimal circuit:** 36 beam splitters + 9 phase shifters

## Repository Contents

### Data Files (`data/`)

Complete circuit parameters from Supplementary Information:

- **`beam_splitters.csv`** - All 36 beam splitter parameters (Table S1)
  - Modes, transmittance, reflectance, and phase for each beam splitter
  
- **`phase_shifters.csv`** - All 9 output phase shifter parameters (Table S2)
  - Mode number and phase value for each phase shifter

- **`unitary_matrix.csv`** - Complete 9×9 unitary matrix (Table S3)
  - Real and imaginary components of all matrix elements

These files contain the complete specification needed to implement the optimized W-state generation circuit.

## Key Results

### Fabrication Sensitivity (Table S6)

| Tolerance Level | Error Magnitude | Success Retention | Fidelity |
|----------------|-----------------|-------------------|----------|
| Conservative   | ±0.5% T, ±π/200 φ | 19.1% ± 0.1% | 98.8% |
| Realistic      | ±1.0% T, ±π/100 φ | 9.3% ± 0.1%  | 98.8% |
| Challenging    | ±2.0% T, ±π/50 φ  | 4.7% ± 0.1%  | 98.8% |

### Critical Components (Table S5)

The five most critical beam splitters requiring enhanced fabrication precision:

| Component | Mode Coupling | Total Sensitivity | Primary Impact |
|-----------|---------------|-------------------|----------------|
| BS-9      | Modes 8-9     | 23.97%           | Herald channel mixing |
| BS-4      | Modes 5-6     | 23.78%           | Qubit-herald coupling |
| BS-5      | Modes 4-5     | 23.75%           | Qubit-herald coupling |
| BS-6      | Modes 3-4     | 23.71%           | Qubit-herald coupling |
| BS-2      | Modes 7-8     | 23.27%           | Herald channel mixing |

## Usage

### Loading Circuit Parameters

**Python:**
```python
import pandas as pd
import numpy as np

# Load beam splitter parameters
bs_params = pd.read_csv('data/beam_splitters.csv')
print(bs_params.head())

# Load phase shifter parameters
ps_params = pd.read_csv('data/phase_shifters.csv')
print(ps_params)

# Load unitary matrix
unitary = pd.read_csv('data/unitary_matrix.csv', index_col=0)
# Convert to complex numbers
unitary_complex = unitary.values.astype(complex)
```

**Julia:**
```julia
using CSV, DataFrames

# Load beam splitter parameters
bs_params = CSV.read("data/beam_splitters.csv", DataFrame)

# Load phase shifter parameters
ps_params = CSV.read("data/phase_shifters.csv", DataFrame)

# Load unitary matrix
unitary = CSV.read("data/unitary_matrix.csv", DataFrame)
```

**MATLAB:**
```matlab
% Load beam splitter parameters
bs_params = readtable('data/beam_splitters.csv');

% Load phase shifter parameters
ps_params = readtable('data/phase_shifters.csv');

% Load unitary matrix
unitary = readtable('data/unitary_matrix.csv');
```

## Circuit Implementation

The circuit uses a **Clements decomposition** architecture:
- 36 beam splitters arranged in triangular mesh layers
- 9 output phase shifters for final phase corrections
- Implements a 9×9 unitary transformation U on the input state

### Input Configuration
Six photons distributed across modes: {0, 1, 2, 6, 7, 8}

### Heralding Condition
Success is conditioned on detecting exactly one photon in each herald mode: {6, 7, 8}

### Target State
Three-qubit dual-rail encoded W-state:
```
|W⟩ = (1/√3)(|011010⟩ + |100110⟩ + |101001⟩)
```

## Performance

- **Perfect conditions:** 0.2446% success rate, 99.1615% fidelity
- **Realistic conditions (±1% tolerances):** 0.0228% success rate, 98.8% fidelity
- **Success retention under realistic fabrication:** 9.3% of ideal value
- **Fidelity stability:** Remains at ~98.8% across all tolerance scenarios

## Citation

If you use this data in your research, please cite:
```bibtex
@article{....
  note={Data available at https://github.com/SomiMehr4/W-State-Linear-Optics}
}
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact

For questions about this data or the paper:
- Open an issue on GitHub
- Email: s.mehrabankar@griffith.edu.au
## Acknowledgments

This work was conducted at ...

## References

See the paper and supplementary information for complete references.
