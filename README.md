# Image Classification — Looksee project

This repository packages the **Looksee** project, an image-understanding web application. “Image-Classification” is the repository name; the source application remains Looksee and is described honestly as the existing project, not as a newly developed classifier.

## Download the complete source

Download [`Looksee_VS_Code_Project.zip`](Looksee_VS_Code_Project.zip) from this repository, extract it, and open the extracted `Looksee_VS_Code_Project` folder in Visual Studio Code. Inside, `DOWNLOAD_AND_RUN_IN_VSCODE.md` contains detailed, step-by-step instructions for Windows, macOS and Linux, setup prerequisites, private API-key configuration, startup commands and troubleshooting. `README.md` provides the same core run instructions.

## What’s included

- React + Vite frontend.
- Python + FastAPI backend.
- OpenRouter-powered vision-language requests, using a privately configured key.
- Safe `.env.example` templates; no real key is included.
- Product requirements, deployment configuration and optional Google Colab notebook.

## About this project

Looksee requests AI-generated descriptions of image content and suggestions about visible components. It does not train a new model, guarantee recognition accuracy, establish that a part is compatible, or diagnose equipment. Any output should be checked independently before use. The included source and guide document the project and known limits.

## Quick start

See [`DOWNLOAD_AND_RUN_IN_VSCODE.md`](DOWNLOAD_AND_RUN_IN_VSCODE.md) in this repository, or inside the downloaded source ZIP. Live image analysis requires your own OpenRouter API key in the private file `backend/.env`; do not commit or share that file. Provider requests may use your account’s quota.

## Share and attribution

This is the Looksee project source packaged under the public repository name **Image-Classification**. Use an accurate description and attribution when you share, submit or adapt this work. Follow applicable course and academic-integrity requirements. No license is specified, so do not assume this upload grants rights that were not otherwise provided.
