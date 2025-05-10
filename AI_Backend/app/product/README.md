# 🤖 Ecommerce Product API

A FastAPI microservice for product data exploration and search, designed to support an LLM-powered chatbot and retrieval-augmented generation (RAG) pipeline. It integrates well with vector databases like Weaviate.

---

## 🚀 Features

* 🔍 Search products by title, category, store, or rating
* 📊 Filter and fetch product insights
* 🧠 Supports intelligent RAG pipelines (via `/values/*` endpoints)
* 📂 Preloaded with static product data (via `load_product_data`)
* 🌐 Fully documented Swagger UI + Postman-ready

---

## 🧰 Requirements

* Python 3.9+
* `pip` or `poetry`

---

## 🗂️ Project Structure

```
app/
├── product/
│   ├── product_service.py   # Product API logic
│   ├── product_main.py      # FastAPI app entry point
├── data/
│   └── preprocess.py        # Loads product dataset
```

---

## 🔧 Setup Instructions

1. **Clone the repo:**

   ```bash
   git clone https://github.com/your-username/ecommerce-product-api.git
   cd ecommerce-product-api
   ```

2. **Create virtual environment:**

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies:**

   ```bash
   pip install -r requirements.txt
   ```

   *(If not available, install manually:)*

   ```bash
   pip install fastapi uvicorn pandas numpy
   ```

4. **Run the server:**

   ```bash
   python app/product/product_main.py
   ```

   Server will be accessible at:
   👉 `http://127.0.0.1:8000`

---

## 📖 API Documentation

* **Swagger UI:**
  [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

* **ReDoc:**
  [http://127.0.0.1:8000/redoc](http://127.0.0.1:8000/redoc)

---

## 📬 Postman Integration

1. Open Postman.
2. Import from URL:

   ```
   http://127.0.0.1:8000/openapi.json
   ```
3. Postman will auto-generate API requests.

---

## 📚 Key Endpoints

### 📦 Product Data

* `GET /product/all`
  → All products

* `GET /product/search/{title}`
  → Search by product title

* `GET /product/category/{category}`
  → Filter by main category

* `GET /product/rating/above/{threshold}`
  → Filter by rating threshold

* `GET /product/store/{store_name}`
  → Filter by store name

### 📊 Metadata for Filtering (Useful for Chatbot or UI)

* `GET /product/values/average_rating`
* `GET /product/values/store`
* `GET /product/values/main_category`
* `GET /product/values/title`


