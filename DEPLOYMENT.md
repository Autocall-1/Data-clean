# 🚀 DataClean AI — Deployment Guide
## GitHub Pages (Frontend) + Render (Backend)

---

## ARCHITECTURE

```
[User Browser]
     ↓ visit
[GitHub Pages]  →  index.html (frontend)
     ↓ API calls
[Render.com]    →  FastAPI backend
     ↓ store data
[MongoDB Atlas] →  database
     ↓ store files
[Cloudinary]    →  file storage
```

---

# PART 1 — BACKEND → RENDER

## 1.1 GitHub pe Backend Upload

```bash
cd dataclean-backend

git init
git add .
git commit -m "DataClean AI Backend"

# github.com pe new repo banao: dataclean-backend
git remote add origin https://github.com/YOUR_USERNAME/dataclean-backend.git
git branch -M main
git push -u origin main
```

## 1.2 Render Deploy

1. **render.com** → Sign Up / Login
2. **"New +"** → **"Web Service"**
3. **"Connect a repository"** → GitHub connect → `dataclean-backend` select

### Settings:
| Field | Value |
|-------|-------|
| Name | `dataclean-api` |
| Region | Singapore |
| Branch | `main` |
| Runtime | Python 3 |
| Build Command | `pip install -r requirements.txt` |
| Start Command | `uvicorn main:app --host 0.0.0.0 --port $PORT` |
| Instance Type | Free |

### Environment Variables (bahut zaroori!):
| Key | Value |
|-----|-------|
| `MONGODB_URL` | `mongodb+srv://user:pass@cluster0.xxx.mongodb.net/dataclean?retryWrites=true&w=majority` |
| `MONGODB_DB_NAME` | `dataclean` |
| `SECRET_KEY` | `koi-bhi-32-char-random-string-yahan` |
| `RAZORPAY_KEY_ID` | `rzp_test_XXXXXXXXXX` |
| `RAZORPAY_KEY_SECRET` | `your_secret` |
| `ALLOWED_ORIGINS` | `https://YOUR_USERNAME.github.io` |

4. **"Create Web Service"** → ~3-5 min deploy hoga

## 1.3 Backend URL Note Karo
Deploy hone ke baad URL milega:
```
https://dataclean-api.onrender.com
```
**YEH URL SAVE KARO ← IMPORTANT**

## 1.4 Backend Test Karo
Browser mein kholo:
```
https://dataclean-api.onrender.com/docs
```
✅ Swagger UI dikhna chahiye

---

# PART 2 — FRONTEND → GITHUB PAGES

## 2.1 index.html mein URL Update Karo

`index.html` file open karo, line ~527:
```javascript
// YAHAN APNA RENDER URL DAALO ↓
const API_BASE = "https://dataclean-api.onrender.com";
```

## 2.2 GitHub pe Frontend Upload

```bash
cd dataclean-frontend

git init
git add .
git commit -m "DataClean AI Frontend"

# github.com pe new repo banao: dataclean-frontend
# IMPORTANT: Repo name aisa rakho: YOUR_USERNAME.github.io
# Ya koi bhi naam — settings mein Pages enable karenge

git remote add origin https://github.com/YOUR_USERNAME/dataclean-frontend.git
git branch -M main
git push -u origin main
```

## 2.3 GitHub Pages Enable Karo

1. GitHub pe repo open karo
2. **Settings** tab click karo
3. Left sidebar mein **"Pages"** click karo
4. Source: **"Deploy from a branch"**
5. Branch: **main** → folder: **/ (root)**
6. **"Save"** click karo
7. ~2 min baad URL milega:
   ```
   https://YOUR_USERNAME.github.io/dataclean-frontend/
   ```

## 2.4 CORS Update Karo (Render mein)

Render dashboard → dataclean-api → Environment:
```
ALLOWED_ORIGINS = https://YOUR_USERNAME.github.io
```
Save karo → Render auto-redeploy karega

---

# PART 3 — VERIFICATION

Browser mein kholo: `https://YOUR_USERNAME.github.io/dataclean-frontend/`

```
✅ Page load hoti hai
✅ "Backend online ✓" dikhta hai (green dot)
✅ Sign Up kaam karta hai
✅ Login kaam karta hai
✅ CSV upload kaam karta hai
✅ Cleaning kaam karta hai
✅ CSV download milti hai
✅ MongoDB Atlas → Browse Collections mein data dikhta hai
```

---

# TROUBLESHOOTING

### "Backend offline" dikhta hai
- Render free plan = 15 min baad sleep
- Pehli request slow hogi (cold start ~30 sec) — normal hai
- `/health` pe manually hit karo: `https://your-api.onrender.com/health`

### CORS Error (browser console mein)
- Render mein `ALLOWED_ORIGINS` check karo
- `https://` include karna zaroori hai
- Trailing slash mat daalo

### GitHub Pages 404 aa raha hai
- Repo settings → Pages → Branch: main, folder: / (root)
- `index.html` root mein hona chahiye
- 2-3 min wait karo after enabling

### MongoDB connect nahi
- Atlas → Network Access → `0.0.0.0/0` allow karo
- Connection string mein password sahi hai?
- `dataclean` database name confirm karo
