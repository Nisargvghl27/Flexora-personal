# 🌸 Flexora - Fashion, Lookbooks, Blog, and Community Platform

Welcome to **Flexora**, a premium student-focused fashion and lifestyle ecosystem. Flexora enables students, young designers, and fashion enthusiasts to discover their style personas through interactive quizzes, create custom digital lookbooks, read and publish engaging fashion blogs, shop a curated catalog, and participate in a vibrant community.

The project is structured as a full-stack monorepo featuring a **Django REST Framework (DRF) backend** and a **Vite + React + TypeScript + Tailwind CSS frontend**.

---

## 🎨 Design & Key Features

*   **Interactive Fashion Quiz**: Discover your fashion archetype (Minimalist, Bohemian, Vintage, Casual, Streetwear, Formal) dynamically.
*   **Custom Digital Lookbooks**: Personalize collections based on your style persona, add/remove curated products, and rearrange the items in your lookbook.
*   **Dynamic Blogging Workspace**: Read trending articles and publish your own style insights. Features full engagement metrics such as likes, views, comments, and specific category filters.
*   **E-Commerce Shop**: Browse categorized fashion products, view details, manage a persistent shopping cart, place mock orders, and view order history.
*   **Student Spotlights & Community Hub**: Dedicated showcase profiles for student designers, signups for newsletter subscriptions, and community memberships.
*   **Premium Interactive UI**: Implements glassmorphic elements, vibrant color aesthetics, custom user avatars, responsive layouts, and smooth animations using **Framer Motion** and **Sonner** notifications.
*   **Authentication & Security**: Fully secured via **JWT Authentication** (SimpleJWT), including profile updates, password changes, username availability checking, and safe account deletion.

---

## 🛠️ Technology Stack

### Frontend
*   **Core**: [React](https://react.dev/) + [TypeScript](https://www.typescriptlang.org/) + [Vite](https://vitejs.dev/)
*   **Styling**: [Tailwind CSS](https://tailwindcss.com/) + [Shadcn/UI](https://ui.shadcn.com/) (Radix primitives)
*   **Animations**: [Framer Motion](https://www.framer.com/motion/)
*   **State & Networking**: [TanStack Query (React Query)](https://tanstack.com/query/latest) + [Axios](https://axios-http.com/)
*   **Routing**: [React Router v6](https://reactrouter.com/)
*   **Notifications & Forms**: [Sonner](https://seed.run/) + [React Hook Form](https://react-hook-form.com/) + [Zod](https://zod.dev/)

### Backend
*   **Core**: [Django 5.2](https://www.djangoproject.com/) + [Django REST Framework (DRF) 3.15](https://www.django-rest-framework.org/)
*   **Authentication**: [SimpleJWT](https://django-rest-framework-simplejwt.readthedocs.io/en/latest/) (JSON Web Tokens)
*   **Database**: [PostgreSQL](https://www.postgresql.org/) (Production/Default) or [SQLite](https://www.sqlite.org/) (Local Fallback)
*   **Storage**: [Cloudinary](https://cloudinary.com/) (for profile photos, blog cover images, and product assets)
*   **Integrations**: [Razorpay](https://razorpay.com/) Payment Gateway API
*   **Utilities**: `python-decouple`, `dj-database-url`, `Pillow`, `django-cors-headers`

---

## 📁 Project Structure

```
Flexora/
├── backend/                       # Django Backend App
│   ├── api/                       # API application (Models, Views, Serializers, URLs)
│   │   ├── migrations/            # Django migrations directory
│   │   ├── admin.py               # Django Admin configuration
│   │   ├── models.py              # Database models (UserProfile, Product, Blog, Lookbook, CommunityMember)
│   │   ├── serializers.py         # DRF Serializers
│   │   ├── views.py               # Controller logic / API view classes
│   │   └── urls.py                # App-specific URL mapping
│   ├── core/                      # Project configuration (settings.py, urls.py, wsgi.py)
│   ├── setup_database.py          # PostgreSQL Database and configuration setup helper
│   ├── test_suite.py              # Suite to test core authentication and suggestions functionality
│   ├── manage.py                  # Django management CLI
│   └── requirements.txt           # Backend python dependencies
├── frontend/                      # React Frontend App
│   ├── src/
│   │   ├── components/            # Reusable UI components (Navbar, Footer, loading, style quiz)
│   │   ├── pages/                 # Routing pages (Home, Cart, Profile, WriteBlog, StudentSpotlights, etc.)
│   │   │   ├── categories/        # Dedicated style category subpages
│   │   │   ├── collections/       # Curated collections pages (Summer Vibes, Minimalist Elegance, etc.)
│   │   │   ├── students/          # Individual Student Spotlight profiles
│   │   │   └── trending/          # Individual trending fashion blog styles
│   │   ├── services/              # API Client interfaces and helper methods
│   │   ├── styles/                # Styling stylesheets (index.css, main.css)
│   │   ├── App.tsx                # Main Routing & Provider Assembly
│   │   └── main.tsx               # Entry point
│   ├── package.json               # Frontend node dependencies
│   ├── tailwind.config.ts         # Tailwind configuration
│   └── vite.config.ts             # Vite bundler options
├── requirements.txt               # Global python dependencies
└── test_registration.py           # Endpoint integration test for Registration API
```

---

## ⚙️ Backend Setup & Configuration

### 1. Prerequisites
Ensure you have the following installed on your machine:
*   [Python 3.10+](https://www.python.org/downloads/)
*   [PostgreSQL](https://www.postgresql.org/download/) (running locally) *or* configure the project to use SQLite instead.

### 2. Configure Environment Variables (`.env`)
Create a `.env` file in the `backend/` directory (or use the helper script below to generate it). The file must contain:

```env
# PostgreSQL Config
DB_NAME=flexora_db
DB_USER=postgres
DB_PASSWORD=your_postgres_password
DB_HOST=localhost
DB_PORT=5432

# Django Settings
SECRET_KEY=django-insecure-your-secret-key
DEBUG=True

# Cloudinary Storage
CLOUDINARY_CLOUD_NAME=dlpuuekkl
CLOUDINARY_API_KEY=474816865319319
CLOUDINARY_API_SECRET=OqVqRF4FwbBhAEH_xtzSnl2aU28

# JWT Settings
JWT_SECRET_KEY=your-jwt-secret-key-here
JWT_ACCESS_TOKEN_LIFETIME=5
JWT_REFRESH_TOKEN_LIFETIME=1
```

### 3. Quickstart: Automatic Setup Script
The project includes a `setup_database.py` script that automatically creates the PostgreSQL database and user, generates the `.env` file, runs migrations, creates a default superuser, and seeds mock data.

Run the following inside the `backend` directory:
```bash
python setup_database.py
```
*   **Default Superuser Credentials created by script**:
    *   **Username**: `admin`
    *   **Password**: `admin123`
    *   **Email**: `admin@flexora.com`

### 4. Alternative: Local SQLite Setup
If you want to run the project locally using SQLite instead of PostgreSQL:
1. Set the `USE_SQLITE` environment variable to `true`:
   * **Windows (PowerShell)**: `$env:USE_SQLITE="true"`
   * **Linux/macOS (Bash)**: `export USE_SQLITE=true`
2. Run standard Django commands to migrate and seed:
   ```bash
   python manage.py migrate
   python manage.py createsuperuser
   python manage.py populate_trending_posts # Seeds trending blogs
   ```

### 5. Running the Backend Server
Start the Django development server:
```bash
python manage.py runserver
```
The backend API is now running at `http://localhost:8000/`. You can view the admin portal at `http://localhost:8000/admin/`.

---

## 💻 Frontend Setup & Development

### 1. Prerequisites
*   [Node.js](https://nodejs.org/) (v18+)
*   [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)

### 2. Installation
Navigate to the `frontend/` directory and install the required dependencies:
```bash
cd frontend
npm install
```

### 3. Run Development Server
Start the Vite local development server:
```bash
npm run dev
```
The frontend application will compile and become accessible at `http://localhost:5173/` or `http://localhost:5174/`.

---

## 🔌 API Endpoints Summary

All APIs are prefixed with `/api/`. Below is a reference of the primary endpoints:

| Endpoint | Method | Authentication | Description |
| :--- | :--- | :--- | :--- |
| `/api/register/` | `POST` | None | Create a new user account |
| `/api/login/` | `POST` | None | Login user & retrieve access/refresh JWT tokens |
| `/api/profile/` | `GET` / `PUT` | JWT | Get or update profile, address, and avatar |
| `/api/delete-account/` | `DELETE` | JWT | Delete user profile and deactivate account |
| `/api/change-password/` | `POST` | JWT | Change user password |
| `/api/usernames/?search=<str>`| `GET` | None | Verify username suggestions for registration |
| `/api/products/` | `GET` | None | List products, with search and category filtering |
| `/api/products/<uuid>/` | `GET` | None | Fetch detailed info of a single product |
| `/api/blogs/` | `GET` | None | List blog articles (supports trending and category filter) |
| `/api/blogs/create/` | `POST` | JWT | Write and publish a new blog post |
| `/api/blogs/<slug>/` | `GET` | None | Fetch details for a specific blog article |
| `/api/blogs/<id>/engagement/`| `POST` | None / JWT | Log engagement metrics (increment likes, views, comments) |
| `/api/lookbooks/style/<style>/` | `GET` | JWT | Retrieve/Create user's lookbook for specific Style Persona |
| `/api/lookbooks/<id>/items/` | `POST` | JWT | Add a product item to a specific lookbook |
| `/api/lookbooks/<id>/items/<item_id>/`| `DELETE` | JWT | Remove a product item from a lookbook |
| `/api/join-community/` | `POST` | JWT | Register as a community member with interests and newsletter option |
| `/api/create-razorpay-order/` | `POST` | JWT | Initialize a payment checkout order with Razorpay |
| `/api/verify-razorpay-payment/` | `POST` | JWT | Verify digital signature of payment signature |

---

## 🧪 Testing

The codebase includes verification test suites:

1.  **Backend Integrity Tests**: Runs custom tests for authorization and username recommendation logic.
    ```bash
    cd backend
    python test_suite.py
    ```
2.  **API Integration Test**: A standalone HTTP check utility verifying registration handling. Ensure the backend server is running, then invoke:
    ```bash
    python test_registration.py
    ```
3.  **Django Test Commands**:
    ```bash
    python manage.py test api
    ```

---

*Flexora represents the intersection of fashion, community, and tech. Create your style profile today!*
