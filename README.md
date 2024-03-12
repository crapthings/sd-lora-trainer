# Trainer

Code for finetuning and training LoRa modules on top of Stable Diffusion.

## Setup

1. Install Replicate 'cog':

```
sudo curl -o /usr/local/bin/cog -L "https://github.com/replicate/cog/releases/latest/download/cog_$(uname -s)_$(uname -m)"
sudo chmod +x /usr/local/bin/cog
```

2. Build the image with `sudo cog build`
3. Run a training run with `sudo sh test_train.sh`



## TODO's

Code / Cleanup:
- make a clean train.py entrypoint that can be run as a normal python command (instead of having to use cog)
- integrate PEFT (https://github.com/huggingface/peft) instead of the hacky, ad-hoc lora stuff
- Modularize the logic in train.py as much as possible, trying to minimize dev work that needs to happen when SD3 drops

Algo:
- add proper gradient accumulation so we can train with smaller bs if needed
- Improve the img captioning by swapping BLIP for cogVLM: https://github.com/THUDM/CogVLM
- Add aspect_ratio bucketing into the dataloader so we can train on non-square images (take this from https://github.com/kohya-ss/sd-scripts)
- Implement / Tryout DoRa: https://github.com/catid/dora/tree/main
- Add multi-token training
- test if textual inversion training can also happen with prodigy_optimizer
- the random initialization of the token embeddings has a relatively large impact on the final outcome, there are prob ways to reduce
this random variance, eg CLIP_similarity pretraining.
