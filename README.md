# Simple Captioner

A minimal media captioning tool powered by **[Qwen2.5-VL-7B-Instruct](https://huggingface.co/Qwen/Qwen2.5-VL-7B-Instruct)** from Alibaba Group.

This tool uses a Gradio UI to batch process folders of **images and videos** and generate descriptive captions.

Written by [Olli S.](https://github.com/o-l-l-i)

---

![Splash image](/images/screenshot.png)

## ✨ Features

- ✅ Uses `Qwen2.5-VL-7B-Instruct` for high-quality understanding
- ✅ Caption multiple images or videos from a selected folder
- ✅ Sub-folder support
- ✅ Supports prompt customization
- ✅ "Summary Mode" and "One-Sentence Mode" options for different caption styles
- ✅ Can skip already-captioned images
- ✅ Image previews with real-time progress
- ✅ Abort long runs safely
- ✅ Runs on GPU with 8-bit quantization (via BitsAndBytes)

---

## Requirements

- Python 3.9+
- A modern NVIDIA GPU with CUDA (tested on Ampere and newer)
- ~16GB VRAM recommended for smooth operation

---

## Setup Instructions

1. **Clone the repository**:

   ```bash
   git clone https://github.com/o-l-l-i/simple-captioner.git
   cd simple-captioner

2. **Create a virtual environment (optional but recommended)**:

    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate

3. **Install the dependencies**:

    ```bash
    pip install -r requirements.txt

4. **Install Torch with GPU support**:
   - You have to install GPU compatible Torch yourself, get it from here:
   - [https://pytorch.org/get-started/locally/](https://pytorch.org/get-started/locally/)
   - Copy the "Run this Command" string from the page after selecting correct version.
     - i.e. if you have Cuda 12.6, select that option. (Windows, Pip, Python, CUDA 12.6.)

    ```bash
    pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu126

5. **Install Triton**:

    On Windows, install [woctordho's Triton fork for Windows](https://github.com/woct0rdho/triton-windows)

    ```bash
    pip install triton
    pip install triton-windows # On Windows use this

6. **Run the app**:

    ```bash
    python app.py

7. **To run this app later**:

    - When you need to return back to use this, the virtual environment (venv) needs to be activated again.
    - Use/modify the included start up scripts.

    **Windows**:
    - run_app.bat

    ```bash
    @echo off
    call venv\Scripts\activate
    python app.py
    ```

    **Linux/macOS**:
    - run_app.sh

    ```bash
    #!/bin/bash
    source venv/bin/activate
    python app.py
    ```

    Make it executable:
    ```bash
    chmod +x run_app.sh
    ```

## Model Files

When you run the app for the first time, the model (Qwen/Qwen2.5-VL-7B-Instruct) is automatically downloaded from Hugging Face. This download is cached locally, so subsequent runs are much faster and offline-compatible.

By default, Hugging Face stores downloaded models in:


```bash
Linux/macOS: ~/.cache/huggingface/

Windows: C:\Users\<YourUsername>\.cache\huggingface\
```

You can inspect, manage, or clear this cache manually, or change the location by setting the HF_HOME environment variable:


```bash
export HF_HOME=/custom/path/to/huggingface
# On Windows: set HF_HOME=E:\huggingface_cache
```

This is useful if you're working with limited disk space or want to centralize model caches across multiple projects.

---

## Video Support Note
To enable video processing, make sure qwen-vl-utils is installed.
On Linux:

```bash
pip install qwen-vl-utils[decord]==0.0.8

```

```bash
On other platforms (Windows/macOS):
pip install qwen-vl-utils
```

This will fall back to using torchvision for video loading if decord does not work, which is slower.
For better performance, [you can try to install decord from source](https://github.com/dmlc/decord)

## Usage Notes
- Place your images in a folder (recursively scanned, subfolders are supported.)
- Text files with the same name (e.g. image1.jpg → image1.txt) are created alongside the images.
- Use the “Skip already captioned” checkbox to avoid reprocessing.
- Captions can be styled with prompt modifiers or sentence-length constraints.

---

## Customization

- Prompt handling is adjustable with toggles.
- Modify the base prompt or model behavior in generate_caption() inside the code.
- Want more control over output format? Adjust the file writing or UI code.

---

## Troubleshooting

- Make sure you’re using a CUDA-compatible GPU.
- On Windows you have to install GPU compatible Torch yourself, get it from here:
  - [https://pytorch.org/get-started/locally/](https://pytorch.org/get-started/locally/)
  - Select a Torch version which matches your CUDA version.
- If VRAM usage is too high, reduce max_tokens. This is only tested on 3090 and 5090, but I did monitor the VRAM usage.

---

## Early Development Notice

This project is currently in a very early phase of development. While it aims to provide useful image and video captioning capabilities, you may encounter bugs, unexpected behavior, or incomplete features.

If you run into any issues:

- Please check the console or logs for error messages.
- Try to use supported media formats as listed.
- Feel free to report problems or request features via the project’s GitHub Issues page.

---
