# Backpropagation

Backpropagation efficiently computes how each model parameter contributed to the loss. An optimizer uses these gradients to update billions of parameters.

## Training Step

~~~mermaid
flowchart LR
    B["Token batch"] --> F["Forward pass"]
    F --> L["Compute loss"]
    L --> BP["Backward pass"]
    BP --> G["Gradients"]
    G --> O["Optimizer step"]
    O --> W["Updated weights"]
    W --> F
~~~

## Chain Rule

If the loss depends on a parameter through several operations, the chain rule multiplies local derivatives along the path:

~~~text
dLoss/dWeight =
    dLoss/dOutput
  × dOutput/dHidden
  × dHidden/dWeight
~~~

Automatic differentiation records the forward computation graph and traverses it backward.

## Gradient Descent

A simple update is:

~~~text
weight_new = weight_old - learning_rate × gradient
~~~

Modern training commonly uses Adam or AdamW, which maintain moving statistics of gradients. Weight decay, learning-rate schedules, and optimizer hyperparameters materially affect stability and generalization.

## Mini-Batches and Accumulation

Training uses mini-batches to estimate the gradient over the data distribution. Gradient accumulation processes several micro-batches before an optimizer step, allowing a larger effective batch than device memory alone permits.

~~~text
effective batch =
    micro-batch
  × accumulation steps
  × data-parallel workers
~~~

## Distributed Training

| Parallelism | Splits |
|---|---|
| Data parallelism | Batches across model replicas |
| Tensor parallelism | Matrix operations across devices |
| Pipeline parallelism | Layer groups across stages |
| Sequence parallelism | Sequence-related activations |
| Expert parallelism | Mixture-of-Experts experts |
| Sharded data parallelism | Parameters, gradients, optimizer state |

Large systems combine several forms. Communication and failure recovery become as important as arithmetic throughput.

## Precision and Memory

FP32 is accurate but expensive. BF16 and FP16 reduce memory and increase accelerator throughput. Mixed-precision training keeps sensitive operations or optimizer state at higher precision.

Activation checkpointing discards selected forward activations and recomputes them during backward pass, exchanging extra compute for lower memory.

## Gradient Problems

- exploding gradients can cause unstable loss or NaNs;
- vanishing gradients weaken learning in early layers;
- clipping can limit extreme gradient norms;
- warmup prevents large early updates;
- normalization and residual connections support stable deep networks.

Monitor gradient norms, update norms, learning rate, loss scale, memory, throughput, and hardware errors.

## Reproducibility

Record code, data order, random seeds, model initialization, optimizer state, precision, device count, and library versions. Distributed kernels may remain nondeterministic even with fixed seeds.

## Related Guides

- [Loss Functions](loss-functions.md)
- [Pretraining](pretraining.md)
