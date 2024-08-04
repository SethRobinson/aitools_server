# AI Tools Server (made to be used with Seth's AI Tools front-end)

This is a forked version of the [AUTOMATIC1111/stable-diffusion-webui](https://github.com/AUTOMATIC1111/stable-diffusion-webui) project - basically the same thing with some additional API features like background removal.  Setup is the same, so check their github for better docs.

### This server is designed to be used with the [Seth's AI Tools Client](https://github.com/SethRobinson/aitools_client) <-- github page that has its download and screenshots/movies ###

Or, don't use my front-end client and just use its API directly:

* Here's a [Python Jupter notebook](https://github.com/SethRobinson/aitools_server/blob/master/aitools/automatic1111_api_tester_jupyter_notebook.ipynb) showing examples of how to use the standard AUTOMATIC1111 api
* Here's a [Python Jupter notebook](https://github.com/SethRobinson/aitools_server/blob/master/aitools/aitools_extensions_api_tester_jupyter_notebook.ipynb) showing how to use the extended features available in my forked server (AI background removal, AI subject masking, etc)

**Note:**  This repository was deleted and replaced with the [AUTOMATIC1111/stable-diffusion-webui](github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Install-and-Run-on-AMD-GPUs) fork Sept 19th 2022, specific missing features that I need are folded into it. Previously I had written my own custom server but that was like, too much work man

# Last update August 4th, 2024, recent changes:

* (merged with latest auto1111 stuff)
* Versioned to 0.49

## Installation and Running (modified from [stable-diffusion-webui](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki) docs)
Make sure the required [dependencies](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Dependencies) are met and follow the instructions available for both [NVidia](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Install-and-Run-on-NVidia-GPUs) (recommended) and [AMD](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Install-and-Run-on-AMD-GPUs) GPUs.


### Installation on Windows

Note:  This might not work, auto1111 has changed the setup a bit and I haven't tested it under Windows, just linux.  If that happens, check the auto1111 instructions instead, it should still apply here.

1. Install [Python 3.10.6](https://www.python.org/downloads/windows/), checking "Add Python to PATH"
2. Install [git](https://git-scm.com/download/win).
3. Download the aitools_server repository, for example by running `git clone https://github.com/SethRobinson/aitools_server.git`.
4. Place any stable diffusion checkpoint such as `sd-v1-5-inpainting.ckpt` in the `models/Stable-diffusion` directory (see [dependencies](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Dependencies) for where to get one)
5. Run `webui-user.bat` from Windows Explorer as normal, non-administrator, user.

### Installation on Linux
1. Install the dependencies:
Note:  Requires Python 3.10+ now!

```bash
# Debian-based:
sudo apt install wget git python3 python3-venv libgl1 libglib2.0-0
# Red Hat-based:
sudo dnf install wget git python3 gperftools-libs libglvnd-glx
# openSUSE-based:
sudo zypper install wget git python3 libtcmalloc4 libglvnd
# Arch-based:
sudo pacman -S wget git python3
```
2. To install in `/home/$(whoami)/aitools_server/`, run:
```bash
bash <(wget -qO- https://raw.githubusercontent.com/SethRobinson/aitools_server/master/webui.sh)
```

## Adding a necessary file (needed for Win/linux installs)

4. Place sd-v1.5-inpainting.ckpt or another stable diffusion model in models/Stable-diffusion. (see [dependencies](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Dependencies) for where to get it).
5. Run the server from shell with:
```bash
python launch.py --listen --port 7860 --api
```

(if on linux, you can do sh runserver.sh, it's an included helper script that does something similar)

## Google Colab

Don't have a strong enough GPU or want to give it a quick test run without hassle?  No problem, use this [Colab notebook](https://colab.research.google.com/drive/14FT8N_MfKNBmbPi4-xlt2YvrRzK1UN8K).  (Works fine on the free tier)

## How to update an existing install of the server to the latest version

Go to its directory (probably aitools_server) in a shell or command prompt and type:

```bash
git pull
```

## Merging with Automatic1111 manually ##

If you feel bold, you can also merge it with the latest Automatic1111 server yourself.  This CAN break things, so you probably shouldn't do this unless you really need a new feature and Seth hasn't merged the latest yet.  (not recommended unless you know how to resolve what are probably simple merge issues)

```bash
sh merge_with_automatic1111.sh
```

## Running Seth's AI Tools front-end

Verify the server works by visiting it with a browser.  You should be able to generate and paint images via the default web gradio interface. Now you're ready to use the native client.

**Note** The first time you use the server, it may appear that nothing is happening - look at the server window/shell, it's probably downloading a bunch of stuff for each new feature you use.  This only happens the first time!

* [Download the Client (Windows, ~36 MB)](https://www.rtsoft.com/files/SethsAIToolsWindows.zip) (Or get the [Unity source](https://github.com/SethRobinson/aitools_client))
    
* Unzip somewhere and run aitools_client.exe

The client should start up.  If you click "Generate", images should start being made.  By default it tries to find the server at localhost at port 7860.  If it's somewhere else, you need to click "Configure" and edit/add server info.  You can add/remove multiple servers on the fly while using the app. (all will be utilitized simultaneously by the app)

<a href="aitools/aitools_server_setup.png"><img src="aitools/aitools_server_setup.png" width=300></a>

## Using multiple GPUs on the same computer

You can run multiple instances of the server from the same install.

Start one instance: (uh, this is how for linux, not sure about Windows)

```CUDA_VISIBLE_DEVICES=0 python launch.py --listen --port 7860 --api```

Then from another shell start another specifying a different GPU and port:

```CUDA_VISIBLE_DEVICES=1 python launch.py --listen --port 7861 --api```

Then on the client, click Configure and edit in an add_server command for both servers.

## Credits for things specific to this fork
- Seth's AI Tools created by Seth A. Robinson (seth@rtsoft.com) twitter: @rtsoft - [Codedojo](https://www.codedojo.com), Seth's blog
- [Highly Accurate Dichotomous Image Segmentation](https://github.com/xuebinqin/DIS) (Xuebin Qin and Hang Dai and Xiaobin Hu and Deng-Ping Fan and Ling Shao and Luc Van Gool)

## Credits for Automatic1111's Stable Diffusion WebUI
- The original [stable-diffusion-webui project](https://github.com/AUTOMATIC1111/stable-diffusion-webui) the server portion is forked from
- Stable Diffusion - https://github.com/CompVis/stable-diffusion, https://github.com/CompVis/taming-transformers
- k-diffusion - https://github.com/crowsonkb/k-diffusion.git
- Spandrel - https://github.com/chaiNNer-org/spandrel implementing
  - GFPGAN - https://github.com/TencentARC/GFPGAN.git
  - CodeFormer - https://github.com/sczhou/CodeFormer
  - ESRGAN - https://github.com/xinntao/ESRGAN
  - SwinIR - https://github.com/JingyunLiang/SwinIR
  - Swin2SR - https://github.com/mv-lab/swin2sr
- LDSR - https://github.com/Hafiidz/latent-diffusion
- MiDaS - https://github.com/isl-org/MiDaS
- Ideas for optimizations - https://github.com/basujindal/stable-diffusion
- Cross Attention layer optimization - Doggettx - https://github.com/Doggettx/stable-diffusion, original idea for prompt editing.
- Cross Attention layer optimization - InvokeAI, lstein - https://github.com/invoke-ai/InvokeAI (originally http://github.com/lstein/stable-diffusion)
- Sub-quadratic Cross Attention layer optimization - Alex Birch (https://github.com/Birch-san/diffusers/pull/1), Amin Rezaei (https://github.com/AminRezaei0x443/memory-efficient-attention)
- Textual Inversion - Rinon Gal - https://github.com/rinongal/textual_inversion (we're not using his code, but we are using his ideas).
- Idea for SD upscale - https://github.com/jquesnelle/txt2imghd
- Noise generation for outpainting mk2 - https://github.com/parlance-zz/g-diffuser-bot
- CLIP interrogator idea and borrowing some code - https://github.com/pharmapsychotic/clip-interrogator
- Idea for Composable Diffusion - https://github.com/energy-based-model/Compositional-Visual-Generation-with-Composable-Diffusion-Models-PyTorch
- xformers - https://github.com/facebookresearch/xformers
- DeepDanbooru - interrogator for anime diffusers https://github.com/KichangKim/DeepDanbooru
- Sampling in float32 precision from a float16 UNet - marunine for the idea, Birch-san for the example Diffusers implementation (https://github.com/Birch-san/diffusers-play/tree/92feee6)
- Instruct pix2pix - Tim Brooks (star), Aleksander Holynski (star), Alexei A. Efros (no star) - https://github.com/timothybrooks/instruct-pix2pix
- Security advice - RyotaK
- UniPC sampler - Wenliang Zhao - https://github.com/wl-zhao/UniPC
- TAESD - Ollin Boer Bohan - https://github.com/madebyollin/taesd
- LyCORIS - KohakuBlueleaf
- Restart sampling - lambertae - https://github.com/Newbeeer/diffusion_restart_sampling
- Hypertile - tfernd - https://github.com/tfernd/HyperTile
- Initial Gradio script - posted on 4chan by an Anonymous user. Thank you Anonymous user.
- (You)
