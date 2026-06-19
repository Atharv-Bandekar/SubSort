# SubSort: AI YouTube Subscription Organizer

An AI-powered Chrome Extension (Manifest V3) that automatically categorizes a user's chaotic YouTube subscription feed into 12 clean, distinct buckets. Built with a modern, asynchronous MLOps pipeline using a fine-tuned DeBERTa-v3-Small architecture.

## The Architecture

This project utilizes a highly optimized **Client-Thin, Server-Thick** architecture to bypass API rate limits and survive strict cloud hosting memory constraints.

* **Zero-API Extraction:** The extension extracts subscription data instantly from YouTube's hidden `ytInitialData` JSON object, requiring zero network overhead or DOM scraping.
* **Horizontal Feed UI:** Injects lightweight CSS pill filters directly into the native YouTube subscription grid for instant, zero-lag categorization.
* **ONNX Quantization:** The backend runs a fine-tuned DeBERTa-v3-Small text classification model, exported to an Int8-quantized ONNX format to perform high-speed inference within a 512MB RAM server limit.
* **Global Caching:** A relational database caches AI predictions globally, ensuring that popular channels are categorized in milliseconds without redundant compute.

## Tech Stack

**Frontend (Chrome Extension)**
* Vanilla JavaScript (ES6+)
* HTML5 / CSS3
* Manifest V3 Architecture

**Backend (MLOps & API)**
* FastAPI (Python, Asynchronous ASGI)
* PyTorch & Hugging Face Transformers
* ONNX Runtime (CPU Inference)
* Supabase / PostgreSQL (Global Cache)
* Pandas (Data Wrangling)

## Repository Structure
```
├── backend/                  # FastAPI server and ML pipeline
│   ├── app/                  # API endpoints, models, and database logic
│   └── data_engineering/     # Pandas scripts and Kaggle dataset processing
├── frontend/                 # Chrome extension source code
│   ├── manifest.json         # Extension configuration
│   ├── content.js            # DOM extraction and UI injection
│   └── styles.css            # Pill filter styling
├── .gitignore                
└── README.md                 
```

## The API Contract

To enable parallel development, the frontend and backend strictly adhere to the following JSON payload structure:

**Client POST Request (`/classify`):**
```json
{
  "user_id": "string",
  "channels": ["@MarquesBrownlee", "@3blue1brown"]
}

```

**Server Response**:
```json
{
  "status": "success",
  "classifications": {
    "@MarquesBrownlee": "Technology & Software",
    "@3blue1brown": "Science & Education"
  }
}

```
