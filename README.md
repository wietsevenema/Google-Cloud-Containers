# 🤗 Hugging Face Deep Learning Containers for Google Cloud

<img alt="Hugging Face x Google Cloud" src="https://huggingface.co/datasets/huggingface/documentation-images/resolve/main/google-cloud/thumbnail.png" />

[Hugging Face Deep Learning Containers for Google Cloud](https://cloud.google.com/deep-learning-containers/docs/choosing-container#hugging-face) are a set of Docker images for training and deploying Transformers, Sentence Transformers, and Diffusers models on Google Cloud Vertex AI, Google Kubernetes Engine (GKE), and Google Cloud Run.

The [Google-Cloud-Containers](https://github.com/huggingface/Google-Cloud-Containers/tree/main) repository contains the container files for building Hugging Face-specific Deep Learning Containers (DLCs), examples on how to train and deploy models on Google Cloud. The containers are publicly maintained, updated and released periodically by Hugging Face and the Google Cloud Team and available for all Google Cloud Customers within the [Google Cloud's Artifact Registry](https://cloud.google.com/deep-learning-containers/docs/choosing-container#hugging-face). For each supported combination of use-case (training, inference), accelerator type (CPU, GPU, TPU), and framework (PyTorch, TGI, TEI) containers are created. Those include:

- Training
  - [PyTorch](./containers/pytorch/training/README.md)
    - GPU
    - TPU (soon)
- Inference
  - [PyTorch](./containers/pytorch/inference/README.md)
    - CPU
    - GPU
    - TPU (soon)
  - [Text Generation Inference](./containers/tgi/README.md)
    - GPU
    - TPU (soon)
  - [Text Embeddings Inference](./containers/tei/README.md)
    - CPU
    - GPU

## Published Containers

| Container URI                                                                                                                     | Path                                                                                                                                               | Framework | Type      | Accelerator |
| --------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- | --------- | --------- | ----------- |
| us-docker.pkg.dev/deeplearning-platform-release/gcr.io/huggingface-text-generation-inference-cu121.2-2.ubuntu2204.py310           | [text-generation-inference-gpu.2.2.0](./containers/tgi/gpu/2.2.0/Dockerfile)                                                                       | TGI       | Inference | GPU         |
| us-docker.pkg.dev/deeplearning-platform-release/gcr.io/huggingface-text-embeddings-inference-cu122.1-4.ubuntu2204                 | [text-embeddings-inference-gpu.1.4.0](./containers/tei/gpu/1.4.0/Dockerfile)                                                                       | TEI       | Inference | GPU         |
| us-docker.pkg.dev/deeplearning-platform-release/gcr.io/huggingface-text-embeddings-inference-cpu.1-4                              | [text-embeddings-inference-cpu.1.4.0](./containers/tei/cpu/1.4.0/Dockerfile)                                                                       | TEI       | Inference | CPU         |
| us-docker.pkg.dev/deeplearning-platform-release/gcr.io/huggingface-pytorch-training-cu121.2-3.transformers.4-42.ubuntu2204.py310  | [huggingface-pytorch-training-gpu.2.3.0.transformers.4.42.3.py310](./containers/pytorch/training/gpu/2.3.0/transformers/4.42.3/py310/Dockerfile)   | PyTorch   | Training  | GPU         |
| us-docker.pkg.dev/deeplearning-platform-release/gcr.io/huggingface-pytorch-inference-cu121.2-2.transformers.4-44.ubuntu2204.py311 | [huggingface-pytorch-inference-gpu.2.2.2.transformers.4.44.0.py311](./containers/pytorch/inference/gpu/2.2.2/transformers/4.44.0/py311/Dockerfile) | PyTorch   | Inference | GPU         |
| us-docker.pkg.dev/deeplearning-platform-release/gcr.io/huggingface-pytorch-inference-cpu.2-2.transformers.4-44.ubuntu2204.py311   | [huggingface-pytorch-inference-cpu.2.2.2.transformers.4.44.0.py311](./containers/pytorch/inference/cpu/2.2.2/transformers/4.44.0/py311/Dockerfile) | PyTorch   | Inference | CPU         |

> [!NOTE]
> The listing above only contains the latest version of each of the Hugging Face DLCs, the full listing of the available published containers in Google Cloud can be found either in the [Deep Learning Containers Documentation](https://cloud.google.com/deep-learning-containers/docs/choosing-container#hugging-face), in the [Google Cloud Artifact Registry](https://console.cloud.google.com/artifacts/docker/deeplearning-platform-release/us/gcr.io) or via the `gcloud container images list --repository="us-docker.pkg.dev/deeplearning-platform-release/gcr.io" | grep "huggingface-"` command.

## Examples

The [`examples`](./examples) directory contains examples for using the containers on different scenarios, and digging deeper on some of the features of the containers offered within Google Cloud.

### Training Examples

| Service   | Example                                                                                                                                    | Title                                                                       |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------- |
| GKE       | [examples/gke/trl-full-fine-tuning](./examples/gke/trl-full-fine-tuning)                                                                   | Fine-tune Gemma 2B with PyTorch Training DLC using SFT on GKE               |
| GKE       | [examples/gke/trl-lora-fine-tuning](./examples/gke/trl-lora-fine-tuning)                                                                   | Fine-tune Mistral 7B v0.3 with PyTorch Training DLC using SFT + LoRA on GKE |
| Vertex AI | [examples/vertex-ai/notebooks/trl-full-sft-fine-tuning-on-vertex-ai](./examples/vertex-ai/notebooks/trl-full-sft-fine-tuning-on-vertex-ai) | Fine-tune Mistral 7B v0.3 with PyTorch Training DLC using SFT on Vertex AI  |
| Vertex AI | [examples/vertex-ai/notebooks/trl-lora-sft-fine-tuning-on-vertex-ai](./examples/vertex-ai/notebooks/trl-lora-sft-fine-tuning-on-vertex-ai) | Fine-tune Gemma 2B with PyTorch Training DLC using SFT + LoRA on Vertex AI  |

### Inference Examples


| Service   | Example                                                                                                                   | Description                                                                                                                                     |
| --------- | ------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| GKE       | [tgi-deployment](./examples/gke/tgi-deployment)                                                                           | Deploying Llama3 8B with Text Generation Inference (TGI) on GKE.                                                                                |
| GKE       | [tgi-from-gcs-deployment](./examples/gke/tgi-from-gcs-deployment)                                                         | Deploying Qwen2 7B Instruct with Text Generation Inference (TGI) from a GCS Bucket on GKE.                                                      |
| GKE       | [tei-deployment](./examples/gke/tei-deployment)                                                                           | Deploying Snowflake's Arctic Embed (M) with Text Embeddings Inference (TEI) on GKE.                                                             |
| GKE       | [tei-from-gcs-deployment](./examples/gke/tei-from-gcs-deployment)                                                         | Deploying BGE Base v1.5 (English) with Text Embeddings Inference (TEI) from a GCS Bucket on GKE.                                                |
| Vertex AI | [deploy-bert-on-vertex-ai](./examples/vertex-ai/notebooks/deploy-bert-on-vertex-ai)                                       | Deploying a BERT model for a text classification task using `huggingface-inference-toolkit` for a Custom Prediction Routine (CPR) on Vertex AI. |
| Vertex AI | [deploy-embedding-on-vertex-ai](./examples/vertex-ai/notebooks/deploy-embedding-on-vertex-ai)                             | Deploying an embedding model with Text Embeddings Inference (TEI) on Vertex AI.                                                                 |
| Vertex AI | [deploy-gemma-on-vertex-ai](./examples/vertex-ai/notebooks/deploy-gemma-on-vertex-ai)                                     | Deploying Gemma 7B Instruct with Text Generation Inference (TGI) on Vertex AI.                                                                  |
| Vertex AI | [deploy-gemma-from-gcs-on-vertex-ai](./examples/vertex-ai/notebooks/deploy-gemma-from-gcs-on-vertex-ai)                   | Deploying Gemma 7B Instruct with Text Generation Inference (TGI) from a GCS Bucket on Vertex AI.                                                |
| Vertex AI | [deploy-flux-on-vertex-ai](./examples/vertex-ai/notebooks/deploy-flux-on-vertex-ai)                                       | Deploying FLUX with Hugging Face PyTorch DLCs for Inference on Vertex AI.                                                                       |
| Vertex AI | [deploy-llama-3-1-405b-on-vertex-ai](./examples/vertex-ai/notebooks/deploy-llama-405b-on-vertex-ai/vertex-notebook.ipynb) | Deploying Meta Llama 3.1 405B in FP8 with Hugging Face DLC for TGI on Vertex AI.                                                                |
| Cloud Run | [tgi-deployment](./examples/cloud-run/tgi-deployment/README.md)                                                           | Deploying Meta Llama 3.1 8B with Text Generation Inference on Cloud Run.                                                                        |


### Evaluation

| Service   | Example                                                                                     | Description                                     |
| --------- | ------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| Vertex AI | [evaluate-llms-with-vertex-ai](./examples/vertex-ai/notebooks/evaluate-llms-with-vertex-ai) | Evaluating open LLMs with Vertex AI and Gemini. |
