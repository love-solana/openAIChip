# Source Code Directory

This directory will contain simulation models, hardware description language (HDL) sketches, and experimental neuromorphic computing code.

## Planned Contents

### Simulations
- **`snn_models/`**: Spiking neural network simulators and neuron models
  - Leaky Integrate-and-Fire (LIF) neurons
  - Izhikevich models for biological realism
  - Spike-timing-dependent plasticity (STDP) learning rules

### HDL / RTL Prototypes
- **`rtl/`**: Verilog/SystemVerilog or VHDL implementations
  - Neuron state machines
  - Address-event representation (AER) routers
  - Synaptic crossbar arrays

### Analysis Scripts
- **`analysis/`**: Python scripts for power modeling, area estimation, and performance benchmarking
  - Energy-per-spike calculations
  - Latency profiling
  - Comparison with GPU baselines

### Datasets & Preprocessing
- **`datasets/`**: Event-based datasets (DVS camera recordings, neuromorphic audio)
  - Preprocessing pipelines to convert frame-based data to spike trains

## Getting Started

Once code is added to this directory, installation and usage instructions will be provided here.

## Dependencies

Anticipated dependencies for simulation and analysis:
- **Python 3.8+**: NumPy, SciPy, Matplotlib
- **Brian2** or **NEST**: For large-scale spiking network simulations
- **PyTorch** (optional): For surrogate gradient training of SNNs
- **Verilator** or **Icarus Verilog**: For HDL simulation

---

*This directory is currently a placeholder. Simulation models and HDL code will be added as the research progresses.*
