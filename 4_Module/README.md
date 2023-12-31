# Finetuning and Prompt Engineering

## Prompting

1. Go to terminal and run:
```bash
vim .env
```
2. Copy the HF TOKEN and save:
```
TOKEN={HF TOKEN}
```
3. install requirements:
```
pip install -r requirements.txt
```
4. Go to [Prompt Engineering Notebook](../4_Module/Prompt_Engineering.ipynb)
5. Go to [QA Bot Code using ChatGPT](https://chat.openai.com/share/eb3079ba-1379-4b9a-b21c-839feb023309) for seeing how I used ChatGPT to scrape the PEFT documentation using `scrapy` and `BeautifulSoap`, chunk it, embed the chunks using `sentence-transformers`, create index using `hnswlib` and loading the search index and utils for embedding user query.

## Finetuning StarCoder on your private codebase to get personal co-pilot

### Dataset Generation
Go to [Dataset Generation](../personal_copilot/dataset_generation/) folder to seee how to create dataset from internal codebase for training your own co-pilot on internal codebase.

### Training

1. Install git lfs
```bash
apt-get update
apt-get install git-lfs
git lfs install
```
2. Install flash attention and common requirements
```
MAX_JOBS=8 pip install flash-attn --no-build-isolation
git clone https://github.com/pacman100/DHS-LLM-Workshop.git
cd DHS-LLM-Workshop.git
pip install -r requirements.txt
```
3. Go to [personal_copilot](../personal_copilot/training/) and install specific requirements. Also, login into HF hub via `huggingface-cli login`
```
pip install -r requirements.txt
huggingface-cli login
wandb login --relogin
```
4. Go to [train.py](../personal_copilot/training/train.py) for the training code using 🤗 Accelerate and 🤗 Transformers Trainer.  
5. Go to [run_deepspeed.sh](../personal_copilot/training/run_deepspeed.sh) to fully finetune `starcoderbase-3b` model with ZeRO Stage-3 and CPU offloading.
6. Infere using the trained model in this notebook [Full Finetuned Personal Co-Pilot](../4_Module/Full%20Finetuned%20Personal%20Co-Pilot.ipynb).
7. Go to [run_fsdp.sh](../personal_copilot/training/run_fsdp.sh) to fully finetune `starcoderbase-3b` model with FSDP when atleast 4 GPUs are available.