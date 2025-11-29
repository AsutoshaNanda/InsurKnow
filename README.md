<div align="center">

# InsurKnow

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/downloads/)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4-green.svg)](https://platform.openai.com/)
[![Gradio](https://img.shields.io/badge/Gradio-Interface-orange.svg)](https://gradio.app/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

**Insurance Knowledge Assistant: RAG-Powered AI Platform for Employee & Product Information**

</div>

--- 
<div align="center">
    <h2>📋 Table of Contents</h2>
    <table>
        <tr>
            <td><a href="#features">✨ Features</a></td>
            <td><a href="#requirements">📦 Requirements</a></td>
            <td><a href="#installation">🔧 Installation</a></td>
        </tr>
        <tr>
            <td><a href="#configuration">⚙️ Configuration</a></td>
            <td><a href="#usage">🎮 Usage</a></td>
            <td><a href="#architecture">🏗️ Architecture</a></td>
        </tr>
        <tr>
            <td><a href="#knowledge-base">📚 Knowledge Base</a></td>
            <td><a href="#contributing">🤝 Contributing</a></td>
            <td><a href="#license">📄 License</a></td>
        </tr>
        <tr>
           <td style="padding:0; border:none;"></td>
            <td style="text-align:center;">
                <a href="#troubleshooting">🐛 Troubleshooting</a>
            </td>
            <td style="padding:0; border:none;"></td>
        </tr>
    </table>
</div>

---

## ✨ Features

### 🤖 **Retrieval-Augmented Generation (RAG)**
- Smart context retrieval from knowledge base
- Automatically identifies relevant employee and product information
- Provides accurate answers based on internal knowledge
- Seamless integration with OpenAI's GPT models

### 📚 **Comprehensive Knowledge Base**
- **Employees**: 30+ employee profiles with professional information
- **Products**: 8 insurance products with detailed specifications
- Easily expandable and updatable knowledge sources
- Organized file-based storage system

### 💬 **Conversational AI**
- Multi-turn chat interface with conversation history
- Context-aware responses maintaining conversation flow
- Brief and accurate answer generation
- Graceful handling of unknown queries

### 🖥️ **Interactive Web UI**
- Beautiful Gradio chat interface
- Real-time response streaming
- Clean, intuitive design
- Accessible from any browser

### 🔒 **Secure Configuration**
- Environment variable management via `.env` file
- API key protection
- Safe model initialization

---


## 📦 Requirements

### System Requirements
- **Python 3.8+**
- **8GB+ RAM**
- **Internet connection** (for OpenAI API)

### Python Dependencies
```
python-dotenv>=0.21.0
openai>=1.0.0
gradio>=4.0.0
```

---

## 🔧 Installation

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/insurknow.git
cd insurknow
```

### 2. Create Virtual Environment
```bash
python -m venv venv
source venv/bin/activate  # On macOS/Linux
# or
venv\Scripts\activate  # On Windows
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Configure Environment Variables
Create a `.env` file in the project root:
```env
OPENAI_API_KEY=your_openai_api_key_here
```

### 5. Organize Knowledge Base
Ensure you have the following directory structure:
```
project-root/
├── knowledge-base/
│   ├── employees/
│   │   ├── Employee 1.txt
│   │   ├── Employee 2.txt
│   │   └── ...
│   └── products/
│       ├── Product 1.txt
│       ├── Product 2.txt
│       └── ...
```

---

## ⚙️ Configuration

### API Keys Setup

#### OpenAI API
1. Visit [OpenAI Platform](https://platform.openai.com/)
2. Navigate to API keys section
3. Create new secret key
4. Add to `.env` file as `OPENAI_API_KEY`

### Model Configuration
```python
# Set your preferred model in the notebook
MODEL = "gpt-4.1-nano"  # Change to your desired OpenAI model
openai = OpenAI()  # Initializes with API key from .env
```

### Knowledge Base Structure

The system automatically loads all files from:
- `../knowledge-base/employees/*` - Employee information files
- `../knowledge-base/products/*` - Product information files

Files are indexed by their filename stem (last word before extension).

---

## 🎮 Usage

### Quick Start

#### 1. Launch Jupyter Notebook
```bash
jupyter notebook InsurKnow.ipynb
```

#### 2. Execute All Cells
- Run all cells sequentially to initialize the system
- The knowledge base will be loaded into memory
- API connection will be verified

#### 3. Launch Gradio Interface
- Execute the final cell to start the chat interface
- Access via the provided local URL (typically `http://127.0.0.1:7861`)

#### 4. Ask Questions
- Type your question about Insurellm employees or products
- The system will automatically retrieve relevant context
- Receive accurate, brief answers

### Example Queries

```
"Tell me about Employee Lancaster"
"What are our insurance products?"
"Who is Chen and what do they do?"
"Describe the Home insurance product"
"List all claims-related products"
```

---

## 🏗️ Architecture

### Component Overview

```
┌──────────────────────────────────────────────────────┐
│        Gradio Chat Interface (UI Layer)              │
├──────────────────────────────────────────────────────┤
│                                                      │
│  ┌────────────────────┐      ┌──────────────────┐    │
│  │  User Input        │      │  Assistant Reply │    │
│  └────────────────────┘      └──────────────────┘    │
│                                                      │
├──────────────────────────────────────────────────────┤
│        Retrieval-Augmented Generation (RAG)          │
├──────────────────────────────────────────────────────┤
│                                                      │
│  ┌─────────────────────────────────────────────┐     │
│  │  Context Retrieval Engine                   │     │
│  │  - Extract keywords from user message       │     │
│  │  - Match against knowledge base             │     │
│  │  - Build relevant context                   │     │
│  └─────────────────────────────────────────────┘     │
│                                                      │
├──────────────────────────────────────────────────────┤
│        OpenAI API Integration Layer                  │
├──────────────────────────────────────────────────────┤
│                                                      │
│  ┌─────────────────────────────────────────────┐     │
│  │  System Prompt + Context + History          │     │
│  │  ↓                                          │     │
│  │  GPT Model Processing                       │     │
│  │  ↓                                          │     │
│  │  Response Generation                        │     │
│  └─────────────────────────────────────────────┘     │
│                                                      │
├──────────────────────────────────────────────────────┤
│        Knowledge Base Layer                          │
├──────────────────────────────────────────────────────┤
│                                                      │
│  ┌────────────────────┐  ┌────────────────────┐      │
│  │  Employee Data     │  │  Product Data      │      │
│  │  (30+ profiles)    │  │  (8 products)      │      │
│  └────────────────────┘  └────────────────────┘      │
│                                                      │
└──────────────────────────────────────────────────────┘
```

### Key Functions

| Function | Purpose | Input | Output |
|----------|---------|-------|--------|
| `get_relevant_contexts()` | Extract knowledge base matches | User message | List of relevant documents |
| `additional_context()` | Format context for prompt | User message | Formatted context string |
| `chat()` | Main chat function with RAG | Message + history | AI response |
| `load_knowledge()` | Initialize knowledge base | File paths | Dictionary of documents |

### Data Flow

1. **User Input** → User types a question in Gradio
2. **Context Retrieval** → System extracts keywords and retrieves matching documents
3. **Prompt Construction** → System builds prompt with context and conversation history
4. **API Call** → Request sent to OpenAI with full prompt
5. **Response Generation** → GPT generates answer based on context
6. **Output** → Response displayed in Gradio interface

---

## 📚 Knowledge Base

### Supported Content

#### Employees (30 profiles)
- Kim, Patel, Sharma, Chen, Spencer, Foster, Tran, Blake, Zhang, Thompson, Adams, Liu, Lancaster, Park, Greene, Johnson, Thomson, O'Brien, Martinez, Williams, Rivera, Trenton, Anderson, Harper, Rodriguez, Wilson, Bishop, Carter, Brooks, Walker

#### Products (8 categories)
- rellm (General)
- claimllm (Claims)
- bizllm (Business)
- lifellm (Life Insurance)
- healthllm (Health Insurance)
- markellm (Marketing)
- homellm (Home Insurance)
- carllm (Car Insurance)

### Adding New Content

1. Create text file with relevant information
2. Place in appropriate directory:
   - `../knowledge-base/employees/` for employee files
   - `../knowledge-base/products/` for product files
3. File will be automatically loaded on next system restart
4. Naming convention: Use last word before extension as the key

---

## 🐛 Troubleshooting

### Issue: "OpenAI API Key not set"
**Solution**: Verify `.env` file exists and contains correct key
```bash
cat .env  # Check file contents
echo $OPENAI_API_KEY  # Verify environment variable
```

### Issue: "Knowledge base files not found"
**Solution**: Check directory structure
```bash
ls ../knowledge-base/employees/
ls ../knowledge-base/products/
```

### Issue: "No additional context relevant to the user's question"
**Solution**: This is normal for out-of-domain questions. The system will still try to answer based on general knowledge.

### Issue: "Rate limit exceeded" from OpenAI
**Solution**: Wait a few minutes before making new requests, or upgrade OpenAI plan

### Issue: Gradio interface won't launch
**Solution**: Check if port 7861 is available
```bash
# On macOS/Linux
lsof -i :7861

# On Windows
netstat -ano | findstr :7861
```

### Issue: "Module not found" errors
**Solution**: Reinstall dependencies
```bash
pip install -r requirements.txt --upgrade
```

---

## 🤝 Contributing

Contributions welcome! Please follow these steps:

1. Fork the repository
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open Pull Request

### Guidelines
- Follow PEP 8 for Python code
- Add docstrings to new functions
- Test with sample queries before submitting
- Include documentation for new knowledge base additions
- Update README with significant changes

---

## 📁 File Structure

```
insurknow/
├── InsurKnow.ipynb                     # Main Jupyter notebook
├── knowledge-base/
│   ├── employees/
│   │   ├── Employee 1.txt
│   │   ├── Employee 2.txt
│   │   └── ...
│   └── products/
│       ├── Product 1.txt
│       ├── Product 2.txt
│       └── ...
├── .env                                # Environment variables (git-ignored)
├── requirements.txt                    # Python dependencies
├── README.md                           # This file
└── LICENSE                             # MIT License
```

---

## 📄 License

This project is licensed under the Apache License - see the [LICENSE](LICENSE) file for details.

---

## 📚 Additional Resources

- [OpenAI API Docs](https://platform.openai.com/docs/)
- [Gradio Documentation](https://www.gradio.app/docs/)
- [Python dotenv](https://python-dotenv.readthedocs.io/)

---

## 🙋 Support & Contact

- **Issues**: Open GitHub issues for bugs
- **Questions**: Create discussions in GitHub

---

<div align="center">

**[⬆ Back to Top](#-insurknow)**

**Insurance Knowledge Assistant**  
Made with ❤️ for Insurellm

</div>
