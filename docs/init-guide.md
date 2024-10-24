######
# Installation Guide
######

1. Install pipx in venv then poetry
    - source:
      - https://github.com/pypa/pipx
      - https://python-poetry.org/docs/#installing-with-pipx
```bash
which pipx #check old pipx installation, uninstall if exists
cd ~/*/oGai
sudo apt update
python3 -m venv venv
source venv/bin/activate
sudo sudo apt install pipx --fix-missing
python3 -m pipx ensurepath
pipx install poetry
poetry config keyring.enabled false # disable keyring chck to avoid pending during downlaod
    # equivalent in Dockerfile:  'ENV POETRY_CONFIG_KEYRING_ENABLED=false'
 ```

 2. Rebuild poetry.lock
 ```bash
 cd ~/*/oGai
 rm -r ./poetry.lock
 poetry cache clear --all pypi
 poetry lock
 poetry install
 ```

# Charaf local run method in ollama API mode in docker 

```bash
cd /home/charafel/Git/AuvaLocalRag/private-gpt
 source venv/bin/activate
 docker stop ollama
 docker remove ollama
 docker run -d --gpus=all -v ./models:/root/.ollama -p 11434:11434 -e OLLAMA_NUM_PARALLEL=15 -e OLLAMA_MAX_LOADED_MODELS=3 --name ollama ollama/ollama
 docker exec ollama ollama pull mistral #pull locally mistral model
 PGPT_PROFILES=ollama make run 
```