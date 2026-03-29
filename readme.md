# Advanced Motion Capture

Advanced Motion Capture is a graduation project focused on turning regular videos into reusable 3D motion data. The main application in this repository, `motionLab_app`, lets users upload a video, extract motion into BVH files, create or import avatars, and preview or retarget the results for 3D workflows.

## What this project does

- Converts uploaded videos into BVH motion capture data.
- Supports multi-person segmentation before pose processing.
- Lets users create and manage avatars.
- Retargets animation data onto 3D avatars.
- Provides a frontend for users and an admin dashboard for management tasks.

## Repository structure

- `motionLab_app/frontend`: Main React + TypeScript + Vite web application.
- `motionLab_app/backend`: Main Flask API, processing pipeline, database models, and tests.
- `threejs`: Earlier Three.js prototype and scene experiments.
- `retarget`: Retargeting notebooks, sample BVH files, and avatar assets.
- `temp`: Research, notebooks, prototype scripts, and third-party experimentation code.

If you only want to run the product, start with `motionLab_app/frontend` and `motionLab_app/backend`.

## Main stack

### Frontend

- React
- TypeScript
- Vite
- Tailwind CSS
- React Router
- Three.js / React Three Fiber
- Ready Player Me avatar creator

### Backend

- Flask
- SQLAlchemy + Flask-Migrate
- MediaPipe
- OpenCV
- PyTorch
- Ultralytics YOLO
- Blender Python API (`bpy`)

## Core workflow

1. A user uploads a video from the frontend.
2. The backend stores the upload temporarily and segments people when needed.
3. Pose processing converts the motion into one or more `.bvh` files.
4. The generated BVH files are linked to a project record in the database.
5. Users can view projects, manage avatars, and work with retargeted outputs.

The main video-processing endpoint is exposed at `POST /pose/process-video`.

## Prerequisites

Make sure you have these installed before running the app:

- Python 3.10+ recommended
- Node.js 18+ recommended
- npm

You will also need the model file referenced by the backend README:

1. Download `best_58.58.pth` from the linked Google Drive in `motionLab_app/backend/README.md`.
2. Place it inside `motionLab_app/backend/utils`.

## Backend setup

From `motionLab_app/backend`:

```powershell
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
python app.py
```

The backend runs on port `5000` by default.

### Backend environment variables

These are the main environment variables used by the backend:

- `DATABASE_URL`: Database connection string. Defaults to `sqlite:///database.db`.
- `JWT_SECRET_KEY`: Secret used for authentication tokens.
- `SECRET_KEY`: Secret used for serializers and secure token generation.
- `FLASK_DEBUG`: Set to `1` to enable debug mode.
- `FLASK_RUN_PORT`: Override the backend port. Default is `5000`.
- `FRONTEND_URL`: Used in password reset and email verification links.
- `MAIL_SERVER`: Optional mail server host. Defaults to `smtp.gmail.com`.
- `MAIL_USERNAME`: Email sender account.
- `MAIL_PASSWORD`: Email sender password or app password.

If mail credentials are not set, email-related flows may not work fully.

## Frontend setup

From `motionLab_app/frontend`:

```powershell
npm install
npm run dev
```

Create a `.env` file in `motionLab_app/frontend` and set:

```env
VITE_BACKEND_URL=http://localhost:5000
```

Vite usually runs on `http://localhost:5173`.

## Running the full app locally

1. Start the backend from `motionLab_app/backend`.
2. Start the frontend from `motionLab_app/frontend`.
3. Open the frontend Vite URL in your browser.
4. Make sure `VITE_BACKEND_URL` points to the backend URL you are using.

## Important notes

- Large ML and media dependencies are required for the backend pipeline.
- Some folders in this repository are prototypes or experiments and are not required for the main app.
- Generated files such as BVH outputs, avatars, and retargeted avatars are served by the backend.

