# GitHub Upload Steps - MindBridge-RAG Group 16

This folder is the GitHub-safe version of the project. It does not include `backend/.env`, the Gemini API key, Python virtual environments, `node_modules`, cache folders, or the final submission zip.

## 1. Open This Folder

```powershell
cd "C:\Users\Hp\Desktop\mindbridge_rag_group16_github_ready"
```

## 2. Confirm Secrets Are Not Present

Before uploading, confirm that `backend/.env` is not inside this folder. Only `backend/.env.example` should be present.

```powershell
Test-Path "backend\.env"
```

Expected output:

```text
False
```

## 3. Initialize Git

```powershell
git init
git status
```

## 4. Add Files

```powershell
git add .
git status
```

Check that these are not staged:

- `backend/.env`
- `backend/.venv`
- `backend/.python`
- `frontend/node_modules`
- `frontend/dist`
- `__pycache__`
- `.cache`
- any `.zip` file

## 5. Commit

```powershell
git commit -m "Add MindBridge-RAG Group 16 project"
```

## 6. Create GitHub Repository

On GitHub:

1. Click **New repository**.
2. Repository name suggestion:

```text
mindbridge-rag-group16
```

3. Keep it public or private as required by your assignment.
4. Do not add a README from GitHub because this project already has one.
5. Create the repository.

## 7. Connect Local Folder to GitHub

Replace `YOUR_USERNAME` with your GitHub username:

```powershell
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/mindbridge-rag-group16.git
git push -u origin main
```

## 8. If GitHub Rejects Push Because of Existing Remote

Check current remote:

```powershell
git remote -v
```

Update it:

```powershell
git remote set-url origin https://github.com/YOUR_USERNAME/mindbridge-rag-group16.git
git push -u origin main
```

## 9. How to Run After Cloning

Backend:

```powershell
cd backend
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
copy .env.example .env
python run.py
```

Frontend:

```powershell
cd frontend
npm install
npm run dev
```

Frontend URL:

```text
http://127.0.0.1:5173
```

Backend URL:

```text
http://127.0.0.1:8000
```

## Important API Key Note

Do not upload a real Gemini API key to GitHub. If Gemini is needed locally, put the key only in `backend/.env` after cloning. The project can still run with safe offline fallback when an external model API is unavailable or rate-limited.
