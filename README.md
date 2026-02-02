# Y-Docs for LLMs

Turn any YouTube video into structured documentation that AI coding tools and LLMs can easily index and understand.

## 🚀 Features

- **📺 YouTube Video Processing**: Extract video metadata, descriptions, and thumbnails
- **📝 Transcript Extraction**: Automatically extract video transcripts in multiple languages
- **💬 Comments Integration**: Optional inclusion of video comments for additional context
- **🤖 AI-Friendly Output**: Generate structured documentation perfect for LLM consumption
- **⚡ Fast Processing**: Efficient video processing with rate limiting and caching
- **🌍 Multi-Language Support**: Support for transcripts in 9+ languages
- **📱 Responsive Design**: Beautiful, modern UI built with Tailwind CSS
- **🔧 API Access**: RESTful API for programmatic access
- **🐳 Docker Ready**: Easy deployment with Docker and Docker Compose

## 🛠️ Tech Stack

- **Backend**: FastAPI + Python 3.11+
- **Frontend**: Tailwind CSS + Jinja2 templates
- **Video Processing**: yt-dlp, pytube, youtube-transcript-api
- **Token Estimation**: tiktoken
- **Rate Limiting**: slowapi
- **Deployment**: Docker, Docker Compose

## 📦 Installation

### Option 1: Docker (Recommended)

```bash
# Clone the repository
git clone https://github.com/alecbideri/to-doc.git
cd to-doc

# Run with Docker Compose
docker-compose up -d
```

### Option 2: Local Installation

```bash
# Clone the repository
git clone https://github.com/alecbideri/to-doc.git
cd to-doc

# Install dependencies
pip install -r requirements.txt

# Run the application
uvicorn src.server.main:app --host 0.0.0.0 --port 8000 --reload
```

## 🚀 Usage

### Web Interface

1. Open your browser and navigate to `http://localhost:8000`
2. Enter a YouTube video URL
3. Configure processing options:
   - **Transcript Length**: Maximum characters to include
   - **Language**: Preferred transcript language
   - **Include Comments**: Whether to extract video comments
4. Click "Create Docs" to process the video

### API Usage

#### Process a Video

```bash
curl -X POST "http://localhost:8000/" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "input_text=https://www.youtube.com/watch?v=VIDEO_ID" \
  -d "max_transcript_length=10000" \
  -d "language=en" \
  -d "include_comments=false"
```

#### Python Example

```python
import requests

url = "http://localhost:8000/"
data = {
    "input_text": "https://www.youtube.com/watch?v=VIDEO_ID",
    "max_transcript_length": 10000,
    "language": "en",
    "include_comments": False
}

response = requests.post(url, data=data)
print(response.text)
```

## 🔧 Configuration

Create a `.env` file based on `.env.example`:

```bash
cp .env.example .env
```

### Key Configuration Options

- `ALLOWED_HOSTS`: Comma-separated list of allowed hosts
- `YOUTUBE_API_KEY`: Optional YouTube Data API key for enhanced features
- `OPENAI_API_KEY`: Optional OpenAI API key for AI-enhanced processing
- `RATE_LIMIT_PER_MINUTE`: Number of requests per minute per IP

### AWS S3 Integration (for cloud documentation links)

To publish generated docs to S3, configure an S3 bucket and environment variables:

1. Create an S3 bucket with appropriate permissions
2. Set environment variables in `.env`:

```bash
AWS_S3_BUCKET=YOUR_BUCKET
AWS_ACCESS_KEY_ID=your_access_key
AWS_SECRET_ACCESS_KEY=your_secret_key
AWS_REGION=your-region
```

### Proxy Configuration (Cloud Deployment Only)

**⚠️ Note: This is only needed for cloud deployment. Local development works without proxies.**

When deploying to cloud providers, YouTube may block requests from cloud IPs. Configure rotating residential proxies:

```bash
YTA_HTTP_PROXY=http://user:pass@proxy-host:port
YTA_HTTPS_PROXY=https://user:pass@proxy-host:port
```

## 📋 Supported YouTube URL Formats

- `https://www.youtube.com/watch?v=VIDEO_ID`
- `https://youtu.be/VIDEO_ID`
- `https://www.youtube.com/embed/VIDEO_ID`
- `https://www.youtube.com/v/VIDEO_ID`

## 🌍 Supported Languages

- English (en)
- Spanish (es)
- French (fr)
- German (de)
- Italian (it)
- Portuguese (pt)
- Japanese (ja)
- Korean (ko)
- Chinese (zh)

## 🔄 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/` | Home page with video processing form |
| `POST` | `/` | Process a YouTube video |
| `GET` | `/video/{video_id}` | Get processing form for specific video |
| `POST` | `/video/{video_id}` | Process specific video |
| `GET` | `/api` | API documentation |
| `GET` | `/health` | Health check endpoint |

## 📊 Rate Limits

- Main endpoint: 10 requests per minute per IP
- Video-specific endpoint: 5 requests per minute per IP

## 🐳 Docker Deployment

### Development

```bash
docker-compose up -d
```

### Production

```bash
docker build -t y-docs .
docker run -p 8000:8000 \
  -e ALLOWED_HOSTS=yourdomain.com \
  -e DEBUG=False \
  y-docs
```

## 📝 Example Output

The generated documentation includes:

- **Video Metadata**: Title, duration, view count, channel info
- **Description**: Full video description
- **Transcript**: Complete video transcript with timestamps
- **Comments**: Top video comments (if enabled)
- **Token Estimation**: Estimated token count for LLM usage

## 🧪 Testing

```bash
python -m pytest tests/
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**Made with ❤️ for the AI and developer community**
