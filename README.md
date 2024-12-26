# AMCS_Hackathon
# Chatbot System with Document Ingestion and Interpretation

This project implements a chatbot system that can ingest and interpret uploaded documents (e.g., PDFs) to provide accurate, fact-based responses using LLM APIs and retrieval techniques. The system supports creating and managing conversations through a REST API.

## Features

### Core Features

- **Document Ingestion**: Supports uploading various document formats, such as PDFs, TXT, DOCX, and images (PNG, JPG, JPEG).
- **Query and Response**: Processes queries to retrieve relevant content from uploaded documents and generates accurate responses using LLMs.
- **Document Vectorization**: Utilizes Qdrant for vector storage and retrieval.
- **User-specific Conversations**: Maintains user-specific data and provides personalized responses.

### Additional Features

- **Bulk Upload Support**: Handles multiple document uploads and processing.
- **Security by Design**: Includes input validation and file type restrictions to ensure security.
- **Enhanced UI/UX**: Integrates streaming APIs for real-time feedback (future implementation).
- **Hallucination Prevention**: Employs techniques like prompt engineering and grounding to ensure responses are based on source material.

## Technologies Used

- **Python**: Core language for backend development.
- **Flask**: Web framework to create REST APIs.
- **Qdrant**: Vector database for storing and retrieving document embeddings.
- **LangChain**: For text processing, embedding, and vectorization.
- **Gemini**: Custom LLM for response generation.
- **Firebase Firestore**: For managing conversation data.
- **Logging**: Ensures traceability and debugging.

## Setup and Installation

### Prerequisites

- Python 3.9+
- Qdrant instance with API key
- Firebase Admin SDK credentials

### Installation Steps

1. **Clone the repository:**

   ```bash
   git clone https://github.com/your-repo/chatbot-system.git
   cd chatbot-system
   ```

2. **Create a virtual environment and activate it:**

   ```bash
   python3 -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies:**

   ```bash
   pip install -r requirements.txt
   ```

4. **Configure Qdrant and Firebase:**

   - Update the Qdrant client configuration in `config/vector_db.py` with your Qdrant URL and API key.
   - Add your Firebase Admin SDK credentials in `config/db.py`.

5. **Set up the upload directory:**

   ```bash
   mkdir uploads
   ```

6. **Start the Flask application:**

   ```bash
   python app.py
   ```

### Environment Variables

Define the following environment variables:

- `QDRANT_API_KEY`: Your Qdrant API key.
- `QDRANT_URL`: URL of your Qdrant instance.
- `FIREBASE_CREDENTIALS`: Path to your Firebase Admin SDK credentials file.

## API Endpoints

### 1. Create New Conversation

- **Endpoint**: `/app/conversation/new`
- **Method**: `POST`

**Parameters:**

- `user_id` (form): User ID
- `query` (form, optional): Query text
- `file` (file, optional): Document to upload

**Response:**

```json
{
  "message": "New conversation created successfully.",
  "conversation_id": "<conversation_id>",
  "queries": []
}
```

### 2. Add Query to Conversation

- **Endpoint**: `/app/conversation/<conversation_id>/add`
- **Method**: `POST`

**Parameters:**

- `query` (form, optional): Query text
- `file` (file, optional): Document to upload

**Response:**

```json
{
  "message": "Query added successfully.",
  "query_id": "<query_id>",
  "response": "<generated_response>"
}
```

## File Upload and Processing

### Supported File Types

- **Text**: `.txt`
- **Documents**: `.pdf`, `.doc`, `.docx`
- **Images**: `.png`, `.jpg`, `.jpeg`

### File Storage

Uploaded files are stored in the `uploads/` directory with unique names.

### Vectorization

Documents are split into chunks using `RecursiveCharacterTextSplitter` and vectorized using embeddings from `model_embedding`. The vectors are stored in a Qdrant collection.

## Logging

The application uses Python’s `logging` module for tracing and debugging. Logs include timestamps, log levels, and meaningful messages to aid in debugging and monitoring.

## Error Handling

Common error scenarios are handled with appropriate HTTP status codes:

- `400`: Invalid input or file type
- `404`: Conversation not found
- `500`: Internal server errors

## Future Enhancements

- Integrate streaming APIs for real-time responses.
- Extend security features (e.g., authentication and encryption).
- Improve UI/UX with a frontend framework like React or Streamlit.
- Add support for more document types (e.g., spreadsheets).
- Enhance hallucination prevention with advanced grounding techniques.
