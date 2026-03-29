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

## Poster
<img width="744" height="964" alt="Screenshot 2026-02-17 155538" src="https://github.com/user-attachments/assets/785fd336-c8ae-405b-8295-3e9864eb865e" />

# Web App
<img width="1894" height="878" alt="Screenshot 2025-04-04 185500" src="https://github.com/user-attachments/assets/00743b19-64d1-4a0b-a9fa-38b0435920f9" />
<img width="1882" height="876" alt="Screenshot 2025-04-04 190300" src="https://github.com/user-attachments/assets/00cba302-e6c0-4034-afd9-d66427d57592" />
<img width="1885" height="873" alt="Screenshot 2025-04-04 184743" src="https://github.com/user-attachments/assets/45dfa6e1-c581-4184-83bc-2baa3e62b34a" />
<img width="1873" height="884" alt="Screenshot 2025-04-04 192340" src="https://github.com/user-attachments/assets/2a3df571-39b9-468d-ae1e-fec833b39ad6" />
<img width="1880" height="879" alt="Screenshot 2025-04-04 192254" src="https://github.com/user-attachments/assets/3cc9999e-4598-4bf3-b11f-0e935e727c8c" />

# Blender
<img width="1919" height="1020" alt="Screenshot 2025-04-04 185300" src="https://github.com/user-attachments/assets/c3071fa6-3538-43e0-bb18-4d0f2ebf6a81" />


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

## Thesis
[Thesis_Document_for_Character_Animation_from_Video.pdf](https://github.com/user-attachments/files/26327915/Thesis_Document_for_Character_Animation_from_Video.pdf)

## Technical document
[Technical_Document_for_Character_Animation_from_Video.pdf](https://github.com/user-attachments/files/26327917/Technical_Document_for_Character_Animation_from_Video.pdf)

## Paper
[Motion_detection__From_video_to_BVH.pdf](https://github.com/user-attachments/files/26327918/Motion_detection__From_video_to_BVH.pdf)

