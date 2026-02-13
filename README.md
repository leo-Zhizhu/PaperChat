# PaperChat

A powerful AI-powered chat application that combines Retrieval Augmented Generation (RAG) with web search capabilities. Upload PDF documents and ask questions to get intelligent answers based on your documents and real-time web information.

## 🌟 Main Features

### 1. **PDF Document Processing**
- Upload PDF documents through an intuitive drag-and-drop interface
- Automatic document parsing and text extraction
- Intelligent chunking and vectorization for efficient retrieval

### 2. **Dual Answer System**
- **RAG Answers**: Get answers based on your uploaded PDF documents using LangChain's vector store
- **Web Search Answers**: Get real-time information from the web using SerpAPI integration
- Compare both answers side-by-side for comprehensive understanding

### 3. **Voice Interaction**
- **Voice Input**: Use speech recognition to ask questions hands-free
- **Voice Output**: Listen to answers with text-to-speech functionality
- **Chat Mode**: Toggle between text and voice interaction modes

### 4. **Modern UI/UX**
- Clean, responsive interface built with Ant Design
- Real-time conversation history display
- Loading states and error handling
- Fixed chat input for easy access

## 🚀 Technical Highlights

### Frontend Stack
- **React 18**: Modern React with hooks and functional components
- **Ant Design**: Beautiful and professional UI components
- **React Speech Recognition**: Browser-based speech-to-text
- **Speak-TTS**: Text-to-speech synthesis
- **Axios**: HTTP client for API communication

### Backend Stack
- **Express.js**: Fast and minimalist web framework
- **LangChain**: Powerful framework for building LLM applications
- **OpenAI API**: GPT models for intelligent question answering
- **Model Context Protocol (MCP)**: Protocol for connecting AI models with external tools
- **SerpAPI**: Web search integration
- **PDF-Parse**: PDF document parsing
- **Multer**: File upload handling

### Key Technologies
- **Vector Stores**: Memory-based vector storage for semantic search
- **Embeddings**: OpenAI embeddings for document vectorization
- **Retrieval Augmented Generation (RAG)**: Combines retrieval and generation for accurate answers
- **Text Splitting**: Recursive character text splitting for optimal chunking

## 📐 Project Architecture

```
agentai/
├── src/                          # React frontend
│   ├── components/
│   │   ├── ChatComponent.js     # Main chat interface with voice support
│   │   ├── PdfUploader.js       # PDF upload component
│   │   └── RenderQA.js          # Q&A display component
│   ├── App.js                   # Main application component
│   └── index.js                 # React entry point
│
├── server/                       # Express backend
│   ├── server.js                # Express server setup
│   ├── chat.js                  # RAG implementation with LangChain
│   ├── chat-mcp.js              # MCP client for web search
│   ├── mcp-server.js            # MCP server for SerpAPI integration
│   └── uploads/                 # PDF storage directory
│
├── public/                       # Static assets
└── package.json                  # Frontend dependencies
```

### Architecture Flow

1. **PDF Upload Flow**:
   ```
   User → PdfUploader → Express /upload → Multer → server/uploads/
   ```

2. **Question Answering Flow**:
   ```
   User Question → ChatComponent → Express /chat
                                      ├→ chat.js (RAG from PDF)
                                      └→ chat-mcp.js (Web Search)
                                  → Combined Response → User
   ```

3. **RAG Pipeline**:
   ```
   PDF → PDFLoader → TextSplitter → Embeddings → VectorStore → Retriever → LLM → Answer
   ```

4. **MCP Web Search Flow**:
   ```
   Query → MCP Client → MCP Server → SerpAPI → Search Results → LLM → Summary
   ```

## 🛠️ Installation & Setup

### Prerequisites
- Node.js (v16 or higher)
- npm or yarn
- OpenAI API key
- SerpAPI key (optional, for web search)

### Step 1: Clone the Repository
```bash
git clone https://github.com/leo-Zhizhu/AgentAI.git
cd AgentAI
```

### Step 2: Install Dependencies

**Frontend:**
```bash
npm install
```

**Backend:**
```bash
cd server
npm install
cd ..
```

### Step 3: Configure Environment Variables

Create a `.env` file in the `server/` directory:

```bash
cd server
cp ../.env.example .env
```

Edit `.env` and add your API keys:
```env
OPENAI_API_KEY=your_openai_api_key_here
SERPAPI_KEY=your_serpapi_key_here
PORT=5001
```

### Step 4: Run the Application

**Option 1: Run both frontend and backend together**
```bash
npm run dev
```

**Option 2: Run separately**

Terminal 1 (Backend):
```bash
npm run server
```

Terminal 2 (Frontend):
```bash
npm start
```

The application will be available at:
- Frontend: http://localhost:3000
- Backend: http://localhost:5001

## 📦 Deployment

### Local Development
Follow the installation steps above. The application runs in development mode with hot-reloading.

### Production Build

**Build Frontend:**
```bash
npm run build
```

**Run Production Server:**
```bash
# Install production dependencies
npm install --production

# Set NODE_ENV
export NODE_ENV=production

# Start server
cd server
npm start
```

### Deployment Options

#### Option 1: Deploy to Vercel/Netlify (Frontend) + Railway/Heroku (Backend)

**Frontend (Vercel):**
1. Connect your GitHub repository to Vercel
2. Set build command: `npm run build`
3. Set output directory: `build`
4. Add environment variable: `REACT_APP_DOMAIN=your_backend_url`

**Backend (Railway/Heroku):**
1. Create a new project and connect your repository
2. Set root directory to `server/`
3. Add environment variables:
   - `OPENAI_API_KEY`
   - `SERPAPI_KEY`
   - `PORT` (usually auto-set by platform)
4. Deploy

#### Option 2: Docker Deployment

Create a `Dockerfile` in the root:
```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
COPY server/package*.json ./server/
RUN npm install && cd server && npm install
COPY . .
RUN npm run build
EXPOSE 5001
CMD ["node", "server/server.js"]
```

#### Option 3: Traditional Server Deployment

1. Build the frontend: `npm run build`
2. Serve the `build/` directory with a static file server (nginx, Apache)
3. Run the backend as a Node.js service (PM2, systemd)
4. Configure reverse proxy to route API calls to backend

### Environment Variables for Production

Ensure these are set in your production environment:
- `OPENAI_API_KEY`: Required
- `SERPAPI_KEY`: Required for web search
- `NODE_ENV`: Set to `production`
- `PORT`: Backend port (default: 5001)
- `REACT_APP_DOMAIN`: Frontend environment variable pointing to backend URL

## 🔒 Security Notes

- Never commit `.env` files or API keys to version control
- The `.gitignore` file is configured to exclude sensitive files
- Uploaded PDFs are stored locally and should be secured in production
- Consider implementing authentication and rate limiting for production use

## 📝 Usage

1. **Upload a PDF**: Drag and drop or click to upload a PDF document
2. **Ask Questions**: Type your question in the search box or use voice input
3. **View Answers**: See both RAG (from PDF) and web search answers
4. **Voice Mode**: Toggle "Chat Mode" to enable voice interaction
5. **Conversation History**: View all previous questions and answers

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is open source and available under the MIT License.

## 🙏 Acknowledgments

- LangChain for the powerful RAG framework
- OpenAI for GPT models
- Ant Design for beautiful UI components
- Model Context Protocol for tool integration

---

**Note**: Make sure to keep your API keys secure and never expose them in client-side code or public repositories.
