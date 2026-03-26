# Andre Huang — Portfolio Website

A modern, fully responsive personal portfolio website for **Andre Huang**, a Software Development student at ROC van Twente. The site showcases projects, skills, certificates, and contact information, and includes a PHP/MySQL-powered user authentication system with account management.

---

## 📋 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Usage](#-usage)
- [Theme System](#-theme-system)
- [Security](#-security)
- [Responsive Breakpoints](#-responsive-breakpoints)
- [Database Schema](#-database-schema)
- [Troubleshooting](#-troubleshooting)
- [Contributing](#-contributing)
- [License](#-license)
- [Author](#-author)
- [Acknowledgments](#-acknowledgments)

---

## ✨ Features

| Feature | Description |
|---|---|
| **Dark / Light Mode** | Toggle switch in the navbar; preference is persisted via `localStorage` |
| **Fully Responsive** | Mobile-first layout that adapts to all screen sizes using Bootstrap 5 |
| **Project Showcase** | Interactive project gallery with dedicated detail pages and image lightbox |
| **Skills Section** | Animated progress-bar skill cards (HTML, PHP, CSS, Bootstrap, JavaScript, C#) |
| **Certificates Section** | Cards for earned certifications and diplomas |
| **Contact Form** | Form with client-side validation and a confirmation modal before submission |
| **User Authentication** | Complete register / login / logout flow backed by a PHP + MySQL API |
| **Account Management** | Authenticated users can view and update their name and email address |
| **Shared Components** | Header and footer are dynamically injected via `fetch()`, keeping markup DRY |
| **Image Lightbox** | Click any zoomable image to view it full-screen; close with ESC or a button |
| **AOS Animations** | Scroll-triggered entrance animations powered by the AOS library |
| **Custom Error Pages** | Branded 403, 404, and 500 error pages configured in `.htaccess` |

---

## 🚀 Tech Stack

### Frontend

| Technology | Version | Purpose |
|---|---|---|
| HTML5 | — | Semantic page structure |
| CSS3 | — | Custom properties, transitions, responsive styles |
| JavaScript | ES6+ | Theme toggle, component loading, lightbox, forms |
| [Bootstrap](https://getbootstrap.com/) | 5.3.0 | Responsive grid and UI components |
| [Bootstrap Icons](https://icons.getbootstrap.com/) | 1.11.3 | Icon library |
| [AOS](https://michalsnik.github.io/aos/) | next | Animate-on-scroll effects |
| [Google Fonts – Poppins](https://fonts.google.com/specimen/Poppins) | — | Typography |

### Backend

| Technology | Purpose |
|---|---|
| PHP 7+ | REST-style JSON API endpoints (auth & user management) |
| MySQL | Relational database for user accounts |
| PDO | Database abstraction with prepared statements |
| PHP Sessions | Server-side authentication state |
| Apache / XAMPP | Local development server with `.htaccess` configuration |

---

## 📁 Project Structure

```
portfolio/
├── backend/
│   ├── auth/
│   │   ├── login.php           # POST: authenticate a user, start session
│   │   ├── register.php        # POST: create a new user account
│   │   └── logout.php          # Destroy session and redirect to login
│   ├── user/
│   │   ├── get_account.php     # GET: return current user's profile (JSON)
│   │   └── update_account.php  # POST: update name / email for logged-in user
│   ├── config/
│   │   └── database.php        # PDO connection + session_start()
│   └── database.sql            # Database and table schema + sample data
├── css/
│   ├── style.css               # Global stylesheet with CSS custom properties
│   ├── login.css               # Styles specific to the login/register page
│   └── project-detail.css      # Styles for project detail pages
├── html/
│   ├── index.html              # Main portfolio page (About, Skills, Projects, Contact)
│   ├── login.html              # Login / Register tab interface
│   ├── account_details.html    # Profile view and edit form (auth required)
│   ├── webshop.html            # Project detail: PHP Web Shop
│   ├── top2000-platform.html   # Project detail: Top2000 Music Platform
│   ├── responsive-design.html  # Project detail: Bootstrap Responsive Design
│   ├── project-wip.html        # Project placeholder (Work in Progress)
│   ├── 403.html                # Custom Forbidden error page
│   ├── 404.html                # Custom Not Found error page
│   ├── 500.html                # Custom Internal Server Error page
│   └── shared/
│       ├── header.html         # Shared navigation bar (loaded via JS)
│       └── footer.html         # Shared footer (loaded via JS)
├── js/
│   ├── script.js               # Theme toggle, dynamic header/footer, lightbox, contact form
│   └── auth.js                 # AJAX handlers for login and registration forms
├── image/
│   ├── bootstrap/              # Screenshots for the Responsive Design project
│   ├── homepage/               # Profile photo
│   ├── top2000/                # Screenshots for the Top2000 project
│   └── webshop/                # Screenshots for the Web Shop project
├── favicon/
│   └── favicon.svg             # SVG site favicon
├── index.html                  # Root entry point (loads the portfolio)
├── .htaccess                   # Custom error pages, directory protection, .git block
└── README.md
```

---

## 🛠️ Installation

### Prerequisites

- **[XAMPP](https://www.apachefriends.org/)** (Apache + MySQL + PHP 7+)
- A modern web browser (Chrome, Firefox, Edge, Safari)
- [Git](https://git-scm.com/) *(optional, for cloning)*

### Step 1 — Clone the Repository

```bash
git clone https://github.com/Andre-bit-coder/portfolio.git
```

### Step 2 — Copy to the XAMPP Web Root

**Windows:**
```bash
xcopy /E /I portfolio "C:\xampp\htdocs\portfolio"
```

**macOS / Linux:**
```bash
cp -r portfolio /opt/lampp/htdocs/portfolio
```

### Step 3 — Start XAMPP Services

1. Open the **XAMPP Control Panel**.
2. Click **Start** next to **Apache**.
3. Click **Start** next to **MySQL**.

### Step 4 — Import the Database

**Option A – via the command line:**
```bash
mysql -u root -p < backend/database.sql
```

**Option B – via phpMyAdmin:**
1. Open [http://localhost/phpmyadmin](http://localhost/phpmyadmin).
2. Click **Import**.
3. Select `backend/database.sql` and click **Go**.

This creates the `portfolio_db` database and a `users` table, and inserts one sample user.

---

## ⚙️ Configuration

Open `backend/config/database.php` and adjust the constants to match your MySQL setup:

```php
define('DB_HOST', 'localhost');
define('DB_NAME', 'portfolio_db');
define('DB_USER', 'root');
define('DB_PASS', '');       // Set your MySQL password here if applicable
```

> **Note:** The `.htaccess` file blocks direct HTTP access to `database.php` for security. Never expose credentials in a public repository.

---

## 🎮 Usage

### Accessing the Website

| Page | URL |
|---|---|
| Homepage | `http://localhost/portfolio/index.html` |
| Login / Register | `http://localhost/portfolio/html/login.html` |
| Account Details | `http://localhost/portfolio/html/account_details.html` |

### Demo Account

After importing the database, a sample account is available:

| Field | Value |
|---|---|
| **Email** | `andre@example.com` |
| **Password** | `password123` |

### Feature Walkthroughs

#### Dark / Light Mode
1. Locate the toggle switch in the top-right corner of the navigation bar.
2. Click to switch between dark (default) and light themes.
3. Your preference is automatically saved and restored on your next visit.

#### Browsing Projects
1. Scroll to the **My Projects** section on the homepage.
2. Click any project card to open its dedicated detail page.
3. On detail pages, click any screenshot to open it in the full-screen lightbox. Press **Esc** or the **×** button to close.

#### Contact Form
1. Scroll to the **Contact Me** section.
2. Fill in your name, email, subject, and message.
3. Click **Send Message** — a confirmation modal will appear before the message is submitted.

#### Registering an Account
1. Navigate to the **Login** page.
2. Switch to the **Register** tab.
3. Enter your full name, email, and a password of at least 8 characters.
4. Click **Register**; on success you will be automatically switched to the Login tab.

> **Note:** The login flow is currently marked as *coming soon* in the UI. Registration is fully functional through the PHP backend.

#### Editing Your Profile
1. Log in and navigate to **Account Details**.
2. Your name, email, and registration date are displayed.
3. Click **Edit Profile** to expand the edit form.
4. Update your name and/or email, then click **Save Changes**.

---

## 🎨 Theme System

The site uses CSS Custom Properties for theming. Dark mode is the default; adding the `light-mode` class to `<body>` switches the palette.

```css
/* Dark Mode — default */
:root {
  --primary-color:   #4e54c8;
  --secondary-color: #8f94fb;
  --bg-color:        #121212;
  --card-bg:         #1e1e1e;
  --text-color:      #e0e0e0;
  --text-muted:      #a0a0a0;
  --border-color:    rgba(255, 255, 255, 0.1);
  --input-bg:        #2a2a2a;
  --navbar-bg:       rgba(18, 18, 18, 0.85);
}

/* Light Mode */
body.light-mode {
  --bg-color:     #f4f7f6;
  --card-bg:      #ffffff;
  --text-color:   #333333;
  --text-muted:   #6c757d;
  --border-color: rgba(0, 0, 0, 0.1);
  --input-bg:     #ffffff;
  --navbar-bg:    rgba(255, 255, 255, 0.85);
}
```

The selected theme is stored in `localStorage` under the key `theme` and re-applied on every page load.

---

## 🔐 Security

| Measure | Implementation |
|---|---|
| Password hashing | `password_hash()` with `PASSWORD_DEFAULT` (bcrypt) |
| SQL injection prevention | PDO prepared statements with bound parameters throughout all queries |
| Session-based authentication | PHP `$_SESSION` checked on every protected endpoint |
| Input validation | Client-side (HTML5 + JavaScript) **and** server-side (PHP `filter_var`, `strlen`) |
| Directory listing disabled | `Options -Indexes` in `.htaccess` |
| Config file protection | `<Files "database.php">` block in `.htaccess` prevents direct HTTP access |
| `.git` folder blocked | `RedirectMatch 404 /\.git` in `.htaccess` |
| Hidden files blocked | `<FilesMatch "^\\.">` directive denies access to dot-files |
| Custom error pages | 403 / 404 / 500 pages prevent information leakage from default server errors |

---

## 📱 Responsive Breakpoints

| Breakpoint | Width |
|---|---|
| Mobile | < 768 px |
| Tablet | 768 px – 992 px |
| Desktop | > 992 px |

---

## 📝 Database Schema

```sql
CREATE DATABASE IF NOT EXISTS portfolio_db
  CHARACTER SET utf8mb4
  COLLATE utf8mb4_unicode_ci;

USE portfolio_db;

CREATE TABLE IF NOT EXISTS users (
  id         INT AUTO_INCREMENT PRIMARY KEY,
  name       VARCHAR(100) NOT NULL,
  email      VARCHAR(150) UNIQUE NOT NULL,
  password   VARCHAR(255) NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  INDEX idx_email (email)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
```

---

## 🐛 Troubleshooting

### Apache Won't Start
```bash
# Windows — check what is using port 80
netstat -ano | findstr :80

# Stop IIS if it is occupying the port
net stop w3svc
```

### Database Connection Error
- Confirm MySQL is running in the XAMPP Control Panel.
- Double-check credentials in `backend/config/database.php`.
- Verify that the `portfolio_db` database was created by importing `database.sql`.

### 404 Errors on Backend Endpoints
- Make sure the project folder is inside `htdocs/` (e.g., `C:\xampp\htdocs\portfolio`).
- Confirm Apache is running.
- Check that the AJAX request paths in the JavaScript files match your folder name.

### Dark Mode Not Working
- Open DevTools → Application → Local Storage and clear the `theme` key.
- Check the browser console for JavaScript errors.
- Verify that `js/script.js` is loaded (Network tab).

---

## 🤝 Contributing

1. Fork the repository.
2. Create a feature branch:
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. Commit your changes:
   ```bash
   git commit -m "Add your feature description"
   ```
4. Push to the branch:
   ```bash
   git push origin feature/your-feature-name
   ```
5. Open a Pull Request.

---

## 📄 License

This project is licensed under the **MIT License**.

---

## 👤 Author

**Andre Huang**

- 🌐 Portfolio: [andrehuang.nl](https://andrehuang.nl)
- 💼 LinkedIn: [linkedin.com/in/andre-huang-0b2843293](https://www.linkedin.com/in/andre-huang-0b2843293/)
- 📸 Instagram: [@hypo.andy](https://www.instagram.com/hypo.andy/)
- 🐙 GitHub: [@hypox](https://github.com/hypox)

---

## 🙏 Acknowledgments

- [Bootstrap](https://getbootstrap.com/) — responsive UI framework
- [Bootstrap Icons](https://icons.getbootstrap.com/) — icon set
- [AOS Library](https://michalsnik.github.io/aos/) — scroll animations
- [Google Fonts](https://fonts.google.com/) — Poppins typeface
- [XAMPP](https://www.apachefriends.org/) — local development environment
  