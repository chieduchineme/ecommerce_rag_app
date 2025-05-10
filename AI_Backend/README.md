Here’s a detailed `README.md` for your FastAPI backend project, focusing on the architecture, setup, and usage, including the steps for deploying the services, integrating the RAG mechanism, and how to run the services together.

---

# FastAPI Microservices Backend

This project implements a backend with three microservices built using **FastAPI**. These services are designed to handle different tasks within an e-commerce platform, including chat-based queries, product search, and order lookup.

## Architecture Overview

The project consists of three main microservices:

1. **Chat Service**: Accepts user queries, determines whether the intent is related to a product or an order, and routes the request to the appropriate microservice.
2. **Product Search Service**: Loads a dataset of products and performs semantic search using embeddings. It supports similarity search using natural language queries.
3. **Order Lookup Service**: Interfaces with a mock API to retrieve and format order details by customer ID, category, or priority.

Although these are separate services, we can run all of them as a single application via a `main.py` file, which coordinates the routes and handles requests for all services.

## Requirements

1. Python 3.8+
2. Virtual environment (recommended)
3. Install the following Python packages:

   * `fastapi`
   * `uvicorn`
   * `sentence-transformers` (for semantic search)
   * `weaviate-client` (for interacting with the vector DB)
   * `cohere` (or `openai` if you prefer to use OpenAI for embeddings)
   * `pydantic` (for validation)

You can install the dependencies using `pip`:

```bash
pip install -r requirements.txt
```

## Setup

### Step 1: Create Virtual Environment

To set up a virtual environment, run the following command in the project root directory:

```bash
python3 -m venv venv
```

Activate the virtual environment:

* On macOS/Linux:

```bash
source venv/bin/activate
```

* On Windows:

```bash
venv\Scripts\activate
```

### Step 2: Populate Vector DB (Weaviate)

To populate the vector database, run the data ingestion script. This will load product titles and descriptions into **Weaviate** using embeddings.

Run the following:

```bash
cd app
cd data
python data_ingestion.py
```

This script will:

* Extract product titles and descriptions.
* Generate embeddings for the titles/descriptions using the chosen embedding model (e.g., **Cohere** or **OpenAI**).
* Store these embeddings in the Weaviate vector database.

### Step 3: Run the Application

You can run the FastAPI application using Uvicorn. In the root directory, use the following command:

```bash
uvicorn main:app --reload
```

This will start the FastAPI app at `http://localhost:8000`.

### Step 4: API Documentation (Swagger UI)

Once the FastAPI app is running, you can access the Swagger UI at the following URL:

[http://localhost:8000/docs](http://localhost:8000/docs)

This provides an interactive UI where you can test all the available API routes.

### Step 5: Postman Setup

You can use Postman to test the API as well. Import the provided collection file `backend_postman_collection.json` into Postman to easily test and explore the API.

---

## Service Overview

### 1. Chat Service

This service accepts user queries and determines whether the query is related to a product or an order. Based on the query, it routes the request to the appropriate service. The API for this service might look like:

#### `POST /chatbot/ask`

**Response:**

* If the query is related to a product, it forwards the query to the **Product Search Service**.
* If the query is related to an order, it forwards the query to the **Order Lookup Service**.

### 2. Product Search Service

The Product Search Service is responsible for performing semantic search on the products dataset. It uses embeddings to understand the meaning of product queries.

This service performs the following steps:

* It loads a preprocessed dataset of products.
* It uses **sentence embeddings** (via `sentence-transformers` or similar models like **Cohere** or **OpenAI**) to embed the product descriptions and titles.
* When a query comes in, it searches for the top-N most similar products using the vector database (Weaviate).

#### Product API endpoints are in the Product microservice

### 3. Order Lookup Service

The Order Lookup Service interfaces with a mock API (or a real backend) to fetch order information by `customer_id`, `category`, or `priority`.

This service is used to query and retrieve orders based on customer requirements.

#### Order API endpoints are in Order microservice

---

## RAG (Retrieve and Generate) Integration Plan

The backend will use a lightweight **RAG** mechanism for product search. This will be accomplished in the following way:

### Preprocessing & Embedding:

* Preprocess product titles and descriptions.
* Use **vector embeddings** (from models like **Cohere** or **OpenAI**) to generate vector representations of the product data.
* Store the embeddings in **Weaviate** for fast similarity search.

### On Product Query:

* Extract the semantic meaning of the user's query using sentence embeddings.
* Perform a **similarity search** in the vector database to retrieve the top-N most relevant products.
* Generate a natural language response using either a **template-based response** or a **language model** (e.g., OpenAI's GPT-3, GPT-4, or a local model).


## Cohere vs OpenAI

While **Cohere** offers a great API for generating sentence embeddings, **OpenAI** (especially with models like **GPT-3** and **GPT-4**) provides superior performance for text generation and understanding. OpenAI’s models are highly accurate and can generate more nuanced and contextually relevant responses. For optimal performance and flexibility, we recommend using **OpenAI** over Cohere for tasks like semantic search and generating natural language responses.

