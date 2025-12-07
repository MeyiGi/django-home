# 🏠 Home — Furniture E-Commerce Store

**Home** is a full-featured **e-commerce web application** built with **Django 4.2** and **Bootstrap 5**. It simulates a modern online furniture store with a dynamic product catalog, full-text search, user authentication, a persistent shopping cart, and a complete order management system.

This project demonstrates clean backend architecture, real-world business logic, and performance-oriented design.

---

## 🚀 Features

### 🪑 Product Catalog

* Browse products by categories (Kitchen, Bedroom, Living Room, etc.)
* **Advanced Full-Text Search** using PostgreSQL `SearchVector` with ranking and highlighting
* **Filtering & Sorting** by sale status and price
* **Pagination** for efficient large catalog handling

### 🛒 Shopping Cart

* **AJAX-powered cart** (jQuery-based) with no page reloads
* Supports:

  * Anonymous users (session-based)
  * Authenticated users (database-backed)
* **Automatic cart merge** after user login
* Real-time quantity update and deletion

### 👤 User Accounts

* User Registration & Authentication
* Profile Management (Avatar, Contact Information)
* Order History Tracking

### 📦 Order System

* Secure checkout process with validation
* **Automatic stock management**
* **Atomic database transactions** for data integrity

### ⚡ Performance & Optimization

* **File-based caching** for catalog categories and user orders
* **Django Debug Toolbar** for development profiling
* Optimized database queries

---

## 🛠️ Tech Stack

* **Backend:** Python 3.x, Django 4.2.7
* **Database:** PostgreSQL
* **Frontend:** HTML5, CSS3, Bootstrap 5
* **JavaScript:** jQuery (AJAX requests)
* **Image Handling:** Pillow
* **Debugging:** django-debug-toolbar

---

## ⚙️ Installation Guide

Follow the steps below to run the project locally.

---

### ✅ 1. Clone the Repository

```bash
git clone https://github.com/MeyiGi/django-home.git
cd django-home
```

---

### ✅ 2. Set Up Virtual Environment

```bash
# Windows
python -m venv venv
venv\Scripts\activate

# macOS / Linux
python3 -m venv venv
source venv/bin/activate
```

---

### ✅ 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

### ✅ 4. Database Configuration (PostgreSQL)

Make sure PostgreSQL is installed and running. Then create the database and user:

```sql
CREATE DATABASE home;
CREATE USER home WITH PASSWORD 'home';
ALTER ROLE home SET client_encoding TO 'utf8';
ALTER ROLE home SET default_transaction_isolation TO 'read committed';
ALTER ROLE home SET timezone TO 'UTC';
GRANT ALL PRIVILEGES ON DATABASE home TO home;
```

If you change these credentials, update the `DATABASES` section in:

```
app/settings.py
```

---

### ✅ 5. Apply Migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

---

### ✅ 6. Load Initial Data

```bash
python manage.py loaddata fixtures/goods/categories.json
python manage.py loaddata fixtures/goods/products.json
```

---

### ✅ 7. Create Admin User

```bash
python manage.py createsuperuser
```

---

### ✅ 8. Run the Development Server

```bash
python manage.py runserver
```

Open in your browser:

```
http://127.0.0.1:8000/
```

---

## 📂 Project Structure

```
app/        - Core project settings, URLs, WSGI/ASGI
main/       - Static pages (Home, About)
goods/      - Products, Categories, Catalog & Search
users/      - Custom User Model & Profile management
carts/      - Shopping cart logic & AJAX views
orders/     - Order processing & database models
templates/  - Django templates
static/     - CSS, JS, fonts, images
media/      - Uploaded files (product images, avatars)
```

---

## 🔍 Key Implementations

### 🔎 Full-Text Search

Located in:

```
goods/utils.py
```

Uses PostgreSQL’s `SearchVector` for:

* Multi-field searching
* Relevance ranking
* Highlighting matched words using `SearchHeadline`

---

### 🛒 Cart System

Located in:

```
carts/views.py
carts/mixins.py
```

* Implemented with a reusable `CartMixin`
* Session-based cart for guests
* Persistent database cart for authenticated users
* **Automatic cart migration after login**

---

## ⚠️ Production Deployment Notes

The current configuration is for **development only**.

Before deploying to production:

1. Set:

   ```
   DEBUG = False
   ```
2. Store sensitive values using **environment variables**:

   * `SECRET_KEY`
   * Database credentials
3. Configure:

   ```
   ALLOWED_HOSTS
   ```
4. Collect static files:

   ```bash
   python manage.py collectstatic
   ```

---

## 📜 License

© **Home Python Hub Studio** — 2023–2024
All rights reserved.
