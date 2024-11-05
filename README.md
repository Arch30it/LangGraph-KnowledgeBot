# LangGraph RAG Chatbot

This repository contains code for a LangChain-based chatbot that utilizes Retrieval-Augmented Generation (RAG) to fetch relevant document snippets based on user queries. It integrates a custom Wikipedia agent alongside web-based document retrieval, using Astra DB (Cassandra) as the vector store to store and retrieve embedded document vectors. The chatbot pipeline also includes environment configuration for securely handling API keys and database tokens.

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Installation](#installation)
- [Environment Setup](#environment-setup)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

## Overview

This project sets up a chatbot using LangChain and RAG, with two main retrieval methods: web-based document fetching and a Wikipedia-based query agent. The Wikipedia agent enables the chatbot to answer questions by directly retrieving summaries from Wikipedia. For documents sourced from the web, the project uses a predefined set of URLs, splitting and embedding them for efficient search and retrieval.

## Features

- **Document Loading**: Fetches content from specified URLs using LangChain's `WebBaseLoader`.
- **Text Splitting**: Splits large documents into smaller chunks for better retrieval performance.
- **Vector Embedding**: Embeds text chunks using the `all-MiniLM-L6-v2` model from HuggingFace.
- **Vector Store with Cassandra**: Stores and retrieves embedded document vectors from Astra DB (Cassandra).
- **Wikipedia Agent**: Uses LangChain’s `WikipediaAPIWrapper` to enable Wikipedia-based query retrieval.
- **Environment Configuration**: Uses `.env` for secure storage of API keys and database credentials.

## Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/yourusername/langgraph-rag-chatbot.git
   cd langgraph-rag-chatbot
   ```
   
2. **Install required Python packages**:
```bash
  pip install -r requirements.txt
```

## Environment Setup
Create a .env file in the root directory with the following keys:

```bash
ASTRA_DB_APPLICATION_TOKEN=your_astra_db_token
ASTRA_DB_ID=your_astra_db_id
GROQ_API_KEY=your_groq_api_key
```

## Load environment variables 
The code automatically loads environment variables from .env using load_dotenv().

## Usage
Set up Database Connection: The code initializes a connection to Astra DB and sets up a Cassandra vector store for document embedding and retrieval.

Document Processing and Embedding:

URLs are specified in the code and loaded using LangChain's WebBaseLoader.
Documents are split into smaller chunks using RecursiveCharacterTextSplitter.
Each chunk is embedded using the all-MiniLM-L6-v2 model.
Wikipedia Agent Setup: The Wikipedia agent allows the chatbot to retrieve concise information from Wikipedia based on user queries.

The agent is created using LangChain's WikipediaAPIWrapper, which connects to Wikipedia's public API to fetch summaries.
This agent can act as a fallback or supplement to web-based document retrieval, enriching the chatbot’s responses with encyclopedic content.
Insert Documents into Vector Store: The embedded document chunks are stored in Cassandra, with a confirmation message indicating the number of documents inserted.

Run the Chatbot: Implement a chatbot interface (not shown in this notebook) to query the stored documents based on user input and retrieve relevant snippets, including data retrieved via the Wikipedia agent.

## Example
Here’s a basic outline of how the notebook processes documents and integrates the Wikipedia agent:

Load documents from specified URLs and Wikipedia queries.
Split web-based documents into smaller chunks.
Embed and store chunks in Cassandra.
Retrieve document snippets or Wikipedia summaries based on the user query.
Contributing
Feel free to fork this repository, make changes, and submit pull requests. For major changes, please open an issue first to discuss your ideas.

## License
This project is licensed under the MIT License. See the LICENSE file for more details.
