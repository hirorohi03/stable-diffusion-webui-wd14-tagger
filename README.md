<p align="center">
🌍
<strong>English</strong> |
<a href="./README_JP.md">日本語</a> |
</p>

---

<div align="center">

# Tagger for [Stable Diffusion WebUI Forge - Neo & Classic](https://github.com/Haoming02/sd-webui-forge-classic)

---

</div>

This repository is a fork based on 67372a's [stable-diffusion-webui-wd14-tagger](https://github.com/67372a/stable-diffusion-webui-wd14-tagger).<BR>

I'm sorry for creating yet another fork of Tagger.<BR>
However, this fork will help those who have been struggling because they couldn't use Tagger on Forge Neo.<P>

In this fork I have removed unused and unnecessary features that were preventing it from running on Forge Neo.<BR>
Since this fork does not use `tensorflow` (which conflicts with the version of `protobuf` required by the WebUI), I believe this fork is useful even on A1111/Forge/reForge.

## Fork changes

### Fixed

- I have fixed code that relied on Deepbooru Interrogator which is not included in Forge Neo, as well as code that was incompatible with the UI.

### Removed Features

- `tensorflow`
   - The version of `protobuf` required by `tensorflow` is not compatible with the version of `protobuf` required by the WebUI.
   - In the original tagger, `tensorflow` is installed solely for experimental features available only in `tensorflow 2.10` and for DeepDanbooruInterrogator.
- `deepdanbooru` & DeepDanbooruInterrogator
   - No one uses this anymore, right?
   - Instead, please use WaifuDiffusionInterrogator, MLDanbooruInterrogator, or Z3DInterrogator.
- `opencv_python_headless`
   - `opencv_python` and `opencv_python_headless` conflict during installation. Since `opencv_python` is pre-installed on Forge Neo, `opencv_python_headless` is not required.

After migrating from another Tagger to this one, you can remove them using `pip uninstall`, provided you are not using `tensorflow`, `deepdanbooru` or `opencv_python_headless` with other tools.

## Changelog

### 2026/5/30

- Handle missing use_cpu option in Forge Neo

### 2026/5/7

- Replace `generation_parameters_copypaste` with `infotext_utils`.
   - This is because `generation_parameters_copypaste` was removed in Forge Neo commit [e40900c](https://github.com/Haoming02/sd-webui-forge-classic/commit/e40900cd8bf7275d89dd01c534108661960f38f3) (updated May 5, 2026).

### 2026/4/20

- Added a version constraint of `<4.12` to the `opencv_python` and `opencv_contrib_python` lines in `requirements.txt`.
   - If the version of `opencv_python` or `opencv_contrib_python` is 4.12 or higher, `numpy` will be updated to 2.x, which causes issues like ControlNet errors in WebUIs using `gradio 3.x` (Forge Neo is not affected as it uses `gradio 4.x`).

---

The following is the README provided by the original repository.

---
## Fork changes
- v3 taggers added
- Z3D-E621-Convnext tagger added
- Onnxruntime dep version required by v3 taggers 

Tagger for [Automatic1111's WebUI](https://github.com/AUTOMATIC1111/stable-diffusion-webui)
---
Interrogate booru style tags for single or multiple image files using various models, such as DeepDanbooru.

[한국어를 사용하시나요? 여기에 한국어 설명서가 있습니다!](README.ko.md)

## Disclaimer
I didn't make any models, and most of the code was heavily borrowed from the [DeepDanbooru](https://github.com/KichangKim/DeepDanbooru) and MrSmillingWolf's tagger.

## Installation
1. *Extensions* -> *Install from URL* -> Enter URL of this repository -> Press *Install* button
   - or clone this repository under `extensions/`
      ```sh
      $ git clone https://github.com/picobyte/stable-diffusion-webui-wd14-tagger.git extensions/tagger
      ```

1. *(optional)* Add interrogate model
   - #### [*Waifu Diffusion 1.4 Tagger by MrSmilingWolf*](docs/what-is-wd14-tagger.md)
      Downloads automatically from the [HuggingFace repository](https://huggingface.co/SmilingWolf/wd-v1-4-vit-tagger) the first time you run it.

   - #### *DeepDanbooru*
      1. Various model files can be found below.
         - [DeepDanbooru models](https://github.com/KichangKim/DeepDanbooru/releases)
         - [e621 model by 🐾Zack🐾#1984](https://discord.gg/BDFpq9Yb7K)
            *(link contains NSFW contents!)*

      1. Move the project folder containing the model and config to `models/deepdanbooru`

      1. The file structure should look like:
         ```
         models/
         └╴deepdanbooru/
           ├╴deepdanbooru-v3-20211112-sgd-e28/
           │ ├╴project.json
           │ └╴...
           │
           ├╴deepdanbooru-v4-20200814-sgd-e30/
           │ ├╴project.json
           │ └╴...
           │
           ├╴e621-v3-20221117-sgd-e32/
           │ ├╴project.json
           │ └╴...
           │
           ...
         ```

1. Start or restart the WebUI.
   - or you can press refresh button after *Interrogator* dropdown box.
   - "You must close stable diffusion completely after installation and re-run it!"


## Model comparison
[Model comparison](docs/model-comparison.md)

## Screenshot
![Screenshot](docs/screenshot.png)

Artwork made by [hecattaart](https://vk.com/hecattaart?w=wall-89063929_3767)

## Copyright

Public domain, except borrowed parts (e.g. `dbimutils.py`)
