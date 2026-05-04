---
tags: [concept, nvidia, deployment, inference]
exam: NCA-GENL
domain: Deployment and Optimization
---

# Triton Inference Server

Open-source inference server for serving AI models at scale. Also called NVIDIA Dynamo Triton.

## Supported Model Formats

TensorRT, ONNX, PyTorch TorchScript, TensorFlow SavedModel

## Key Features

| Feature | Description |
|---------|-------------|
| **Dynamic batching** | Auto-combines multiple inference requests into one batch before GPU execution; improves throughput without changing client code |
| **Concurrent model execution** | Multiple model instances run simultaneously |
| **Model ensemble** | Chain multiple models in a pipeline |
| **Multi-format support** | Serves TensorRT, ONNX, PyTorch, TensorFlow models |
| **gRPC and HTTP endpoints** | Standard APIs for client integration |

## Dynamic Batching (Detail)

- Server merges multiple incoming requests into one batch dynamically
- Sends the combined batch to the model for a single GPU execution
- Result: higher throughput per GPU without client-side changes
- Critical for production LLM serving where many users send concurrent requests

## Relationship to TensorRT

- TensorRT **optimizes** a model (layer fusion, quantization, kernel tuning) and produces an engine
- Triton **serves** that engine (and others) at scale with batching and concurrency

## Related

- [[NVIDIA Ecosystem]]
- [[Quantization]]
- [[TensorRT-LLM]]
