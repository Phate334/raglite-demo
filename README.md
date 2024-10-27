# Minimal RAG Backend with Llama.cpp and Grafana

This repository provides a minimal implementation of a Retrieval-Augmented Generation (RAG) backend. It leverages llama.cpp for inference using both large language models (LLMs) and embedding models. The backend is equipped with Grafana for real-time monitoring and performance visualization. Ideal for developers seeking a lightweight and efficient RAG solution with integrated observability.

![](./grafana-screenshot.png)

## Tech stack

- llama.cpp-server
  - LLM
  - Embedding models
- LiteLLM
  - OpenAI API spec. compatible
- gemma 2 2b
  - https://huggingface.co/phate334/gemma-2-2b-it-Q4_K_M-GGUF/
- multilingual e5 large 
  - https://huggingface.co/phate334/multilingual-e5-large-gguf

Download the models and place them in the `models` directory.

## Run it

- CPU only

```bash
docker compose up -d
```

- call the API

If you installed [REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client) in VSCode, you can use the `api.http` file to test the API.

or

```bash
# chat completions api
curl --request POST \
  --url http://localhost:8000/v1/chat/completions \
  --data '{"model": "gemma-2-2b-it-q4","messages": [{"role": "system","content": "You are a helpful assistant."},{"role": "user","content": "Hi"}]}'
# embedding api
curl --request POST \
  --url http://localhost:8000/v1/embeddings \
  --data '{"model": "multilingual-e5-large-q4","input": ["test"]}'
```

## Monitor it (WIP)

```bash
docker compose --profile monitor up -d
```

Open Grafana at http://localhost:3000 and login with `admin`/`admin` by default.

## Preparing the Python environment

To prepare the Python environment for running `demo.ipynb`, follow these steps:

1. Install Python 3.10 or higher.
2. Install Poetry for dependency management. `pip install poetry`
3. Clone the repository and navigate to the project directory.
4. Run `poetry install` to install the dependencies.
