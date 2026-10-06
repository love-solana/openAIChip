# Technical Overview: Brain-Inspired Neuromorphic Computing

## Introduction

This document outlines the technical motivation and design considerations for the OpenChip project, focusing on the fundamental differences between brain-inspired neuromorphic architectures and conventional GPU-accelerated deep learning pipelines.

## Brain-Inspired vs. GPU Pipelines

### GPU-Accelerated Deep Learning

Modern deep learning relies on massively parallel matrix operations executed on GPUs:

- **Synchronous Computation**: All operations proceed in lockstep, driven by a global clock
- **Dense Activations**: Every neuron processes every input in each layer (though dropout and sparsity techniques exist)
- **High Precision**: 16-bit or 32-bit floating-point arithmetic is standard
- **Batch Processing**: Training requires large batches (32-1024+ samples) for efficient GPU utilization
- **Power Profile**: 100-400W TDP for datacenter GPUs; power consumption scales with compute intensity

**Strengths**: Excellent for training large models offline; mature software ecosystems; predictable performance.

**Limitations**: High power consumption; inefficient for sparse or event-driven workloads; poor energy scaling for inference at the edge.

### Neuromorphic Architectures

Brain-inspired systems adopt fundamentally different primitives:

- **Asynchronous Events**: Neurons communicate via discrete spikes only when thresholds are crossed
- **Sparse Activity**: Typical cortical firing rates are 1-10 Hz; most neurons are silent most of the time
- **Event-Driven Routing**: Communication occurs only when spikes are generated, reducing data movement
- **Local Computation**: Learning rules (e.g., STDP) operate on local spike timing without global gradients
- **Low Precision**: Binary or few-bit spike representations; information encoded in timing and patterns

**Strengths**: Potentially orders-of-magnitude better energy efficiency; natural fit for temporal/sequential data; continuous learning without retraining.

**Challenges**: Immature toolchains; difficult to program; limited applicability to tasks requiring high precision.

## Learning vs. Inference Considerations

### Training (Learning)

Neuromorphic systems typically employ **local learning rules** rather than backpropagation:

- **Spike-Timing-Dependent Plasticity (STDP)**: Synaptic weights adjust based on relative timing of pre/post-synaptic spikes
- **Hebbian Learning**: "Neurons that fire together, wire together"
- **Eligibility Traces**: Delayed reinforcement signals modulate recent synaptic activity

**Trade-offs**:
- ✅ No need for external gradient computation or weight updates from a host CPU/GPU
- ✅ Continuous adaptation without distinct train/deploy phases
- ❌ Convergence guarantees are weaker than backpropagation
- ❌ Difficult to scale to very deep networks (backprop solves credit assignment explicitly)

### Inference

For inference-only deployment, neuromorphic chips can be programmed with weights trained offline (via GPU-based surrogate gradient methods or rate-based SNNs):

- **Hybrid Workflow**: Train with backprop-compatible SNN simulators, then deploy weights to neuromorphic hardware
- **Rate Coding**: Encode inputs as spike trains where frequency represents activation magnitude
- **Latency Coding**: Use spike timing directly (e.g., earlier spikes = stronger features)

**Key Advantage**: Once deployed, inference power consumption can drop by 10-1000× compared to GPU inference, especially for sparse real-world inputs (e.g., event-based vision sensors).

## Design Philosophy for OpenChip

OpenChip research prioritizes:

1. **Realism**: Target manufacturable CMOS process nodes (28nm, 22nm) rather than exotic devices
2. **Measurability**: Quantify energy per spike-op, latency, and area for fair comparisons
3. **Co-Design**: Explore algorithms, architectures, and circuits together (not in isolation)
4. **Benchmarking**: Evaluate on tasks where neuromorphic approaches have theoretical advantages (not trying to beat GPUs at ImageNet classification)

## Next Steps

- Develop event-driven network simulators to model spike propagation and energy consumption
- Survey existing neuromorphic platforms (Loihi 2, TrueNorth, SpiNNaker, BrainScaleS) for architectural insights
- Prototype small-scale RTL blocks (leaky integrate-and-fire neurons, address-event representation routers)
- Identify target applications: keyword spotting, gesture recognition, robotic control

---

*This document will be updated as the research evolves and architectural decisions are refined.*
