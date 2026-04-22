# Deployment Guide

This project is structured for easy deployment with the frontend on **Vercel** and the backend on **Render**.

## 1. Backend Deployment (Render)

1.  Create a new project on [Render](https://render.com/).
2.  Connect your GitHub repository.
3.  Set the **Root Directory** to `backend`.
4.  Set the **Build Command** to `npm install`.
5.  Set the **Start Command** to `npm start`.
6.  Add the following **Environment Variables** in Render:
    *   `MONGODB_URI`: Your MongoDB connection string (from MongoDB Atlas).
    *   `JWT_SECRET`: A long, random string (e.g., `Chat4U_Secret_789_!@#_Secure_Key_2026`). You create this yourself.
    *   `CLOUDINARY_CLOUD_NAME`: Found at the top of your Cloudinary dashboard (e.g., `dozmok2uy`).
    *   `CLOUDINARY_API_KEY`: From Cloudinary "API Keys" section.
    *   `CLOUDINARY_API_SECRET`: From Cloudinary "API Keys" section.
    *   `CLIENT_URL`: The URL of your frontend (e.g., `https://chat4-u.vercel.app`).
    *   `NODE_ENV`: `production`

## 2. Frontend Deployment (Vercel)

1.  Create a new project on [Vercel](https://vercel.com/).
2.  Connect your GitHub repository.
3.  Set the **Root Directory** to `frontend`.
4.  Vercel should automatically detect **Vite** as the framework.
5.  Add the following **Environment Variable** in Vercel:
    *   `VITE_API_BASE_URL`: Your backend URL followed by `/api` (e.g., `https://chat4u.onrender.com/api`).
6.  Update `frontend/vercel.json`:
    *   The `destination` URLs should point to your actual Render backend URL.

## Important Notes

*   **Cookies**: The backend is configured to use `sameSite: "none"` and `secure: true` in production, which is required for cross-domain cookies to work between Vercel and Render.
*   **CORS**: Ensure `CLIENT_URL` in the backend matches your Vercel deployment URL exactly (without a trailing slash).
*   **Socket.IO**: The frontend automatically derives the Socket.IO connection URL from `VITE_API_BASE_URL`.
