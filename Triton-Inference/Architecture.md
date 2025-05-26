# Triton Inference Server: Architecture Overview

This document summarizes the architecture of NVIDIA Triton Inference Server, focusing on deployment structure, model management, and scalability mechanisms — from a Technical Program Manager's perspective.

---

## 🔧 Core Components

### 1. Frontend Interface
- **Protocols Supported**: HTTP / gRPC / C++ API / Python API
- **Function**: Accepts inference requests, handles client-server communication

### 2. Model Repository
- **Location**: Local filesystem or cloud (e.g., S3, GCS)
- **Structure**: Organized by model name/version (e.g. `resnet50/1/model.onnx`)
- **Auto-reload**: Triton can hot-reload updated models

### 3. Backend Runtimes
- **Supported Frameworks**:
  - TensorFlow
  - PyTorch
  - ONNX Runtime
  - TensorRT
  - Python / Custom backends
- **Function**: Execute inference based on pre-loaded model + input tensors

### 4. Scheduler / Batching Engine
- Dynamically schedules requests to optimize throughput
- Supports dynamic and static batching per model configuration

---

## 🧠 Key Architecture Features

| Feature | Description |
|--------|-------------|
| **Multi-framework Support** | Run TensorFlow, ONNX, PyTorch in parallel |
| **Model Versioning** | Serve multiple versions of the same model simultaneously |
| **Ensemble Models** | Chain multiple models together as a single logical model |
| **Metrics Export** | Prometheus-compatible monitoring |
| **GPU / CPU Runtime Flexibility** | Assign models to specific devices via config |

---

## 🧭 TPM Perspective: Why It Matters

- Helps align AI model team + infra team expectations early
- Supports **scalable deployment planning** (e.g. model A on GPU 0, model B on CPU)
- Enables **multi-model validation** across versions and platforms
- Integration-friendly with Kubernetes / Helm for MLOps pipelines

---

## 🗂️ References

- [Triton GitHub](https://github.com/triton-inference-server/server)
- [Triton Deployment Examples](https://github.com/triton-inference-server/server/tree/main/docs/examples)
- [ONNX vs TensorRT Comparison](../Deployment-Flow.md)

