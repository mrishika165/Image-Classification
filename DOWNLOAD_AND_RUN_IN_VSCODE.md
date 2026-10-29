# Download Looksee and run it in VS Code

The GitHub repository is named **Image-Classification**. The application inside it is the existing **Looksee** project; the repository name does not mean the code has been replaced with a different project. The app uses React + Vite in its frontend and FastAPI in its backend.

## You’ll need

- A computer with internet access.
- Visual Studio Code: https://code.visualstudio.com/
- Python 3.10 or newer: https://www.python.org/downloads/ (on Windows, enable **Add Python to PATH** in the installer).
- Node.js LTS, which includes npm: https://nodejs.org/
- Your own OpenRouter API key for live image analysis: https://openrouter.ai/keys. Keep it private. Provider access, model availability and usage limits can change; model calls may consume your account’s quota.

> Opening or previewing the website may work without an API key; actually analysing an image requires the backend’s private OpenRouter key.

## 1. Download the source from GitHub

1. Open the repository: https://github.com/mrishika165/Image-Classification
2. Select the green **Code** button.
3. Select **Download ZIP**.
4. Find the downloaded ZIP on your computer and extract it. On Windows, right-click the ZIP and choose **Extract All…**.
5. Keep the extracted project in a folder you can find again, such as Documents or your Desktop. Do not edit files inside the compressed ZIP itself.

## 2. Open the extracted folder in VS Code

1. Start VS Code.
2. Select **File → Open Folder…**.
3. Choose the extracted `Image-Classification` folder. The correct folder is the one that directly contains `backend`, `frontend`, `README.md`, and this guide.
4. If VS Code asks whether you trust the authors of the files, choose based on whether you trust this project source.
5. Select **Terminal → New Terminal**. The commands below use PowerShell on Windows; on macOS or Linux, use a terminal and the commands in the corresponding section.

## 3. Configure the backend key (do this once)

Keep the API key in the backend only. Never paste it into this guide, `frontend`, GitHub, a screenshot, or a message.

In the first VS Code terminal, run these commands from the project’s top-level folder:

```powershell
cd backend
Copy-Item .env.example .env
```

If the command reports that `backend/.env` already exists, do not overwrite it; open it and check whether it already has your own key.

1. In the VS Code Explorer, open `backend/.env`.
2. Replace `replace-with-your-key` on the `OPENROUTER_API_KEY=` line with your own OpenRouter key.
3. Save the file. Do not add spaces around `=` and do not include quotes unless the key’s provider format explicitly requires them.
4. Leave the `OPENROUTER_MODEL` and `CORS_ORIGINS` example settings in place initially. You can change the model later to one supported by your OpenRouter account.
5. Confirm `backend/.env` is not listed as a tracked file. This project’s `.gitignore` excludes real `.env` files.

Example structure only (the placeholder is not a working key):

```text
OPENROUTER_API_KEY=replace-with-your-key
OPENROUTER_MODEL=nvidia/nemotron-3-nano-omni-30b-a3b-reasoning:free
CORS_ORIGINS=http://localhost:5173
```

## 4. Install and start the backend (Terminal 1)

If you are still in the `backend` directory from step 3, run:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m uvicorn app.main:app --reload --port 8000
```

If PowerShell blocks activating the virtual environment, you can skip the activation command and use the local interpreter explicitly for installation and starting:

```powershell
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m uvicorn app.main:app --reload --port 8000
```

Keep Terminal 1 running. When it says Uvicorn is running, check the backend health page at http://localhost:8000/health. It should show a JSON response with a status such as `ok`.

## 5. Install and start the website (Terminal 2)

In VS Code, select **Terminal → New Terminal** again. From the project’s top-level folder, run:

```powershell
cd frontend
npm install
npm run dev
```

Keep Terminal 2 running too. Open the local address printed by Vite, normally http://localhost:5173.

## 6. Test the app

1. On the website, choose **General analysis** or **Identify parts**.
2. Select a JPG, PNG or WebP image no larger than 10 MB.
3. Start analysis. For this step, both terminals need to remain running and the backend needs your private OpenRouter API key.
4. Treat names and descriptions as AI-generated suggestions. Looksee does not confirm hidden parts, diagnose faults, guarantee compatibility, or replace a qualified technician.

## 7. Stop the local servers

When finished, return to each terminal and press **Ctrl+C**. You can restart them later by repeating step 4 in the backend terminal and step 5 in the frontend terminal; you do not need to reinstall dependencies every time.

## macOS or Linux

Use a terminal opened in the extracted project root. Set up and run the backend in Terminal 1:

```bash
cd backend
cp .env.example .env       # Run once; edit backend/.env to add your own key.
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m uvicorn app.main:app --reload --port 8000
```

Open a second terminal in the project root and run the frontend:

```bash
cd frontend
npm install
npm run dev
```

Open http://localhost:5173. Leave both terminals open while testing, then stop both processes with **Ctrl+C**.

## Optional: Windows one-click launcher

On Windows, the root folder also contains `start-image-classifier.cmd`. Double-clicking it creates the local Python environment, installs missing dependencies, starts the backend and frontend in separate windows, and opens the website. You must first create `backend/.env` from `backend/.env.example` and add your own API key. Keep both server windows open until you finish testing.

## Common problems

- **`python` is not recognised:** reinstall Python with **Add Python to PATH** selected; close and reopen VS Code.
- **`npm` is not recognised:** install Node.js LTS and reopen VS Code.
- **`ModuleNotFoundError` or missing packages:** make sure the backend virtual environment is active and install again with `python -m pip install -r requirements.txt` from `backend`.
- **The page does not open:** verify `npm run dev` is still running in `frontend` and open the exact local URL printed by Vite.
- **Cannot connect to the API or a CORS error:** verify Terminal 1 is running on port 8000 and `backend/.env` has `CORS_ORIGINS=http://localhost:5173`. Restart the backend after changing `.env`.
- **Missing/rejected key, model error or rate limit:** check your own OpenRouter account and key, and select a model available to your account. Provider quotas and model availability can change.
- **A browser upload does not return analysis:** check both terminal windows for error messages. Do not publish or send your private API key in an error report.

## What's in the repository?

- `frontend/` — React + Vite web app.
- `backend/` — FastAPI service and image-analysis request handling.
- `backend/.env.example` — safe environment-variable template. It contains a placeholder, not an API key.
- `frontend/.env.example` — optional frontend URL template for the local backend.
- `start-image-classifier.cmd` — optional Windows starter.
- `PRD.md` — product requirements document.
- `DEPLOYMENT.md` and `render.yaml` — hosting configuration and notes.
- `looksee_deep_learning_colab.ipynb` — optional Google Colab example; prompts for a key at runtime.

## Source, reuse and attribution

The repository name is **Image-Classification**; the source project and running application remain **Looksee**. The name change is a repository-label change only. It does not transform Looksee into a separately developed project. If you use or present this work, describe its existing origins and contributions accurately and follow your course’s academic-integrity rules. No claim is made here that Looksee was newly developed, trained on a new dataset, or independently evaluated as part of this upload.

## Privacy and sharing

The public repository intentionally contains no personal OpenRouter key, local `.env` file, Python virtual environment or installed `node_modules`. Your computer sends an uploaded image to the configured OpenRouter service when you request analysis. Review that provider’s current terms and do not upload private or sensitive images without appropriate permission.
