# 🤖 RAG Intelligent Chatbot - Modern Web Application

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![React 18](https://img.shields.io/badge/react-18.2+-61DAFB.svg)](https://reactjs.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.104+-009688.svg)](https://fastapi.tiangolo.com/)
[![Docker](https://img.shields.io/badge/docker-ready-2496ED.svg)](https://www.docker.com/)

An intelligent chatbot built with **Retrieval-Augmented Generation (RAG)** technology. This full-stack application combines the power of large language models with your custom knowledge base to provide accurate, contextual responses based on your documents.

## 🌟 Features

### Core RAG Capabilities
- **🧠 Hybrid Retrieval System**: Combines semantic search with BM25 and ensemble retrievers for optimal accuracy
- **📚 Multi-Format Document Support**: Processes PDF, TXT, DOCX, and more
- **🔍 Advanced Vector Search**: ChromaDB-powered semantic search with embedding optimization
- **💬 Conversational Memory**: Maintains context across chat sessions
- **🎯 Source Attribution**: Provides explicit references to source documents

### Advanced Features
- **📊 Admin Dashboard**: Document management, user analytics, and system configuration
- **🌐 Multi-Language Support**: French and English interface support
- **📱 Responsive Design**: Optimized for desktop, tablet, and mobile devices
- **⚡ High Performance**: Asynchronous processing and intelligent caching
- **🔐 Secure Authentication**: JWT-based authentication with role management
- **📈 Analytics & Monitoring**: Real-time performance metrics and conversation analytics

## 🏗️ Architecture

### 3-Tier Architecture
```
┌─────────────────────┐      ┌─────────────────────┐      ┌─────────────────────┐
│   React Frontend    │      │   FastAPI Backend   │      │   ChromaDB          │
│   TypeScript/Vite   │ ────>│   Python/LangChain  │ ────>│   PostgreSQL        │
│   (Port 3000)       │      │   Embedding         │      │   User Data         │
└─────────────────────┘      └─────────────────────┘      └─────────────────────┘

```

### RAG Pipeline Architecture

#### 📥 Document Ingestion Pipeline
![Document Ingestion](docs/images/ingestion-pipeline.png)

#### 🔍 Query & Response Generation Pipeline
![Query Generation](docs/images/query-pipeline.png)

## 🚀 Quick Start

### Prerequisites
- Python 3.11+
- React.js 18+
- Docker & Docker Compose (recommended)
- API Key (OpenAI or LLAMA)

### Option 1: Docker Setup (Recommended)

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/rag-intelligent-chatbot.git
cd rag-intelligent-chatbot
```

2. **Configure environment**
```bash
cp .env.example .env
# Edit .env with your configuration (see Configuration section below)
```

3. **Launch with Docker Compose**
```bash
docker-compose up -d
```

4. **Access the application**
- Frontend: http://localhost:3000
- Backend API: http://localhost:8000
- API Documentation: http://localhost:8000/docs
- Admin Panel: http://localhost:3000/admin

### Option 2: Manual Setup

#### Backend Setup
```bash
cd backend
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt

# Database initialization
alembic upgrade head

# Start the server
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

#### Frontend Setup
```bash
cd frontend
npm install
npm run dev
```

## 📋 Configuration

Create a `.env` file in the project root:

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
CORS_ORIGINS=["http://localhost:3000", "http://127.0.0.1:3000"]

# Performance
MAX_CONCURRENT_REQUESTS=50
CACHE_TTL=3600
```

## 🔧 System Components

### Backend Services

#### RAG Service
- **Document Processing**: Automated text extraction from multiple formats
- **Intelligent Chunking**: Context-preserving document segmentation
- **Embedding Generation**: Semantic vector representation using Sentence Transformers
- **Hybrid Retrieval**: Combines semantic and keyword-based search
- **Response Generation**: Contextual response generation with source attribution

#### Authentication Service
- **JWT Token Management**: Secure session handling with refresh tokens
- **Role-Based Access Control**: Admin and user role management
- **Password Security**: Bcrypt hashing with configurable complexity

#### Document Management Service
- **Multi-format Support**: PDF, DOCX, TXT processing
- **Metadata Extraction**: Automatic language detection and document analysis
- **Version Control**: Document versioning and update tracking

### Frontend Components

#### Chat Interface
- **Real-time Messaging**: WebSocket-based instant communication
- **Message History**: Persistent conversation storage
- **Typing Indicators**: Real-time interaction feedback
- **Source Display**: Referenced document visualization

#### Document Management
- **Drag-and-Drop Upload**: Intuitive file management
- **Processing Status**: Real-time upload and processing feedback
- **Metadata Editing**: Custom tags and categorization

#### Admin Dashboard
- **User Management**: Account administration and permissions
- **System Analytics**: Performance metrics and usage statistics
- **Document Organization**: Collection management and access control

## 🔌 API Endpoints

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

## 📊 Performance Characteristics

### Response Times (Target)
- **Document Processing**: < 30 seconds per document
- **Query Response**: < 5 seconds for semantic search
- **Chat Generation**: < 10 seconds for contextual responses

### Scalability
- **Concurrent Users**: 50+ simultaneous sessions
- **Document Corpus**: 1000+ documents supported
- **Vector Search**: Sub-second similarity queries

### Reliability
- **Availability**: 99% uptime target
- **Error Recovery**: Automatic retry mechanisms
- **Data Integrity**: Transactional consistency across services

## 🎨 Customization

### UI Theming
Customize the interface appearance in `frontend/tailwind.config.js`:

```javascript
module.exports = {
  theme: {
    extend: {
      colors: {
        primary: {
          50: '#eff6ff',
          500: '#3b82f6',
          900: '#1e3a8a'
        },
        // Add custom color schemes
      }
    }
  }
}
```

### RAG Configuration
Adjust retrieval and generation parameters in `backend/app/core/config.py`:

```python
class RAGSettings:
    # Retrieval settings
    MAX_RETRIEVED_DOCS = 5
    SIMILARITY_THRESHOLD = 0.7
    
    # Generation settings
    MAX_RESPONSE_LENGTH = 500
    TEMPERATURE = 0.7
    
    # Chunking parameters
    CHUNK_SIZE = 1000
    CHUNK_OVERLAP = 200
```

## 🧪 Testing

### Backend Tests
```bash
cd backend
pytest tests/ -v --cov=app --cov-report=html
```

### Frontend Tests
```bash
cd frontend
npm test
npm run test:coverage
```

### Integration Tests
```bash
# Full system testing
docker-compose -f docker-compose.test.yml up --abort-on-container-exit
```

## 🚀 Deployment

### Production Docker Setup
```bash
# Build and deploy production environment
docker-compose -f docker-compose.prod.yml up -d

# Scale services for high availability
docker-compose -f docker-compose.prod.yml up -d --scale backend=3 --scale frontend=2
```

### Cloud Deployment
The application supports deployment on:
- AWS (ECS, Lambda)
- Google Cloud Platform (Cloud Run, GKE)
- Azure (Container Apps, AKS)
- DigitalOcean (App Platform, Kubernetes)

## 🔍 Monitoring & Analytics

### System Metrics
- Response time tracking
- Error rate monitoring
- Resource utilization
- User engagement analytics

### Performance Optimization
- Redis caching for frequent queries
- Connection pooling for database access
- Lazy loading for document embeddings
- Compression for API responses

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/enhancement-name`)
3. Commit your changes (`git commit -m 'Add enhancement description'`)
4. Push to the branch (`git push origin feature/enhancement-name`)
5. Open a Pull Request

### Development Guidelines
- Follow PEP 8 for Python code style
- Use ESLint/Prettier for TypeScript formatting
- Write comprehensive tests for new features
- Update documentation for API changes
- Ensure Docker builds pass all tests

## 🐛 Troubleshooting

### Common Issues

**Vector Database Connection**
```bash
# Reset ChromaDB
rm -rf ./data/chroma_db
# Restart services
docker-compose restart backend
```

**Frontend Build Errors**
```bash
# Clear dependencies
rm -rf node_modules package-lock.json
npm install
npm run build
```

**Embedding Generation Failures**
```bash
# Verify model availability
python -c "from sentence_transformers import SentenceTransformer; SentenceTransformer('all-MiniLM-L6-v2')"
```

**Authentication Issues**
```bash
# Regenerate JWT secrets
python -c "import secrets; print(secrets.token_urlsafe(32))"
```

## 📚 Documentation

- **API Documentation**: Available at `/docs` when running in development mode
- **Architecture Guide**: See `docs/architecture.md`
- **Deployment Guide**: See `docs/deployment.md`
- **Contributing Guidelines**: See `CONTRIBUTING.md`

## 🔮 Future Enhancements

### Planned Features
- **Multi-Agent Architecture**: Specialized agents for different query types
- **Knowledge Graphs**: Enhanced relationship modeling between entities
- **RAFT Integration**: Retrieval-Augmented Fine-Tuning capabilities
- **Advanced Analytics**: User behavior analysis and system optimization
- **Mobile App**: Native iOS and Android applications

### Performance Improvements
- Streaming response generation
- Advanced caching strategies
- Distributed processing capabilities
- Real-time model fine-tuning

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [LangChain](https://langchain.com/) for the RAG framework
- [ChromaDB](https://www.trychroma.com/) for vector database capabilities
- [FastAPI](https://fastapi.tiangolo.com/) for the high-performance backend
- [React](https://reactjs.org/) for the modern frontend framework
- [Hugging Face](https://huggingface.co/) for transformer models and embeddings

---

**⭐ Star this repository if you find it helpful for your RAG implementations!**
