# Ecommerce Chatbot with RAG (Retrieve and Generate)

This project implements an intelligent **e-commerce chatbot** powered by a **Retrieve and Generate (RAG)** mechanism. It provides users with the ability to query product details and order histories through natural language, leveraging advanced semantic search and AI language models for an enriched customer experience.

The backend is built using **FastAPI** and integrates various microservices for product search, order lookup, and chat management. The chatbot can help users find specific products, inquire about orders, and get detailed product features.

## Table of Contents

1. [Overview](#overview)
2. [Architecture](#architecture)
3. [Features](#features)
4. [Setup and Installation](#setup-and-installation)
5. [API Routes](#api-routes)
6. [Example Use Cases](#example-use-cases)
7. [Future Enhancements](#future-enhancements)

---

## Overview

This e-commerce chatbot serves as an intelligent assistant for users, providing them with relevant information about products and orders based on natural language queries. Using the **Retrieve and Generate (RAG)** technique, the chatbot uses semantic search and a language model to retrieve the most relevant information and generate human-like responses.

Key services in the backend include:

* **Product Search**: Search for products based on a user’s query using semantic meaning.
* **Order Lookup**: Retrieve order history or specific order details by customer ID.
* **Chat Service**: Handle incoming user queries, route them to appropriate services (Product or Order), and provide a response.

---

## Architecture

The system is divided into the following microservices:

1. **Chatbot Service**: Handles incoming user queries and routes the request to the appropriate service (Product or Order).
2. **Product Service**: Loads product information, generates embeddings for semantic search, and performs similarity search.
3. **Order Service**: Retrieves and returns order details for users based on customer IDs or categories.
4. **Main Application**: The `main.py` file integrates all services into a single FastAPI application.

---

## Features

* **Semantic Search for Products**: Users can search for products using natural language queries, and the system retrieves the most relevant products using semantic meaning.
* **Order History Lookup**: The chatbot can provide detailed order history, including product categories, quantities, shipping costs, and more.
* **Retrieve and Generate Responses**: The chatbot combines **retrieval-based techniques** for accurate product and order matching with **generation-based models** to provide human-readable responses.

---

## Setup and Installation

` cd reactFrontend` and follow the instructions in READMe
` cd AI_Backend ` and follow the instructions in READMe

## API Routes

### 1. **Chat Query Service**

This service handles user queries. It first checks whether the query is related to a product or an order and forwards the request accordingly.

**Route**: `POST /chat/query`

Example Request:

```json
{
  "query": "what kind of Teenage Engineering Drums are available?"
}
```

Example Response:

```json
{
  "response": "The *Teenage Engineering Pocket Operator PO-12 Rhythm Drum Machine and Sequencer* is available. It produces 16 different drum sounds, offers 16 built-in effects, and allows you to create and chain up to 16 patterns together. It features real-time effect fine-tuning, a jam-sync function for connectivity, and is priced at *$99.00*."
}
```

---

### 2. **Product Search Service**

This service searches for products based on the user’s query and returns the most relevant results.

**Route**: `POST /product/search`

Example Request:

```json
{
  "query": "is there any Donner Electric Guitar Bag Gig Bag"
}
```

Example Response:

```json
{
  "response": "Yes, the *Donner 39 inch Electric Guitar Bag Gig Bag* is available. Here are its key features:\n\n1. *Material: Made of durable water-resistant 600D nylon Oxford with 10mm padded sponge and 210D smooth soft lining fabric.  \n2. **Protection: Features dual protection with an exterior bottom rubber pad and adjustable neck fixed strap to secure the guitar.  \n3. **Portability: Includes two adjustable shoulder straps, a side handle, and a top loop hanger for easy carrying and storage.  \n4. **Zippers: Equipped with durable two-way metal zippers.  \n5. **Pockets: Has three pockets for storing music sheets, accessories, and a phone.  \n6. **Price*: $35.99."
}
```

---

### 3. **Order Lookup Service**

This service retrieves and provides detailed information about a user’s orders.

**Route**: `POST /order/lookup`

Example Request:

```json
{
  "customer_id": "17631"
}
```

Example Response:

```json
{
  "response": "Based on the provided context, there is only one order associated with the customer_id *17631*:\n\n- **Product Category: Auto & Accessories\n- **Product: Car Pillow & Neck Rest\n- **Order Date: 2018-09-26\n- **Quantity: 3.0\n- **Discount: 0.1\n- **Customer Login Type: Member\n- **Shipping Cost: 13.0\n- **Order Priority: High\n- **Sales: 231.0\n- **Payment Method: credit_card\n- **Profit: 130.2"
}
```

---

## Example Use Cases

### Product Search Example 1

**User Input**: "What kind of Teenage Engineering Drums are available?"

**Response**:
"The *Teenage Engineering Pocket Operator PO-12 Rhythm Drum Machine and Sequencer* is available. It produces 16 different drum sounds, offers 16 built-in effects, and allows you to create and chain up to 16 patterns together. It features real-time effect fine-tuning, a jam-sync function for connectivity, and is priced at *\$99.00*."

### Product Search Example 2

**User Input**: "Is there any Donner Electric Guitar Bag Gig Bag?"

**Response**:
"Yes, the *Donner 39 inch Electric Guitar Bag Gig Bag* is available. It is made from durable, water-resistant nylon with a padded interior, ensuring great protection for your guitar. It costs *\$35.99*."

### Order Lookup Example 1

**User Input**: "Tell me about all the orders of a user with the customer\_id 17631."

**Response**:
"Based on the provided context, there is only one order associated with the customer\_id *17631*:\n\n- **Product Category**: Auto & Accessories\n- **Product**: Car Pillow & Neck Rest\n- **Order Date**: 2018-09-26\n- **Quantity**: 3.0\n- **Discount**: 0.1\n- **Order Priority**: High."

### Order Lookup Example 2

**User Input**: "Has a user with the customer\_id 86057 ordered a Home & Furniture item before?"

**Response**:
"Yes, a user with the customer\_id *86057* ordered a Home & Furniture item. Specifically, they ordered *Curtains* on *2018-09-26*."

---

## Future Enhancements

* Global State Management in Frontend
* PWA in frontend
* Integration with Mongo or MySQL DB in backend ...