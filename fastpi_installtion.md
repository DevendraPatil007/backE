STEP-BY-STEP: FASTAPI INSTALLATION AND SETUP

STEP 1: Check Python is installed
   Command:  python3 --version
   Why: FastAPI requires Python 3.8+. This confirms Python exists and
   which version you have before installing anything on top of it.

STEP 2: (Recommended) Create a virtual environment
   Command:  python3 -m venv venv
   Why: Creates an isolated folder ("venv") containing its own Python
   binary and its own site-packages directory. This keeps FastAPI and
   its dependencies separate from your system Python, avoiding version
   conflicts with other projects.

STEP 3: Activate the virtual environment
   Command:
     source venv/bin/activate        (Mac/Linux)
     venv\Scripts\activate           (Windows)
   Why: Rewires your terminal's PATH so "python" and "pip" now point to
   the venv's own binaries instead of the system ones. Your prompt will
   show "(venv)" at the start once active.

STEP 4: Install FastAPI and Uvicorn
   Command:  pip install fastapi "uvicorn[standard]"
   Why:
     - fastapi = the framework that lets you define routes, request
       validation, and response models using Python type hints.
     - uvicorn = the ASGI server that actually runs your app and
       listens for HTTP requests. FastAPI alone can't serve traffic;
       it needs an ASGI server underneath it.
     - "[standard]" pulls in optional extras (uvloop, httptools,
       websockets support, auto-reload watcher) for better performance
       and a smoother dev experience.

STEP 5: Verify the installation
   Command:  python3 -c "import fastapi, uvicorn; print(fastapi.__version__, uvicorn.__version__)"
   Why: Confirms both packages installed correctly and prints their
   versions, catching any silent install failures early.

STEP 6: Create your first app file
   File:  main.py
   Content:
     from fastapi import FastAPI
     app = FastAPI()

     @app.get("/")
     def read_root():
         return {"message": "Hello, FastAPI"}
   Why: "app" is the FastAPI instance uvicorn will look for by name.
   The @app.get("/") decorator registers a route — when someone visits
   "/", this function runs and its return value is auto-converted to
   JSON.

STEP 7: Run the development server
   Command:  uvicorn main:app --reload
   Why:
     - "main:app" tells uvicorn: look inside main.py, find the object
       named "app", and serve it.
     - "--reload" watches your files and restarts the server
       automatically on every save — essential during development,
       should be removed in production.

STEP 8: Test it in the browser
   URLs:
     http://127.0.0.1:8000        → your actual endpoint response
     http://127.0.0.1:8000/docs   → auto-generated interactive Swagger UI
     http://127.0.0.1:8000/redoc  → alternative auto-generated docs
   Why: FastAPI reads your type hints and route definitions to build
   this documentation automatically — no extra code required.

STEP 9: Deactivate the environment when done
   Command:  deactivate
   Why: Exits the virtual environment and returns your terminal to the
   system Python. You'll need to reactivate (Step 3) next time you
   work on this project.git