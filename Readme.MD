# ACE-Step: AI Music Generation Powerhouse in Colab

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1ka765IfuRXPDjFkHkMIz90cdd6wQGWLJ#scrollTo=QLZb3UQuV59v)
*(Please replace `github.com/Reysajju/ACE-Step/blob/main/ACE-Step-Music-Generation.ipynb` with the actual link to your Colab notebook if you create one in your repository. Otherwise, users can copy the commands below into a new Colab notebook.)*

This repository provides guidance and commands for running the [ACE-Step](https://github.com/ace-step/ACE-Step) model to generate high-quality music using Google Colab. ACE-Step is a novel open-source foundation model for music generation.

## Features of ACE-Step

*   **High-Quality Music Generation:** Creates coherent and rich musical pieces.
*   **Fast Inference:** Synthesizes music rapidly (e.g., up to 4 minutes of music in ~20 seconds on an A100 GPU).
*   **Diverse Styles & Genres:** Supports various music styles and genres.
*   **Multiple Languages:** Can generate music with lyrics in several languages. [1]
*   **Controllability:** Offers features like lyric editing, variations, repainting, and potentially voice cloning. [1]
*   **Applications:** Lyric2Vocal, Text2Samples, and upcoming features like RapMachine and StemGen. [1]
*   **Audio to Audio:** Supports audio inputs for tasks like remixing or style transfer (as indicated by "Audio2Audio Demo support" in their updates). [1]
*   **Colab Ready:** Easily run with a free GPU in Google Colab using the commands below.
*   **Memory Optimized:** Updates have focused on reducing VRAM usage, making it more accessible. [1]

## Prerequisites for Running (General)

*   **For Colab:** A Google Account and a browser.
*   **For Local Setup (Advanced Users - refer to official ACE-Step docs for full details):**
    *   **Python:** Version 3.10 or later is recommended by ACE-Step.
    *   **Git:** For cloning the official ACE-Step repository.
    *   **NVIDIA GPU:** A CUDA-enabled GPU is generally required for good performance. ACE-Step has been optimized for lower VRAM (e.g., 8GB target).
    *   **CUDA Toolkit & cuDNN:** Appropriate NVIDIA drivers and libraries.
    *   **Disk Space:** For Python, dependencies, and the ACE-Step model.

## Setup & Usage in Google Colab (Recommended)

1.  **Open a Google Colab Notebook:**
    *   You can click the "Open In Colab" badge above if you've set up a notebook in this repository.
    *   Alternatively, go to [colab.research.google.com](https://colab.research.google.com) and create a new notebook.

2.  **Set GPU Runtime:**
    *   In Colab, go to "Runtime" -> "Change runtime type".
    *   Select "GPU" from the "Hardware accelerator" dropdown and click "Save".

3.  **Run the following commands in a code cell:**

    ```python
    # 1. Clone the Official ACE-Step Repository
    !git clone https://github.com/ace-step/ACE-Step.git

    # 2. Navigate into the project directory
    %cd ACE-Step

    # 3. Install Dependencies
    # This installs ACE-Step and its core dependencies in editable mode.
    print("Installing dependencies...")
    !pip install -e .
    print("Dependencies installed.")

    # 4. Run the ACE-Step Gradio Interface
    print("Starting ACE-Step Gradio interface...")
    # --share true : Creates a public Gradio link to access the UI.
    # --bf16 true : Uses bfloat16 precision for faster inference.
    # --cpu_offload true : Offloads model weights to CPU to save GPU VRAM.
    # --overlapped_decode true : Speeds up inference with overlapped decoding.
    # --torch_compile true : Optimizes the model with torch.compile() (works on Linux/Colab).
    !acestep --port 7865 --share true --bf16 true --cpu_offload true --overlapped_decode true --torch_compile true
    ```

4.  **Access the ACE-Step Interface:**
    *   After the last command finishes, look for a public URL in the output (e.g., `Running on public URL: https://xxxxxx.gradio.live`).
    *   Open this URL in your browser to access the ACE-Step Gradio interface. You can then input text, lyrics, upload audio (for audio-to-audio features), and generate music.

## Customization (within the ACE-Step Gradio UI)

Once the Gradio interface is running, you can typically customize:

*   **Input Mode:** Text-to-Music, Audio-to-Audio (look for upload options in tabs like "Edit" or "Repainting" or a dedicated Audio2Audio tab).
*   **Tags/Description:** Describe the genre, mood, instruments, etc.
*   **Lyrics:** Input lyrics with structure tags like `[verse]`, `[chorus]`. [1]
*   **Audio Duration:** Set the length of the music to be generated. [1]
*   **Settings:**
    *   **Basic Settings:** Inference steps, guidance scale, seeds. [1]
    *   **Advanced Settings:** Scheduler type, CFG type, etc. [1]
*   **Specific Tasks:** Use dedicated tabs or modes for "Retake," "Repainting," "Edit," or "Extend" functionalities if available. [1]

## Troubleshooting Common Colab Issues

*   **"No GPU backend selected":** Ensure you've set the runtime to GPU (see Step 2).
*   **"ModuleNotFoundError":** Double-check that `!pip install -e .` completed successfully without errors.
*   **"CUDA Out of Memory":**
    *   The flags `--cpu_offload true` and `--bf16 true` are included to help mitigate this.
    *   Try generating shorter audio clips.
    *   Restart the Colab runtime ("Runtime" -> "Disconnect and delete runtime") and try again. Sometimes Colab assigns GPUs with less available memory.
*   **For ACE-Step specific issues:** Refer to the [official ACE-Step GitHub Issues](https://github.com/ace-step/ACE-Step/issues).

## Official ACE-Step Resources

*   **GitHub Repository:** [https://github.com/ace-step/ACE-Step](https://github.com/ace-step/ACE-Step)
*   **Project Page:** [https://ace-step.github.io/](https://ace-step.github.io/)
*   **Hugging Face:** Check their project page for links to models or spaces.
*   **Discord:** They have a Discord server for community discussion (link usually on their GitHub).

## License

This informational `README.md` and any associated Colab notebook in *this* repository can be considered under the [MIT License](LICENSE) (if you add one).
The ACE-Step project itself is licensed under the **Apache License 2.0**. Please consult their official repository for full details and adhere to their licensing terms when using their software.

---

*Keywords for search engines: ACE-Step, AI Music Generation, Text to Music, Audio to Audio, Music AI, Generative Music, Google Colab, Python, Machine Learning, Open Source Music.*
