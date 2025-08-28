### 0) Prerequisites
- Node.js 18+ and npm
- Python 3.10+ (with pip)
- Git
- Ollama (local LLM runner)
  - Install from `https://ollama.com`

### 1) Clone
```bash
git clone <YOUR_REPO_URL>
cd negokart
```

### 2) Backend setup (FastAPI)
Windows PowerShell:
```powershell
cd backend
python -m venv venv
venv\Scripts\activate

pip install fastapi uvicorn sqlalchemy pydantic[dotenv] python-jose[cryptography] passlib[bcrypt] httpx python-multipart
```

### 3) Ollama (Local AI model)
- Open a new terminal and run:
```bash
ollama pull llama3.2:3b
```
- Verify Ollama is up (should return JSON):
```bash
# Windows PowerShell
(Invoke-WebRequest http://127.0.0.1:11434/api/tags).Content
```

### 4) Start the backend
In the backend terminal (with venv active):
```powershell
# Optional: set model envs per session (Windows)
$env:OLLAMA_MODEL="llama3.2:3b"
$env:OLLAMA_BASE_URL="http://127.0.0.1:11434"

uvicorn main:app --reload
```

Backend runs at http://127.0.0.1:8000

### 5) Frontend setup (React + Vite)
Open a second terminal:
```bash
cd frontend
npm install
npm run dev
```
Frontend runs at the URL shown (usually http://localhost:5173)


That’s it. Anyone who clones the repo can follow these steps and get a fully working local instance with AI negotiation using a free local LLM.


### Troubleshooting
1. Ollama not found or model missing:
  - Install Ollama, then run: ollama pull llama3.2:3b
  - Check API: (Invoke-WebRequest http://127.0.0.1:11434/api/tags).Content

2. Backend says “python-multipart required”:
  - pip install python-multipart in the backend venv

3. httpx or others missing:
  - pip install httpx (or re-run the backend pip install line)

4. CORS blocked:
  - CORS is enabled in backend/main.py for dev
