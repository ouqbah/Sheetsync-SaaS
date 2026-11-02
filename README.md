readme_content = """# SheetSync SaaS 🚀

Turn any Google Sheet into a high-performance, cached JSON REST API instantly. Optimized for serverless deployment on Google Cloud Run.

## Features
- **FastAPI Framework**: High performance, auto-generated interactive API documentation (Swagger UI).
- **In-Memory Caching**: Implements a 60-second TTL cache via `cachetools` to stay safely within Google Sheets API quota limits.
- **Robust Security**: Enforces API Key protection via simple HTTP Headers (`X-API-Key`).
- **Dockerized**: Pre-configured `Dockerfile` utilizing a lightweight `python:3.10-slim` base image, ready for Google Cloud Run.
- **Production-Ready**: Configured for stateless autoscaling with minimal memory footprint (under 256Mi).

## Project Structure
```bash
sheetsync-saas/
├── main.py            # FastAPI Application code (API endpoints + caching)
├── requirements.txt   # Pin-point Python dependencies
├── Dockerfile         # Docker container configuration
├── deploy.sh          # Deployment automation script for Google Cloud Run
├── test_main.py       # Local suite tests
└── README.md          # Project documentation
```

## Environment Variables

Configure these variables in your deployment environment (e.g., Cloud Run configuration or local `.env` file):

| Variable Name | Type | Description | Default |
|---|---|---|---|
| `API_KEY` | String | Secret key required in client headers (`X-API-Key`) | `default_secure_key_change_me` |
| `GOOGLE_SERVICE_ACCOUNT_JSON` | JSON String | Complete credential JSON from Google Cloud Console | `{}` |

## Setup & Local Usage

### 1. Installation
```bash
pip install -r requirements.txt
```

### 2. Run Local Server
```bash
uvicorn main:app --host 0.0.0.0 --port 8080 --reload
```
Access API docs locally: [http://localhost:8080/docs](http://localhost:8080/docs)

### 3. Running Unit Tests
```bash
pytest test_main.py
```

## API Endpoints

### Health Check
- **Method**: `GET`
- **Path**: `/`
- **Response**:
  ```json
  {"status": "healthy", "service": "SheetSync SaaS"}
  ```

### Read Cached Google Sheet
- **Method**: `GET`
- **Path**: `/api/v1/{sheet_id}`
- **Query Parameters**:
  - `worksheet` (Optional, default: `Sheet1`)
- **Headers**:
  - `X-API-Key` (Required to match configured `API_KEY`)
- **Response**:
  ```json
  {
    "sheet_id": "your_google_sheet_id",
    "worksheet": "Sheet1",
    "data": [
      {"ColumnA": "Row1Val", "ColumnB": "Row1Val"},
      {"ColumnA": "Row2Val", "ColumnB": "Row2Val"}
    ]
  }
  ```

## Google Cloud Run Deployment
Deploy to GCP with a single command (ensure `gcloud` SDK is configured):
```bash
chmod +x deploy.sh
./deploy.sh
```
"""

with open("README.md", "w") as f:
    f.write(readme_content)

print("✅ README.md file created successfully inside sheetsync-saas directory!")
