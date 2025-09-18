<p align="center">
<img src="app\images\trans_bg.png" width="300px" height="300px">
</p>

# Intelligent News Reading System

The Intelligent News Reading System is designed to enhance the news consumption experience by integrating modern machine learning techniques and large language models. The system collects data from reputable Vietnamese news sources (such as VnExpress, Thanh Niên, Tuổi Trẻ, and Dân Trí) using tools like BeautifulSoup. Leveraging advanced language models (e.g., GPT, Gemini, and ViT5), it automatically summarizes articles and converts them into natural Vietnamese speech. This allows users to quickly grasp key information or listen to the news on the go, which is especially beneficial for busy individuals or those with visual impairments.

# Techs Stack
<p align='center'>
<img src='https://img.shields.io/badge/Google%20Gemini-8E75B2?style=for-the-badge&logo=googlegemini&logoColor=white'/>
<img src='https://img.shields.io/badge/-HuggingFace-FDEE21?style=for-the-badge&logo=HuggingFace&logoColor=black'/>
<img src='https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white'/>
<img src='https://img.shields.io/badge/TensorFlow-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white'/>
<img src='https://img.shields.io/badge/Python-FFD43B?style=for-the-badge&logo=python&logoColor=blue'/>
<img src='https://img.shields.io/badge/scikit_learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white'>
<img src='https://img.shields.io/badge/fastapi-109989?style=for-the-badge&logo=FASTAPI&logoColor=white'/>
<img src='https://img.shields.io/badge/Swagger-85EA2D?style=for-the-badge&logo=Swagger&logoColor=white'/>
<img src='https://img.shields.io/badge/Railway-131415?style=for-the-badge&logo=railway&logoColor=white'/>
</p>

# Key Features

### 📰 News Crawling & Processing
- **Automated News Crawling**: Crawls news articles from major Vietnamese news sources (VnExpress, Thanh Niên, Tuổi Trẻ, Dân Trí)
- **BeautifulSoup Integration**: Efficient web scraping with content extraction and cleaning
- **Configurable Article Limits**: Supports custom limits for the number of articles to crawl
- **Content Validation**: Ensures crawled content meets quality standards

### 🤖 AI-Powered Text Summarization
- **Multi-Model Support**: Integrates with advanced language models including GPT, Gemini, and ViT5
- **Vietnamese Language Optimization**: Specialized handling for Vietnamese text processing
- **Intelligent Summarization**: Generates concise, meaningful summaries while preserving key information
- **Customizable Summary Length**: Configurable summary parameters based on content type

### 🎵 Text-to-Speech (TTS) Conversion
- **Vietnamese TTS**: High-quality Vietnamese speech synthesis
- **Natural Voice Generation**: Produces natural-sounding Vietnamese speech
- **Audio File Management**: Automatic audio file generation and storage
- **Cloud Storage Integration**: Seamless integration with AWS S3 for audio file storage

### ☁️ Cloud Integration
- **AWS S3 Storage**: Secure cloud storage for generated audio files
- **File Management**: Automated upload, retrieval, and management of media files
- **Scalable Storage**: Cloud-based storage solution for handling large volumes of audio content

### 🔧 API Infrastructure
- **RESTful API Design**: Clean, well-documented API endpoints
- **Swagger Documentation**: Interactive API documentation for easy integration
- **Error Handling**: Comprehensive error handling with meaningful error messages
- **Response Validation**: Structured response models with proper validation

# Installation & Setup

### Prerequisites
- **Python 3.8+**
- **pip** (Python package installer)
- **Git**
- **AWS Account** (for S3 storage)
- **Google Gemini API Key** (for AI services)

### Environment Setup

1. **Clone the repository**
```bash
git clone <repository-url>
cd VNNewsVoice_MLService
```

2. **Create and activate virtual environment**
```bash
python -m venv venv
venv\Scripts\activate

# Linux/Mac
python3 -m venv venv
source venv/bin/activate
```

3. **Install dependencies**
```bash
pip install -r requirements.txt
```

4. **Environment Configuration**

Create a .env file in the root directory with the following variables:
```properties
# API Configuration
API_HOST=0.0.0.0
API_PORT=8000
DEBUG=True

# AI Model Configuration
GEMINI_API_KEY=your_gemini_api_key_here
HUGGINGFACE_API_TOKEN=your_huggingface_token_here

# AWS Configuration
AWS_ACCESS_KEY_ID=your_aws_access_key
AWS_SECRET_ACCESS_KEY=your_aws_secret_key
AWS_REGION=your_aws_region
S3_BUCKET_NAME=your_s3_bucket_name

# TTS Configuration
TTS_MODEL_NAME=default_vietnamese_tts_model
TTS_VOICE_SPEED=1.0

# Crawling Configuration
DEFAULT_MAX_ARTICLES=10
CRAWL_TIMEOUT=30
USER_AGENT=VNNewsVoice-Bot/1.0

# Logging
LOG_LEVEL=INFO
```

### Build & run
```bash
# Using uvicorn directly
uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload

# Or using the main script
python -m app.main
```

# Project structure
```
VNNewsVoice_MLService/
├── app/
│   ├── main.py                    # FastAPI application entry point
│   ├── core/
│   │   └── config.py             # Configuration management
│   ├── models/                   # Pydantic models
│   │   ├── __init__.py
│   │   ├── article.py           # Article data models
│   │   └── response.py          # API response models
│   ├── routers/                 # API route handlers
│   │   ├── __init__.py
│   │   ├── news.py             # News crawling endpoints
│   │   ├── summarization.py    # Text summarization endpoints
│   │   └── tts.py              # Text-to-speech endpoints
│   ├── schemas/                # Request/Response schemas
│   │   ├── __init__.py
│   │   ├── article.py          # Article schemas
│   │   └── tts.py              # TTS schemas
│   ├── services/               # Business logic services
│   │   ├── __init__.py
│   │   ├── aws_storage_service.py    # AWS S3 integration
│   │   ├── cloud_service.py          # Cloud services wrapper
│   │   ├── crawl_news_service.py     # News crawling logic
│   │   ├── text_summarization.py    # AI summarization service
│   │   └── tts_service.py            # Text-to-speech service
│   └── images/
│       └── trans_bg.png         # Application assets
├── requirements.txt             # Python dependencies
├── .env                        # Environment variables
├── .gitignore
└── README.md
```

# API Endpoints

News Crawling
- ``GET /api/v1/crawl/vietnamese-news`` - Crawl Vietnamese news articles
- ``POST /api/v1/crawl/custom`` - Custom crawling with parameters

Text Summarization
- ``POST /api/v1/summarize/text`` - Summarize text content
- ``POST /api/v1/summarize/article`` - Summarize news articles

Text-to-Speech
- ``POST /api/v1/tts/generate`` - Generate speech from text
- ``GET /api/v1/tts/audio/{file_id}`` - Retrieve generated audio files

Health & Status
- ``GET /health`` - Service health check
- ``GET /status`` - Service status and metrics

# Support
If you encounter any issues, have questions, or want to contribute, please feel free to:

- Open an [issue](https://github.com/thereaper0602/VNNewsVoice_Backend/issues) in this repository.
- Contact the maintainer via email: **phiminhquang10a10@gmail.com**
- Check the project Wiki or documentation for setup and troubleshooting guides.