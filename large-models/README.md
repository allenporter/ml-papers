# Large Models

This contains notes related to learnings about large models.

## Reading Collection

- [Zephyr](https://arxiv.org/pdf/2310.16944.pdf)
  - Aligned Mistral 7B
  - Paper talks about distilled fine tuning and different eval approaches, such
    as using gpt-4 to evaluate responses.

- [Mistral 7B](https://arxiv.org/pdf/2310.06825.pdf) - Mistral.ai
  - Outperforms LLama 2 13B on everything
  - Outperforms LLama 1 34B on code, reasoning, etc.
  - *Mistral 7B – Instruct* surpasses *Llama 2 13B - Chat*
  - GGUF:
    - https://huggingface.co/TheBloke/Mistral-7B-v0.1-GGUF
    - https://huggingface.co/TheBloke/Mistral-7B-Instruct-v0.1-GGUF

- [LLama2](https://arxiv.org/pdf/2307.09288.pdf) - Meta
  - 7B and 70B models, and LLama Chat
  - GGUF
    - https://huggingface.co/TheBloke/Llama-2-7B-GGUF
    - https://huggingface.co/TheBloke/Llama-2-7B-Chat-GGUF

- [LLama](https://arxiv.org/pdf/2302.13971.pdf) - Meta
  - Collection of models from 7B to 65B
  - LLama 13B out performs GPT-3 (175B on most benchmarks
  - LLaMA65B is competitive with the best models, Chinchilla-70B and PaLM-540B
  - Only trained on public data.

- [PaLM](https://arxiv.org/pdf/2204.02311.pdf) - Google Research
  - 540 model. The paper seems to be all about scaled training via [Pathways](https://arxiv.org/pdf/2203.12533.pdf).
  - The pathways paper talks about how we see more and more fine tuning based on a single large model which is an opportunity for utilization improvements


## Performance

- https://github.com/unslothai/unsloth - 80% faster 50% less memory local QLoRA finetuning
- https://github.com/pytorch-labs/gpt-fast - Simple and efficient pytorch-native transformer text generation.

## llama.cpp


Using a mac m1 for playing around with models, using GGUF format files.
From https://lastmileai.dev/workbooks/clkbifegg001jpheon6d2s4m8

Using any of the above gguf files, you can run the model:

```
cd llama.cpp
LLAMA_METAL=1 make
./main -m ./models/mistral-7b-v0.1.Q4_K_M.gguf -n 1024 -ngl 1 -p "Give me 5 things to do in NYC"
```

Note that some of the instruction tuned models have specific prompts.

## python bindings

```
$ CMAKE_ARGS="-DLLAMA_METAL=on" pip install llama_cpp_python==0.2.19 --force-reinstall --upgrade --no-cache-dir
$ python3 -m llama_cpp.server --model ./models/mistral-7b-instruct-v0.1.Q4_K_M.gguf --n_gpu_layers 1
```
