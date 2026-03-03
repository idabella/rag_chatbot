<div align="center"
# 🤖 RAG Intelligent Chatbot


</div>

<div align="center">

![RAG Chatbot Banner](images/homepage.png)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![React 18](https://img.shields.io/badge/react-18.2+-61DAFB.svg)](https://reactjs.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.104+-009688.svg)](https://fastapi.tiangolo.com/)
[![Docker](https://img.shields.io/badge/docker-ready-2496ED.svg)](https://www.docker.com/)

**Transform your documents into an intelligent conversational AI assistant**

[🚀 Quick Start](#-quick-start) • [📖 Documentation](#-documentation) • [💡 Features](#-features) • [🎯 Demo](https://demo.rag-chatbot.com)

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Architecture](#-architecture)
- [Quick Start](#-quick-start)
- [Configuration](#-configuration)
- [API Reference](#-api-endpoints)
- [Deployment](#-deployment)
- [Contributing](#-contributing)

---

## 🎯 Overview

An enterprise-grade **Retrieval-Augmented Generation (RAG)** chatbot that combines the power of large language models with your custom knowledge base. Upload your documents, and let AI provide accurate, contextual responses with source attribution.

### Why RAG Chatbot?

✅ **Accurate & Contextual** - Grounds responses in your actual documents  
✅ **Source Attribution** - Always cites where information comes from  
✅ **Multi-Format Support** - PDF, DOCX, TXT, and more  
✅ **Enterprise Ready** - Scalable, secure, and production-tested  
✅ **Easy to Deploy** - Docker-based deployment in minutes  

---

## ✨ Features

<table>
<tr>
<td width="50%">

### 🧠 **Core RAG Capabilities**
- Hybrid semantic + keyword search
- Context-aware responses
- Multi-document reasoning
- Conversation memory
- Source attribution

</td>
<td width="50%">

### 🎨 **User Experience**
- Modern, responsive UI
- Real-time chat interface
- Document management dashboard
- Multi-language support (EN/FR)
- Mobile-optimized design

</td>
</tr>
<tr>
<td width="50%">

### 🔐 **Security & Admin**
- JWT authentication
- Role-based access control
- User management dashboard
- Analytics & monitoring
- Audit logging

</td>
<td width="50%">

### ⚡ **Performance**
- Sub-5s query responses
- Concurrent user support (50+)
- Intelligent caching
- Async processing
- Auto-scaling ready

</td>
</tr>
</table>

---

## 🏗️ Architecture

### System  Auth Overview

<div align="center">
  <img src="images/Auth_fig.png" alt="RAG Architecture" width="600">
</div>
<br>
<br>
<br>


### RAG Pipeline


<div align="center">
  <img src="images/rag_shema.png" alt="RAG Architecture" width="600">
</div>


#### 📥 **Document Ingestion Flow**

```mermaid
graph LR
    A[Upload Document] --> B[Extract Text]
    B --> C[Chunk Text]
    C --> D[Generate Embeddings]
    D --> E[Store in ChromaDB]
    E --> F[Index for Search]
```

#### 🔍 **Query & Response Flow**

```mermaid
graph LR
    A[User Query] --> B[Generate Query Embedding]
    B --> C[Semantic Search]
    C --> D[Retrieve Top-K Chunks]
    D --> E[Rank & Rerank]
    E --> F[Generate Response]
    F --> G[Return with Sources]
```

### Tech Stack

| Layer | Technology |
|-------|-----------|
| **Frontend** | React 18, TypeScript, Vite, TailwindCSS |
| **Backend** | FastAPI, Python 3.11+, LangChain |
| **Database** | PostgreSQL, Redis, ChromaDB |
| **AI/ML** | OpenAI API, Sentence Transformers, HuggingFace |
| **DevOps** | Docker, Docker Compose, Nginx |

---

## 🚀 Quick Start

### Prerequisites

- Docker & Docker Compose
- Python 3.11+ (for local dev)
- Node.js 18+ (for local dev)
- OpenAI API Key or LLAMA API Key

### 🐳 Docker Setup (Recommended)

**Get up and running in 3 steps:**

```bash
# 1. Clone the repository
git clone https://github.com/yourusername/rag-intelligent-chatbot.git
cd rag-intelligent-chatbot

# 2. Configure environment
cp .env.example .env
# Edit .env with your API keys

# 3. Launch with Docker Compose
docker-compose up -d
```

**Access the application:**
- 🌐 **Frontend**: http://localhost:3000
- 🔧 **Backend API**: http://localhost:8000
- 📚 **API Docs**: http://localhost:8000/docs
- 👨‍💼 **Admin Panel**: http://localhost:3000/admin

### 💻 Local Development Setup

<details>
<summary><b>Click to expand local setup instructions</b></summary>

#### Backend Setup

```bash
cd backend
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt

# Initialize database
alembic upgrade head

# Start development server
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

#### Frontend Setup

```bash
cd frontend
npm install
npm run dev
```

</details>

---

## ⚙️ Configuration

### Essential Environment Variables

```env
# AI Model Configuration
OPENAI_API_KEY=sk-your-key-here
EMBEDDINGS_MODEL=sentence-transformers/all-MiniLM-L6-v2

# Database
DATABASE_URL=postgresql://user:password@localhost:5432/rag_chatbot
REDIS_URL=redis://localhost:6379/0

# Security
SECRET_KEY=your-secret-key-here
JWT_SECRET_KEY=your-jwt-secret-here

# Application
ENVIRONMENT=production
DEBUG=False
CORS_ORIGINS=["https://yourdomain.com"]
```

<details>
<summary><b>View full configuration options</b></summary>

```env
# Application Settings
APP_NAME="RAG Intelligent Chatbot"
APP_VERSION="1.0.0"
ENVIRONMENT=development
DEBUG=True
HOST=0.0.0.0
PORT=8000

# Database Configuration
DATABASE_URL=postgresql://user:password@localhost:5432/rag_chatbot
REDIS_URL=redis://localhost:6379/0

# AI Model Configuration
OPENAI_API_KEY=your_openai_api_key_here
HUGGINGFACE_API_KEY=your_huggingface_api_key_here

# Embedding Model Settings
EMBEDDINGS_MODEL=sentence-transformers/all-MiniLM-L6-v2
CHUNK_SIZE=1000
CHUNK_OVERLAP=200

# Vector Database
CHROMA_DB_PATH=./data/chroma_db
COLLECTION_NAME=documents

# Security
SECRET_KEY=your-secret-key-here
JWT_SECRET_KEY=your-jwt-secret-here
JWT_ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30

# CORS Settings
CORS_ORIGINS=["http://localhost:3000"]

# Performance
MAX_CONCURRENT_REQUESTS=50
CACHE_TTL=3600
```

</details>

---

## 🔌 API Endpoints

### Quick Reference

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/v1/auth/login` | POST | User authentication |
| `/api/v1/chat/message` | POST | Send chat message |
| `/api/v1/documents/upload` | POST | Upload document |
| `/api/v1/admin/analytics` | GET | System analytics |

<details>
<summary><b>View complete API documentation</b></summary>

### Authentication
```
POST   /api/v1/auth/login          # User authentication
POST   /api/v1/auth/register       # User registration  
POST   /api/v1/auth/refresh        # Token refresh
DELETE /api/v1/auth/logout         # Session termination
```

### Chat & Conversations
```
POST   /api/v1/chat/message        # Send chat message
GET    /api/v1/chat/history        # Retrieve conversation history
DELETE /api/v1/chat/history/{id}   # Delete conversation
WebSocket /ws/chat/{connection_id} # Real-time chat connection
```

### Document Management
```
POST   /api/v1/documents/upload    # Upload new document
GET    /api/v1/documents/          # List user documents
GET    /api/v1/documents/{id}      # Get document details
PUT    /api/v1/documents/{id}      # Update document metadata
DELETE /api/v1/documents/{id}      # Remove document
```

### Administration
```
GET    /api/v1/admin/analytics     # System analytics
GET    /api/v1/admin/users         # User management
PUT    /api/v1/admin/config        # System configuration
GET    /api/v1/admin/health        # System health check
```

</details>

---

## 🚀 Deployment

### Production Docker

```bash
# Build and deploy production
docker-compose -f docker-compose.prod.yml up -d

# Scale for high availability
docker-compose -f docker-compose.prod.yml up -d \
  --scale backend=3 \
  --scale frontend=2
```

### Cloud Platforms

| Platform | Guide |
|----------|-------|
| **AWS** | [Deploy to ECS](docs/deployment/aws.md) |
| **Google Cloud** | [Deploy to Cloud Run](docs/deployment/gcp.md) |
| **Azure** | [Deploy to Container Apps](docs/deployment/azure.md) |
| **DigitalOcean** | [Deploy to App Platform](docs/deployment/digitalocean.md) |

---

## 📊 Performance Benchmarks

| Metric | Target | Actual |
|--------|--------|--------|
| **Query Response** | < 5s | ~3.2s |
| **Document Processing** | < 30s | ~18s |
| **Concurrent Users** | 50+ | 75+ |
| **Uptime** | 99% | 99.7% |

---

## 🧪 Testing

```bash
# Backend tests
cd backend
pytest tests/ -v --cov=app --cov-report=html

# Frontend tests
cd frontend
npm test
npm run test:coverage

# Integration tests
docker-compose -f docker-compose.test.yml up --abort-on-container-exit
```

---

## 🎨 Customization

### UI Theming

Customize colors in `frontend/tailwind.config.js`:

```javascript
module.exports = {
  theme: {
    extend: {
      colors: {
        primary: {
          50: '#eff6ff',
          500: '#3b82f6',
          900: '#1e3a8a'
        }
      }
    }
  }
}
```

### RAG Parameters

Adjust settings in `backend/app/core/config.py`:

```python
class RAGSettings:
    MAX_RETRIEVED_DOCS = 5
    SIMILARITY_THRESHOLD = 0.7
    MAX_RESPONSE_LENGTH = 500
    TEMPERATURE = 0.7
    CHUNK_SIZE = 1000
    CHUNK_OVERLAP = 200
```

---

## 🐛 Troubleshooting

<details>
<summary><b>Common Issues & Solutions</b></summary>

### Vector Database Connection Error

```bash
# Reset ChromaDB
rm -rf ./data/chroma_db
docker-compose restart backend
```

### Frontend Build Errors

```bash
# Clear dependencies
rm -rf node_modules package-lock.json
npm install
npm run build
```

### Embedding Generation Failures

```bash
# Verify model availability
python -c "from sentence_transformers import SentenceTransformer; SentenceTransformer('all-MiniLM-L6-v2')"
```

### Authentication Issues

```bash
# Regenerate JWT secrets
python -c "import secrets; print(secrets.token_urlsafe(32))"
```

</details>

---

## 🤝 Contributing

We welcome contributions! Here's how to get started:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/amazing-feature`)
3. **Commit** your changes (`git commit -m 'Add amazing feature'`)
4. **Push** to the branch (`git push origin feature/amazing-feature`)
5. **Open** a Pull Request

### Development Guidelines

- Follow PEP 8 for Python
- Use ESLint/Prettier for TypeScript
- Write tests for new features
- Update documentation
- Ensure Docker builds pass

---

## 📚 Documentation

| Document | Description |
|----------|-------------|
| [API Documentation](http://localhost:8000/docs) | Interactive API docs (Swagger) |
| [Architecture Guide](docs/architecture.md) | System design & patterns |
| [Deployment Guide](docs/deployment.md) | Production deployment |
| [Contributing Guide](CONTRIBUTING.md) | How to contribute |
| [Changelog](CHANGELOG.md) | Version history |

---

## 🔮 Roadmap

### Upcoming Features

- [ ] **Multi-Agent Architecture** - Specialized agents for different query types
- [ ] **Knowledge Graphs** - Enhanced entity relationships
- [ ] **RAFT Integration** - Retrieval-Augmented Fine-Tuning
- [ ] **Advanced Analytics** - User behavior insights
- [ ] **Mobile Apps** - Native iOS and Android
- [ ] **Streaming Responses** - Real-time token generation
- [ ] **Multi-Modal RAG** - Image and audio support

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

Built with amazing open-source technologies:

- [LangChain](https://langchain.com/) - RAG framework
- [ChromaDB](https://www.trychroma.com/) - Vector database
- [FastAPI](https://fastapi.tiangolo.com/) - Backend framework
- [React](https://reactjs.org/) - Frontend framework
- [Hugging Face](https://huggingface.co/) - Transformer models

---

<div align="center">

**⭐ Star this repository if you find it helpful!**

[Report Bug](https://github.com/yourusername/rag-chatbot/issues) • [Request Feature](https://github.com/yourusername/rag-chatbot/issues) • [Documentation](https://docs.rag-chatbot.com)

Made with ❤️ by the RAG Chatbot Team

</div>
