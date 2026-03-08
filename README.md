# Kevlify Authenticator

A secure, open-source **web-based** two-factor authentication (2FA) application inspired by [Stratum Auth](https://github.com/stratumauth/app).

![Kevlify Logo](client/public/images/logos/logo.png)

## 🎯 About This Project

Kevlify Authenticator is a **web implementation** of the concepts pioneered by [Stratum Auth](https://github.com/stratumauth/app), an excellent Android 2FA client. While Stratum Auth provides a robust mobile experience, Kevlify brings similar functionality to the web, making 2FA accessible from any device with a browser.

**Key Differences:**
- 🌐 **Cross-Platform**: Works on desktop, mobile, and tablets without installation
- ☁️ **Cloud-Ready**: Optional cloud sync via user accounts (Stratum is offline-first)
- 🔐 **Google OAuth**: Sign in with Google (in addition to traditional email/password)
- 🗄️ **Hybrid Database**: SQLite for local development, PostgreSQL for production

**Access the Project at:**: [Kevlify Authenticator](https://kevlify-client.onrender.com) (Note that log in with Google is still a test feature, and that this authenticator isn't registered with Google as of late, so **this feature isn't working**)

**Credit**: This project builds upon the excellent foundation and ideas from [Stratum Auth](https://github.com/stratumauth/app). We highly recommend their Android app for mobile users seeking a privacy-focused, offline-first 2FA solution.

---

## ✨ Features

### 🔐 Security & Privacy
- **Client-Side Encryption** - Secrets encrypted in your browser using AES-256-GCM
- **Zero-Knowledge Architecture** - Server cannot decrypt your OTP secrets
- **Encrypted Backups** - Export `.authpro` files with password-based encryption (PBKDF2 + AES-GCM)
- **PIN/Password Gate** - Optional UI lock for additional security (like a screen lock)
- **Role-Based Access Control** - Admin and user roles with different permissions
- **Secure Sessions** - HTTP-only, SameSite cookies with bcryptjs password hashing

### 🎨 User Experience
- **🔑 Google OAuth** - Sign in with your Google account (no password required)
- **📱 QR Code Scanning** - Add accounts by scanning QR codes with your camera
- **🎨 Theme System** - Choose between Light, Dark, or System Default themes
- **🏷️ 300+ Service Icons** - Automatic brand icon matching for popular services
- **📂 Categories** - Organize accounts into custom categories
- **🔍 Advanced Search** - Find accounts quickly with real-time search
- **✨ Smooth Animations** - Scroll-reveal animations throughout the app
- **📱 Responsive Design** - Works perfectly on desktop, tablet, and mobile

### 🛠️ Management & Compatibility
- **TOTP/HOTP Support** - Compatible with most 2FA providers (Google, Microsoft, GitHub, etc.)
- **Import/Export** - Backup and restore your authenticators
- **Account Management** - Edit, rename, reorder, and categorize accounts
- **Cloud Sync** - Optional account-based sync across devices
- **Offline Capable** - Works without internet after initial load

---

## 🚀 Tech Stack

| Component | Technology |
|-----------|------------|
| Frontend | React 18 + Vite |
| Backend | Express.js + Node.js |
| Database (Dev) | SQLite (sql.js) |
| Database (Prod) | PostgreSQL |
| Authentication | Google OAuth 2.0 + bcryptjs |
| OTP Generation | otpauth |
| QR Scanning | html5-qrcode |
| Encryption | Web Crypto API (AES-GCM + PBKDF2) |
| Testing | Playwright |
| Deployment | Render (Blueprint) |

---

## 📦 Quick Start

### Prerequisites
- Node.js 18+ and npm
- Git

### Installation

```bash
# Clone the repository
git clone https://github.com/BenjaminChristopherHermesB/kevlify-auth.git
cd kevlify-auth

# Install all dependencies (client + server)
npm run install:all

# Set up environment variables
cp server/.env.example server/.env
cp client/.env.example client/.env
# Edit .env files with your configuration

# Start development servers
npm run dev
```

The app will be available at kevlify-client.onrender.com/

For detailed setup instructions, see [docs/SETUP.md](docs/SETUP.md).

---

## 📁 Project Structure

```
kevlify-authenticator/
├── client/                 # React frontend (Vite)
│   ├── src/
│   │   ├── components/     # UI components (Header, Footer, Modal, etc.)
│   │   ├── pages/          # Page components (Home, Login, Authenticator, etc.)
│   │   ├── context/        # React contexts (AuthContext, PinLockContext)
│   │   ├── services/       # API client
│   │   ├── utils/          # Encryption, icon utilities
│   │   └── styles/         # CSS files
│   └── public/
│       └── images/
│           ├── icons/      # 300+ service brand icons
│           └── logos/      # Kevlify logos
├── server/                 # Express backend
│   ├── routes/             # API routes (auth, accounts, categories, backup, admin)
│   ├── middleware/         # Auth middleware with role support
│   └── db/                 # Database layer (SQLite/PostgreSQL)
├── tests/                  # Playwright E2E tests
├── docs/                   # Documentation
│   ├── deployment/         # Deployment guides
│   ├── architecture.md     # System architecture
│   ├── api.md              # API documentation
│   ├── security.md         # Security details
│   └── SETUP.md            # Setup guide
└── render.yaml             # Render Blueprint config
```

---

## 🌐 Pages

| Page | Route | Description |
|------|-------|-------------|
| Home | `/` | Landing page with features |
| About | `/about` | About Kevlify, features, security info |
| Contact | `/contact` | Team information and values |
| Login | `/login` | User login (email or Google) |
| Register | `/register` | User registration |
| Authenticator | `/app` | Main 2FA dashboard (protected) |
| Settings | `/settings` | User settings, backup/restore (protected) |

---

## 🧪 Testing

```bash
# Install Playwright browsers
npx playwright install

# Run all E2E tests
npm run test:e2e

# Run tests with UI
npm run test:e2e:ui

# Run specific test file
npm run test:e2e -- tests/auth.spec.js
```

---

## 🚀 Deployment

Kevlify is designed for easy deployment to [Render](https://render.com) using our Blueprint configuration.

### Quick Deploy

1. Push your code to GitHub
2. Connect repository to Render
3. Render will auto-create both services (backend + frontend)
4. Configure environment variables
5. Deploy!

For detailed deployment instructions, see:
- **[Deployment Documentation](docs/deployment/)** - Complete deployment guides
- **[Render Blueprint Guide](docs/deployment/render-blueprint.md)** - Step-by-step Blueprint deployment
- **[Google OAuth Setup](docs/deployment/auth-setup.md)** - Configure Google Sign-In
- **[Post-Deployment Guide](docs/deployment/post-deploy.md)** - Testing and maintenance

---

## 🔒 Security

Kevlify implements multiple layers of security:

- **Password Hashing**: bcryptjs with 12 rounds
- **Session Management**: Secure, HTTP-only, SameSite=None cookies
- **Client-Side Encryption**: AES-256-GCM with PBKDF2 key derivation (100k iterations)
- **Zero-Knowledge Architecture**: Server cannot decrypt your OTP secrets
- **Role-Based Access Control**: Admin and user roles
- **CORS Protection**: Configured for cross-origin security
- **Helmet.js**: Security headers for Express

For detailed security information, see [docs/security.md](docs/security.md).

---

## 🎨 Design Philosophy

The UI is inspired by modern web design principles:
- Clean, minimalist interface
- Smooth scroll-reveal animations
- Responsive grid layouts
- Blue accent color palette (#3b82f6)
- Dark mode support

---

## 📚 Documentation

- **[Setup Guide](docs/SETUP.md)** - Installation and configuration
- **[Deployment Guides](docs/deployment/)** - Deploy to production
- **[API Documentation](docs/api.md)** - REST API reference
- **[Architecture](docs/architecture.md)** - System design
- **[Security](docs/security.md)** - Security implementation details

---

## 👥 Authors

- **B C H Benjamin** - Developer
- **C Yogeetha** - Developer

Built at Atria Institute of Technology.

---

## 🙏 Acknowledgments

This project is inspired by and builds upon the excellent work of:
- **[Stratum Auth](https://github.com/stratumauth/app)** - The original Android 2FA client that inspired this web implementation
- The open-source community for various libraries and tools

---

## 📄 License

GPL-3.0 - See [LICENSE](LICENSE) for details.

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

---

## 🤝 Contributing

Contributions are welcome! Please:
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 🔗 Links

- **Live Demo**: [Coming Soon]
- **GitHub**: [kevlify-auth](https://github.com/BenjaminChristopherHermesB/kevlify-auth)
- **Stratum Auth** (Inspiration): [stratumauth/app](https://github.com/stratumauth/app)

