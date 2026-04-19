# RAG Chatbot - AI Knowledge Assistant

A Retrieval-Augmented Generation (RAG) application built with Next.js and the Vercel AI SDK. This application allows administrators to ingest PDF documents, converts the text into vector embeddings, and provides a chat interface that answers user questions based on the context of the uploaded data.

## Features

* **Vector Search:** Stores and queries 1536-dimensional embeddings using Neon PostgreSQL with the pgvector extension and HNSW indexing.
* **Document Ingestion:** Processes uploaded PDFs by extracting text and segmenting it into overlapping chunks using LangChain and the Vercel AI SDK.
* **Access Control:** Restricts document upload functionality to authorized administrators using Clerk JWT session claims and Next.js edge middleware.
* **Streaming Responses:** Utilizes the Vercel AI SDK to stream conversational responses back to the user interface.

## Tech Stack

* **Framework:** Next.js (App Router)
* **Language:** TypeScript
* **AI Libraries:** Vercel AI SDK, LangChain
* **Database:** Neon Serverless PostgreSQL
* **ORM:** Drizzle ORM
* **Database Extension:** pgvector
* **Authentication:** Clerk
* **Styling:** Tailwind CSS, Shadcn UI
* **Linting/Formatting:** Biome

## Getting Started

### Prerequisites
You will need Node.js installed on your machine, along with active accounts for Neon (PostgreSQL), Clerk (Authentication), and OpenAI (LLM and Embeddings).

### 1. Clone the repository
```bash
git clone [https://github.com/samiyun/AI-SDK-RAG-Chatbot.git](https://github.com/samiyun/AI-SDK-RAG-Chatbot.git)
cd AI-SDK-RAG-Chatbot
```

### 2. Install dependencies
```bash
npm install
```

### 3. Set up Environment Variables
Create a .env.local file in the root directory and add your configuration keys:
```bash
(example)
# Authentication (Clerk)
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
CLERK_SECRET_KEY=your_clerk_secret_key

# Database (Neon PostgreSQL)
DATABASE_URL=postgresql://user:password@ep-cool-cloud.region.aws.neon.tech/neondb

# AI Providers
OPENAI_API_KEY=your_openai_api_key
```

### 4. Database Setup & Migrations
```bash
npx drizzle-kit push
```
### 5. Run the Development Server
Open http://localhost:3000 with your browser to interact with the application.
```bash
npm run dev
```
### Overview
1. Upload: An authorized administrator uploads a PDF document. The file is parsed and passed to LangChain splitters to divide the text into overlapping chunks.

2. Embedding: The text chunks are sent to OpenAI's embedding model to generate vector representations.

3. Storage: The vectors and their corresponding text chunks are stored in a Neon PostgreSQL database using the pgvector extension.

4. Retrieval: When a user submits a question, the query is converted into a vector. An HNSW-indexed similarity search retrieves the closest matching document chunks from the database.

5. Generation: The retrieved text chunks and the user's prompt are sent to the LLM via the Vercel AI SDK to generate a response based on the provided context.
