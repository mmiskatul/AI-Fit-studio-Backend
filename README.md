# AI Fit Studio Backend

FastAPI backend for an **AI virtual try-on MVP**. A user uploads a full-body photo and picks a product, and the API sends both images to an image model, which generates a try-on preview.

Built for the **AI Business Summit 2026**, hosted by the Data Science Club at Daffodil International University.

<!-- [add 3-4 example results: user photo, garment, generated try-on] -->

## How it works

```
User photo ──┐
             ├──►  Fal AI image model  ──►  try-on preview  ──►  saved with metadata
Garment ─────┘     (Gemini image edit)
```

1. The user uploads a photo (jpg, jpeg, png, or webp, up to 10 MB).
2. The user chooses a product from the catalog.
3. The backend sends the user image and the garment image, plus a prompt, to Fal AI. The default model is `fal-ai/gemini-25-flash-image/edit`.
4. The result is stored with its history in MongoDB, together with the provider, model ID, output URL, file details, and the seed returned by Fal (when available).

## Features

- Product catalog with full CRUD, seeded on startup
- Photo uploads, stored on Cloudinary in production (local `uploads/` fallback)
- Try-on generation with stored history
- Admin dashboard, usage analytics, and persisted studio settings (rendering preferences feed into future generations)

## API (main endpoints)

| Method | Path | Purpose |
|---|---|---|
| GET, POST | `/api/products` | List or create products |
| GET, PUT, DELETE | `/api/products/{product_id}` | Read, update, or delete a product |
| POST | `/api/uploads/user-photo` | Upload a user photo |
| GET | `/api/admin/dashboard` | Admin overview |
| GET | `/api/admin/analytics?days=30` | Usage analytics |
| GET, PUT | `/api/admin/settings` | Read or update studio settings |

[Add the try-on generation endpoint here.]

## Tech stack

Python 3.11+, FastAPI, Pydantic, MongoDB (Motor, async), Fal AI, Cloudinary

## Getting started

```bash
git clone https://github.com/mmiskatul/AI-Fit-studio-Backend.git
cd AI-Fit-studio-Backend
pip install -r requirements.txt
cp .env.example .env        # add your Fal AI, MongoDB, and Cloudinary keys
uvicorn main:app --reload   # [adjust the module path to match your project]
```

## Related

- Website: [AI-Fit-studio-Website](https://github.com/mmiskatul/AI-Fit-studio-Website)

## Limitations

- Output quality depends on the hosted image model and on the photo quality.
- [Add what you observed: pose, lighting, clothing types that work best or worst.]
