# 🛒 Ecommerce Order API

A FastAPI-based microservice for managing and analyzing ecommerce order data.

## 🚀 Features

* Retrieve all orders
* Filter orders by:

  * Customer ID
  * Product Category
  * Order Priority
* Aggregate insights:

  * Total Sales by Product Category
  * Profit by Customer Gender
  * High-profit products
  * Shipping cost summary
* Access unique values for key fields (useful for dropdowns in UIs)
* Fully documented via Swagger and easy to test via Postman

---

## 📦 Project Structure

```
app/
├── order/
│   ├── order_service.py   # API logic
│   ├── order_main.py      # FastAPI app entry
│   └── ...
├── data/
│   └── preprocess.py      # Data loading utilities
```

---

## 🧰 Requirements

* Python 3.9+
* `pip` or `poetry`

---

## 🔧 Setup Instructions

1. **Clone the repo:**

   ```bash
   git clone https://github.com/your-username/ecommerce-order-api.git
   cd ecommerce-order-api
   ```

2. **Create a virtual environment:**

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies:**

   ```bash
   pip install -r requirements.txt
   ```

   *(If `requirements.txt` doesn't exist, create one with FastAPI, Uvicorn, Pandas, etc.)*

   ```bash
   pip install fastapi uvicorn pandas
   ```

4. **Run the server:**

   ```bash
   python app/order/order_main.py
   ```

   The server should now be running at:
   👉 **[http://127.0.0.1:8000](http://127.0.0.1:8000)**

---

## 📖 API Docs (Swagger)

Once running, visit:

🔗 **Swagger UI:**
[http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

🔗 **ReDoc:**
[http://127.0.0.1:8000/redoc](http://127.0.0.1:8000/redoc)

---

## 📬 Postman Usage

1. Open Postman.
2. Create a new request or import from URL:

   ```
   http://127.0.0.1:8000/openapi.json
   ```
3. Postman will auto-generate request collections based on your API schema.

---

## 📚 Example Endpoints

* `GET /order/all` → Get all orders
* `GET /order/data/customer/{customer_id}` → Orders by customer
* `GET /order/data/total-sales-by-category` → Sales summary
* `GET /order/data/values/order_priority` → All order priorities

---

## 🧪 Testing Tips

* Try playing with query parameters like `/order/data/high-profit-products?min_profit=500`
* Send invalid values to test error handling

---

