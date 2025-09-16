# Intel-GPU-Local-LLM
Until there is better support for the new Intel ARC GPU line. Running local LLMs is seemingly impossible without accelerating the GPU, using Intel's oneAPI toolkit we can achieve a much smoother experience. 
This repo is a guide + setup resource for anyone who wants to run local large language models (LLMs) on machines with Intel GPUs (like Arc or Core Ultra iGPUs).

Most AI/LLM tutorials are built for NVIDIA CUDA, but Intel GPUs can also accelerate models using oneAPI and SYCL. This repo shows you how to:

1. Install and configure Intel oneAPI Toolkit on Windows
2. Set up Ollama to run LLMs locally on Intel Arc / Core Ultra
3. Configure Anaconda/Miniconda for Python + AI libraries
4. Verify that your Intel GPU is actually being used (not just CPU)

##  Requirements

Windows 11 (recommended)

Intel Arc GPU or Core Ultra CPU with integrated GPU

[Ollama (Windows build)](https://ollama.com/)


### [Intel oneAPI Base Toolkit](https://www.intel.com/content/www/us/en/developer/tools/oneapi/base-toolkit-download.html)
Ollama (and most LLM runtimes) need hardware acceleration to run models efficiently.

NVIDIA GPUs use CUDA (via NVIDIA drivers), but Intel doesn’t have CUDA. Instead, they use oneAPI and SYCL for compute acceleration.

The Intel oneAPI Toolkit provides the libraries and drivers that let apps like Ollama or PyTorch actually use your Intel Arc GPU + CPU extensions (like AVX512, AMX).
Without it, your LLM would just run on CPU which is super slow.

### [Visual Studio Build Tools](https://visualstudio.microsoft.com/insiders/) 
If you want a smooth Local LLM experience, build tools are vital. 

   With Build Tools: Everything just works. You can install, run, and even customize LLM software.

   Without Build Tools: You try to install a package but it fails with errors like “Microsoft Visual C++ 14.0 or greater is required”. (Now you go and install build tools)
   
### [IPEX-LLM](https://github.com/intel/ipex-llm/releases) 
This is where the magic happens. 
Ensures that your setup isn’t just “running on CPU” but actually taking advantage of the Arc GPU + oneAPI stack.

Most LLM runtimes are optimized for NVIDIA CUDA, leaving Intel users with poor performance or CPU-only execution.
With IPEX-LLM, you get:

1. Hardware Acceleration for Intel GPUs
2. Lets your Arc GPU handle LLM inference, not just the CPU.
3. Drastically improves speed compared to CPU-only runs.
4. Lower Memory Usage with Quantization
5. You can load bigger models (like 13B or even 70B with quantization) on limited VRAM.

Example: Run llama-2-13b-int4 on an Intel Arc GPU that couldn’t handle the full-precision model.

#### Bridges the Gap with Ollama

While Ollama gives you a great runtime experience, IPEX-LLM is what enables Intel GPUs to be useful when you go deeper into Python-based workflows (fine-tuning, research, Hugging Face integration).

### Conda / Python 3.10+ (Optional but recommended) 
Ollama itself doesn’t require Conda.

But Conda is your safety net for when you start mixing Ollama + Python + Hugging Face + Intel oneAPI toolkits.

So unless you plan on doing more than just ollama you don't really need it. 


