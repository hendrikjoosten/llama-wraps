# llama-wraps

## setup

https://replicate.com/blog/run-llama-locally

https://github.com/ggerganov/llama.cpp


```
#!/bin/bash

# Clone llama.cpp
git clone https://github.com/ggerganov/llama.cpp.git
cd llama.cpp

# Build it. `LLAMA_METAL=1` allows the computation to be executed on the GPU
LLAMA_METAL=1 make

# Download model
export MODEL=llama-2-13b-chat.ggmlv3.q4_0.bin
if [ ! -f models/${MODEL} ]; then
    curl -L "https://huggingface.co/TheBloke/Llama-2-13B-chat-GGML/resolve/main/${MODEL}" -o models/${MODEL}
fi

# Set prompt
PROMPT="Hello! How are you?"

# Run in interactive mode
./main -m ./models/llama-2-13b-chat.ggmlv3.q4_0.bin \
  --color \
  --ctx_size 2048 \
  -n -1 \
  -ins -b 256 \
  --top_k 10000 \
  --temp 0.2 \
  --repeat_penalty 1.1 \
  -t 8
  ```
  

https://replicate.com/a16z-infra/llama-2-13b-chat


## re imp in cpp

Description
The main goal of llama.cpp is to run the LLaMA model using 4-bit integer quantization on a MacBook

Plain C/C++ implementation without dependencies
Apple silicon first-class citizen - optimized via ARM NEON, Accelerate and Metal frameworks
AVX, AVX2 and AVX512 support for x86 architectures
Mixed F16 / F32 precision
4-bit, 5-bit and 8-bit integer quantization support
Supports OpenBLAS/Apple BLAS/ARM Performance Lib/ATLAS/BLIS/Intel MKL/NVHPC/ACML/SCSL/SGIMATH and more in BLAS
cuBLAS and CLBlast support


https://huggingface.co/blog/4bit-transformers-bitsandbytes


### python to cpp wrappped in python again 
https://github.com/abetlen/llama-cpp-python