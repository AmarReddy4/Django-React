# Django-React

A full-stack e-commerce web application with a Django REST Framework backend and a React frontend. Supports user registration and authentication, product browsing by category, shopping cart management, and secure checkout via the Braintree payment gateway.

## Tech Stack

### Backend
- **Framework:** Django 4.2 with Django REST Framework 3.15
- **Language:** Python 3.11
- **Database:** SQLite (default)
- **Authentication:** Token-based authentication (DRF AuthToken) with custom session tokens
- **Payment Gateway:** Braintree (Sandbox)
- **Image Handling:** Pillow
- **CORS:** django-cors-headers
- **Package Manager:** Pipenv

### Frontend
- **Framework:** React 16
- **State Management:** React hooks
- **Routing:** React Router

## Features

### User Features
- Sign up with email, name, phone, and gender
- Sign in / sign out with session token management
- Browse products from the home page
- Add and remove products from the shopping cart
- View grand total of cart items
- Pay securely using any bank card via Braintree payment gateway
- Place orders with transaction tracking

### Admin Features (Django Admin Panel)
- Add, edit, and remove product categories
- Add, edit, and remove products (with image, price, stock, and category)
- Manage user accounts
- View and manage all orders

## Project Structure

```
Django-React/
├── Pipfile                         # Python dependencies
├── ecom/                           # Django project root
│   ├── manage.py
│   ├── db.sqlite3
│   ├── media/                      # Uploaded product images
│   ├── ecom/
│   │   ├── settings.py             # Django settings (DB, auth, CORS, DRF config)
│   │   ├── urls.py                 # Root URL configuration
│   │   └── wsgi.py
│   └── api/                        # Main API app
│       ├── urls.py                 # API route definitions
│       ├── views.py                # API home view
│       ├── category/
│       │   ├── models.py           # Category model (name, description)
│       │   ├── serializers.py
│       │   ├── views.py            # CategoryViewSet (ModelViewSet)
│       │   └── urls.py
│       ├── product/
│       │   ├── models.py           # Product model (name, description, price, stock, image, category FK)
│       │   ├── serializers.py
│       │   ├── views.py            # ProductViewSet (ModelViewSet)
│       │   └── urls.py
│       ├── user/
│       │   ├── models.py           # CustomUser model (extends AbstractUser, email as username)
│       │   ├── serializers.py
│       │   ├── views.py            # UserViewSet, signin, signout
│       │   └── urls.py
│       ├── order/
│       │   ├── models.py           # Order model (user, products, transaction_id, total_amount)
│       │   ├── serializers.py
│       │   ├── views.py            # OrderViewSet, add order with session validation
│       │   └── urls.py
│       └── payment/
│           ├── views.py            # Braintree token generation and payment processing
│           └── urls.py
└── devfront/                       # React frontend (if present)
```

## API Endpoints

All endpoints are prefixed with `/api/`.

### Authentication
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/user/login/` | Sign in with email and password, returns session token |
| GET | `/api/user/logout/<id>/` | Sign out and invalidate session token |
| POST | `/api/api-token-auth/` | Obtain DRF auth token |

### Users
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/user/` | List all users |
| POST | `/api/user/` | Register a new user |
| GET | `/api/user/<id>/` | Get user details |
| PUT | `/api/user/<id>/` | Update user |
| DELETE | `/api/user/<id>/` | Delete user |

### Categories
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/category/` | List all categories |
| POST | `/api/category/` | Create a category |
| GET | `/api/category/<id>/` | Get category details |
| PUT | `/api/category/<id>/` | Update a category |
| DELETE | `/api/category/<id>/` | Delete a category |

### Products
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/product/` | List all products |
| POST | `/api/product/` | Create a product |
| GET | `/api/product/<id>/` | Get product details |
| PUT | `/api/product/<id>/` | Update a product |
| DELETE | `/api/product/<id>/` | Delete a product |

### Orders
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/order/` | List all orders |
| POST | `/api/order/add/<id>/<token>/` | Place an order (session-validated) |

### Payments
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/payment/gettoken/<id>/<token>/` | Get Braintree client token |
| POST | `/api/payment/process/<id>/<token>/` | Process payment via Braintree |

## Getting Started

### Prerequisites
- Python 3.11+
- Pipenv
- Node.js (for the React frontend)

### Backend Setup

1. Navigate to the project root and install Python dependencies:
   ```bash
   pipenv install
   ```

2. Activate the virtual environment:
   ```bash
   pipenv shell
   ```

3. Navigate to the Django project directory:
   ```bash
   cd ecom
   ```

4. Run database migrations:
   ```bash
   python manage.py migrate
   ```

5. Create a superuser for the admin panel:
   ```bash
   python manage.py createsuperuser
   ```

6. Start the Django development server:
   ```bash
   python manage.py runserver
   ```
   The API will be available at `http://localhost:8000/api/` and the admin panel at `http://localhost:8000/admin/`.

### Frontend Setup

1. Navigate to the frontend directory:
   ```bash
   cd devfront
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the React development server:
   ```bash
   npm start
   ```

### Admin Panel

Access the Django admin at `http://localhost:8000/admin/` using your superuser credentials. From here you can:
- Add and manage product categories
- Add products with images, prices, and stock levels
- View and manage user accounts
- View and manage orders
