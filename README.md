# Cold Ego

A personalized gift e commerce mobile application with a separate frontend and backend architecture.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Project Structure](#project-structure)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
- [Backend Setup](#backend-setup)
- [Frontend Setup](#frontend-setup)
- [Building Standalone Apps](#building-standalone-apps)
- [API Reference](#api-reference)
- [Deployment](#deployment)
- [Testing Workflow](#testing-workflow)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

Cold Ego is a full-stack mobile e-commerce application built for personalized gift discovery and purchasing. It features a RESTful Express.js backend powered by MongoDB Atlas and a cross-platform React Native frontend built with Expo.

---

## Features

- User authentication with secure JWT login and registration
- Product catalog with browsing and search
- Shopping cart and order management
- Product customization options per item
- Promo code and discount support
- Reviews and ratings from verified buyers
- Image uploads for products and user content
- Full admin panel for store management

---

## Project Structure

```
EGO_Project/
├── backend/
│   ├── controllers/        # Route handler logic
│   ├── models/             # Mongoose data models
│   ├── routes/             # API route definitions
│   ├── middleware/         # Auth, error, and validation middleware
│   ├── uploads/            # Multer file storage
│   ├── server.js           # App entry point
│   ├── package.json
│   ├── .env                # Environment config (never commit this)
│   └── render.yaml         # Render deployment manifest
│
└── frontend/
    ├── src/                # Screens, components, hooks, and utilities
    ├── App.js              # Root component
    ├── app.json            # Expo configuration
    ├── eas.json            # EAS Build profiles
    ├── package.json
    └── .env                # Expo environment variables
```

---

## Tech Stack

**Backend**

| Technology | Purpose |
|---|---|
| Node.js with Express.js | REST API server |
| MongoDB with Mongoose | Database and ODM |
| JSON Web Tokens | Stateless authentication |
| Multer | File and image upload handling |
| CORS | Cross-origin access for mobile clients |

**Frontend**

| Technology | Purpose |
|---|---|
| React Native with Expo | Cross-platform mobile app |
| React Navigation | In-app routing and navigation |
| Axios | HTTP client for API calls |
| EAS Build | Cloud-based APK and IPA compilation |

**Infrastructure**

| Technology | Purpose |
|---|---|
| MongoDB Atlas | Managed cloud database |
| Render | Backend hosting and deployment |
| Expo | Frontend toolchain and build platform |

---

## Getting Started

### Prerequisites

Before you begin, make sure you have the following installed:

- Node.js v18 or higher
- npm or yarn
- Expo CLI
- A MongoDB Atlas account and cluster
- An Expo account (required for EAS builds)

---

## Backend Setup

**1. Navigate to the backend directory**

```bash
cd backend
```

**2. Install dependencies**

```bash
npm install
```

**3. Configure environment variables**

Create a `.env` file in the `backend/` directory:

```env
PORT=3000
MONGO_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/<dbname>
JWT_SECRET=your_secret_key_here
```

Note: Never commit your `.env` file. Make sure it is listed in `.gitignore`.

**4. Start the development server**

```bash
npm start
```

The API will be available at `http://localhost:3000` and the health check at `http://localhost:3000/health`.

---

## Frontend Setup

**1. Navigate to the frontend directory**

```bash
cd frontend
```

**2. Install dependencies**

```bash
npm install
```

**3. Configure environment variables**

Create a `.env` file in the `frontend/` directory:

```env
EXPO_PUBLIC_API_URL=http://localhost:3000/api
```

For production, replace this with your deployed Render API URL.

**4. Start the Expo development server**

```bash
npm start
```

Scan the QR code with the Expo Go app, or press `a` for Android emulator or `i` for iOS simulator.

---

## Building Standalone Apps

EAS Build compiles your React Native app into a distributable APK for Android or IPA for iOS.

**1. Install EAS CLI globally**

```bash
npm install -g @expo/eas-cli
```

**2. Log in to your Expo account**

```bash
eas login
```

**3. Configure EAS Build**

```bash
eas build:configure
```

**4. Build for your target platform**

```bash
# Android
npm run build:android

# iOS (requires Apple Developer account)
npm run build:ios
```

Once the build completes, download the artifact from the Expo dashboard and install it on your device.

---

## API Reference

### Base URLs

| Environment | URL |
|---|---|
| Local Development | `http://localhost:3000/api` |
| Production | `https://your-app.onrender.com/api` |

### Health Check

```
GET /health
```

Returns `200 OK` when the server is running correctly.

### Authentication

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/auth/register` | Create a new user account |
| POST | `/api/auth/login` | Login and receive a JWT token |

### Products

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/products` | Get all products |
| GET | `/api/products/:id` | Get a single product |
| POST | `/api/products` | Create a product (admin only) |
| PUT | `/api/products/:id` | Update a product (admin only) |
| DELETE | `/api/products/:id` | Delete a product (admin only) |

### Orders and Cart

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/orders` | Get user orders |
| POST | `/api/orders` | Place a new order |
| GET | `/api/cart` | Get cart contents |
| POST | `/api/cart` | Add an item to the cart |

Protected routes require the header: `Authorization: Bearer <token>`

---

## Deployment

**Step 1: Deploy the backend to Render**

1. Push your code to a GitHub repository.
2. Log in to Render and create a new Web Service.
3. Connect your GitHub repository. Render will auto-detect `render.yaml`.
4. Set the following environment variables in the Render dashboard:

| Variable | Value |
|---|---|
| `MONGO_URI` | Your MongoDB Atlas connection string |
| `JWT_SECRET` | Your JWT secret key |
| `NODE_ENV` | `production` |

5. Deploy and note your API URL (e.g. `https://cold-ego.onrender.com`).

**Step 2: Update the frontend API URL**

Edit `frontend/.env`:

```env
EXPO_PUBLIC_API_URL=https://cold-ego.onrender.com/api
```

**Step 3: Build and distribute the mobile app**

```bash
cd frontend
npm run build:android
```

Download the build artifact and distribute it to your users.

---

## Testing Workflow

Follow this order before releasing a new version:

1. Run the backend locally and test all endpoints with Postman or curl.
2. Connect the frontend to the local backend and test all screens.
3. Deploy the backend to Render and verify the `/health` endpoint.
4. Update `EXPO_PUBLIC_API_URL` in `frontend/.env` to the production URL.
5. Test the frontend against the production API.
6. Run an EAS build and install it on a real device for final verification.

---

## Contributing

Contributions are welcome. To get started:

1. Fork the repository.
2. Create a feature branch: `git checkout -b feature/your-feature-name`
3. Commit your changes: `git commit -m "Add your feature"`
4. Push to your branch: `git push origin feature/your-feature-name`
5. Open a Pull Request.

Please ensure your code follows the existing style and that all features are tested before submitting.

---

## License

This project is licensed under the MIT License. See the LICENSE file for details.
