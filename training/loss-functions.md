# Loss Functions

A loss function converts model predictions and training targets into a scalar error. Optimization changes parameters to reduce the expected loss over the training distribution.

## Next-Token Cross-Entropy

For language modeling, the model predicts a probability distribution for the next token. If the correct token is “days” with probability 0.7:

~~~text
loss = -log(0.7)
~~~

Higher probability for the correct token produces lower loss.

For a sequence, training usually averages or sums loss over target positions while ignoring padding and any masked prompt tokens.

## From Logits to Loss

~~~mermaid
flowchart LR
    H["Hidden state"] --> Z["Vocabulary logits"]
    Z --> S["Softmax probabilities"]
    Y["Correct token"] --> CE["Cross-entropy"]
    S --> CE
    CE --> L["Scalar loss"]
    L --> B["Backpropagation"]
~~~

Implementations combine log-softmax and negative log likelihood for numerical stability.

## Perplexity

Perplexity is the exponential of average cross-entropy:

~~~text
perplexity = exp(average loss)
~~~

Lower perplexity indicates better prediction on that tokenized dataset. It is not comparable across different tokenizers without care and does not directly measure helpfulness, truthfulness, or safety.

## Masking

During supervised fine-tuning, loss may be computed only on assistant response tokens:

~~~text
System: ignored
User:   ignored
Assistant response: optimized
~~~

Training on every token can unintentionally teach the model to generate user or system messages. Mask choices are part of the objective and should be tested.

## Other Objectives

| Objective | Used for |
|---|---|
| Binary cross-entropy | Independent labels or classifiers |
| Mean squared error | Regression or value prediction |
| Contrastive loss | Pull related representations together |
| Ranking loss | Prefer one response or document over another |
| KL divergence | Keep a policy near a reference distribution |
| Policy-gradient loss | Increase probability of rewarded actions |
| Auxiliary router loss | Balance experts in MoE models |

A total objective can be a weighted combination of several terms. Weights determine real training behavior, not just reporting.

## Label Smoothing

Label smoothing assigns a small amount of probability to non-target classes. It can improve calibration in classification, but in large-vocabulary generation it changes the desired distribution and is not always used.

## Numerical Stability

Use stable library primitives, appropriate accumulation precision, gradient scaling for low-precision training, and monitoring for NaN or infinite values. A finite average can hide a small number of corrupted batches.

## Interpreting Loss Curves

Training loss falling while validation loss rises suggests overfitting or distribution mismatch. Sudden spikes may indicate bad data, unstable learning rates, overflow, or distributed-system faults.

A smooth loss curve does not prove the model learned the desired behavior. Pair it with downstream and safety evaluations.

## Related Guides

- [Backpropagation](backpropagation.md)
- [Pretraining](pretraining.md)
- [Supervised Fine-Tuning](supervised-fine-tuning.md)
