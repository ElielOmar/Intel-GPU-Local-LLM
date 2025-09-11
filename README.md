# Intel-GPU-Local-LLM
Until there is better support for the new Intel ARC GPU line. Running local LLMs is seemingly impossible without accelerating the GPU, using Intel's oneAPI toolkit we can achieve a much smoother experience. 
This repo is a guide + setup resource for anyone who wants to run local large language models (LLMs) on machines with Intel GPUs (like Arc or Core Ultra iGPUs).

Most AI/LLM tutorials are built for NVIDIA CUDA, but Intel GPUs can also accelerate models using oneAPI and SYCL. This repo shows you how to:

Install and configure Intel oneAPI Toolkit on Windows

Set up Ollama to run LLMs locally on Intel Arc / Core Ultra

Configure Anaconda/Miniconda for Python + AI libraries

Verify that your Intel GPU is actually being used (not just CPU)

🔧 Requirements

Windows 11 (recommended)

Intel Arc GPU or Core Ultra CPU with integrated GPU

Intel oneAPI Base Toolkit

Ollama (Windows build)

Conda / Python 3.10+

