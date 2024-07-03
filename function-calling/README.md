# Function Calling

This is set up to reproduct results for local function calling models.

## Python environment

```bash
$ python3 -m venv venv
$ source venv/bin/activate
```

## Llama cpp python openai compatible server

```bash
$ CMAKE_ARGS="-DLLAMA_METAL=on" pip install -r requirements.txt --force-reinstall --upgrade --no-cache-dir
```

## Download models

```bash
$ huggingface-cli download <path/to/repo or models>
```

## Download v1 models

```bash
$ huggingface-cli download meetkai/functionary-7b-v1.4-GGUF --exclude '*gguf'
$ huggingface-cli download meetkai/functionary-7b-v1.4-GGUF functionary-7b-v1.4.q4_0.gguf
```

## Download v2.1 models

```bash
$ huggingface-cli download meetkai/functionary-7b-v2.1-GGUF --exclude '*gguf'
$ huggingface-cli download meetkai/functionary-7b-v2.1-GGUF functionary-7b-v2.1.q4_0.gguf
```

## Run llama-cpp-python

```bash
$ CONFIG_FILE=models.json python3 -m llama_cpp.server
```

## Findings

The v1 and v2 models appear to work fine on a basic weather function.

The v2.5 models do not yet work and should be fixed by https://github.com/abetlen/llama-cpp-python/pull/1509
