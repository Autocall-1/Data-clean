# 🔥 Firebase Setup Guide — 10 min mein complete

---

## STEP 1 — Firebase Project Banao
1. https://console.firebase.google.com → **"Create a project"**
2. Project name: `dataclean-ai`
3. Google Analytics: disable karo
4. **"Create project"** → Continue

## STEP 2 — Web App Register Karo
1. Project dashboard pe **`</>`** (Web) icon click karo
2. App nickname: `DataClean Frontend`
3. **"Register app"** → Firebase SDK config copy karo:
```javascript
const firebaseConfig = {
  apiKey:            "AIzaSy...",
  authDomain:        "dataclean-ai.firebaseapp.com",
  projectId:         "dataclean-ai",
  storageBucket:     "dataclean-ai.appspot.com",
  messagingSenderId: "123456789",
  appId:             "1:123456:web:abc123"
};
```

## STEP 3 — Email/Password Auth Enable Karo
1. Left sidebar → **Authentication** → **"Get started"**
2. **Sign-in method** tab
3. **Email/Password** → Enable → Save

## STEP 4 — Authorized Domains Add Karo
1. Authentication → **Settings** tab → **"Authorized domains"**
2. **"Add domain"** click karo
3. Add: `YOUR_USERNAME.github.io`

## STEP 5 — index.html mein Config Daalo
`index.html` mein yeh section update karo:
```javascript
const firebaseConfig = {
  apiKey:            "STEP 2 WALA VALUE",
  authDomain:        "STEP 2 WALA VALUE",
  projectId:         "STEP 2 WALA VALUE",
  storageBucket:     "STEP 2 WALA VALUE",
  messagingSenderId: "STEP 2 WALA VALUE",
  appId:             "STEP 2 WALA VALUE"
};
```

## STEP 6 — Service Account (Backend ke liye)
1. Firebase Console → Project Settings (gear icon)
2. **"Service accounts"** tab
3. **"Generate new private key"** → JSON download hoga
4. Yeh JSON file ka content copy karo

### Render pe set karo:
Environment Variable:
```
FIREBASE_SERVICE_ACCOUNT_JSON = { "type": "service_account", ... poora JSON }
```

---

## STEP 7 — Render URL Frontend mein Daalo
`index.html` mein:
```javascript
window.API_BASE = "https://dataclean-api.onrender.com"; // apna URL
```

---

## ✅ Done! Features jo kaam karenge:
- ✅ Email/Password Signup
- ✅ Login
- ✅ Forgot Password (email bhejta hai automatically)
- ✅ JWT token auto-refresh
- ✅ Secure backend verification
