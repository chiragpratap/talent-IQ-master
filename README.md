  
✨ Highlights:

- 🧑‍💻 VSCode-Powered Code Editor
- 🔐 Authentication via Clerk
- 🎥 1-on-1 Video Interview Rooms
- 🧭 Dashboard with Live Stats
- 🔊 Mic & Camera Toggle, Screen Sharing & Recording
- 💬 Real-time Chat Messaging
- ⚙️ Secure Code Execution in Isolated Environment
- 🎯 Auto Feedback — Success / Fail based on test cases
- 🎉 Confetti on Success + Notifications on Fail
- 🧩 Practice Problems Page (solo coding mode)
- 🔒 Room Locking — allows only 2 participants
- 🧠 Background Jobs with Inngest (async tasks)
- 🧰 REST API with Node.js & Express
- ⚡ Data Fetching & Caching via TanStack Query
- 🤖 CodeRabbit for PR Analysis & Code Optimization
- 🧑‍💻 Git & GitHub Workflow (branches, PRs, merges)
- 🚀 Deployment on Sevalla (free-tier friendly)

---

 
 
 #Step 1:  Install root dependencies (if any)
npm install
```

---

## 🛢️ Step 2: MongoDB Setup

### Create MongoDB Atlas Cluster

1. Go to [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Sign up / Login
3. Create a new project
4. Click "Create a Deployment"
5. Choose **FREE** tier (M0)
6. Select region (closest to you)
7. Create cluster (takes 2-3 minutes)

### Get Connection String

1. Click "Connect" on your cluster
2. Select "Drivers" → "Node.js"
3. Copy the connection string
4. Replace `<username>` & `<password>` with your credentials
5. Note: URL should look like:
   ```
   mongodb+srv://username:password@cluster.mongodb.net/dbname?retryWrites=true&w=majority
   ```

---

## 🔐 Step 3: Clerk Authentication Setup

### Create Clerk Application

1. Go to [Clerk Dashboard](https://dashboard.clerk.com)
2. Sign up / Login
3. Click "Create Application"
4. Choose application name (e.g., "talent-iq")
5. Copy your keys:
   - **Publishable Key** (starts with `pk_`)
   - **Secret Key** (starts with `sk_`)

### Add Redirect URLs

1. Go to Settings → Paths
2. Add Allowed Callback URLs:
   - `http://localhost:3000`
   - `http://localhost:5173`
   - `https://your-app.vercel.app`

---

## 💬 Step 4: Stream.io Setup

### Create Stream Application

1. Go to [Stream Dashboard](https://dashboard.getstream.io)
2. Sign up / Login
3. Create a new app
4. Choose a region (closest to you)
5. Copy your keys:
   - **API Key**
   - **API Secret**

### Configuration

1. Go to Settings → App
2. Enable Chat features
3. Enable Video features
4. Save configuration

---

## ⏰ Step 5: Inngest Setup

### Create Inngest Account

1. Go to [Inngest](https://inngest.com)
2. Sign up with GitHub
3. Create a new organization
4. Go to Settings → API Keys
5. Copy your keys:
   - **Event Key**
   - **Signing Key**

---

## 🔙 Step 6: Backend Setup

```bash
# Navigate to backend
cd backend

# Install dependencies
npm install
```

### Create .env File

```bash
# Create .env in backend directory
touch .env
```

### Add Environment Variables

Edit `backend/.env`:

```env
# Server Configuration
PORT=3000
NODE_ENV=development
CLIENT_URL=http://localhost:5173

# Database
DB_URL=mongodb+srv://username:password@cluster.mongodb.net/talent-iq?retryWrites=true&w=majority

# Clerk Authentication
CLERK_PUBLISHABLE_KEY=pk_test_xxxxxxxxxxxxxx
CLERK_SECRET_KEY=sk_test_xxxxxxxxxxxxxx

# Stream.io
STREAM_API_KEY=your_stream_api_key
STREAM_API_SECRET=your_stream_api_secret

# Inngest
INNGEST_EVENT_KEY=your_event_key
INNGEST_SIGNING_KEY=your_signing_key
```

### Start Backend Server

```bash
# In backend directory
npm run dev

# Should see:
# Server is running on http://localhost:3000
```

---

## 🎨 Step 7: Frontend Setup

```bash
# Navigate to frontend
cd frontend

# Install dependencies
npm install
```

### Create .env File

```bash
# Create .env in frontend directory
touch .env
```

### Add Environment Variables

Edit `frontend/.env`:

```env
# Clerk Authentication
VITE_CLERK_PUBLISHABLE_KEY=pk_test_xxxxxxxxxxxxxx

# API Configuration
VITE_API_URL=http://localhost:3000/api

# Stream.io
VITE_STREAM_API_KEY=your_stream_api_key
```

### Start Frontend Server

```bash
# In frontend directory
npm run dev

# Should see:
# ➜  Local:   http://localhost:5173/
```

---

## ✅ Step 8: Verify Setup

### Backend Health Check

```bash
# In a new terminal, run:
curl http://localhost:3000/health

# Should return 200 OK
```

### Frontend Check

1. Open [http://localhost:5173](http://localhost:5173)
2. You should see the home page
3. Click "Sign In" to test Clerk
4. Login with your credentials

### API Test

```bash
# Test API endpoint
curl http://localhost:3000/api/session \
  -H "Authorization: Bearer YOUR_CLERK_TOKEN"
```

---

## 🚀 Development Workflow

### Running Both Servers

**Terminal 1** (Backend):
```bash
cd backend
npm run dev
```

**Terminal 2** (Frontend):
```bash
cd frontend
npm run dev
```

### File Structure During Development

```
talent-IQ/
├── backend/          # Terminal 1
│   └── npm run dev   # Port 3000
└── frontend/         # Terminal 2
    └── npm run dev   # Port 5173
```

---

## 🐛 Troubleshooting

### Backend Won't Start

**Error**: `Cannot connect to MongoDB`
- ✅ Check `DB_URL` in .env
- ✅ Verify IP is whitelisted in MongoDB Atlas
- ✅ Ensure MongoDB cluster is running
- ✅ Check internet connection

**Error**: `Port 3000 already in use`
```bash
# Find process on port 3000
lsof -i :3000

# Kill process
kill -9 <PID>
```

### Frontend Won't Start

**Error**: `Module not found`
```bash
# Clean install
rm -rf node_modules package-lock.json
npm install
```

**Error**: `Clerk keys not working`
- ✅ Verify keys in .env match Clerk dashboard
- ✅ Check `VITE_` prefix is added
- ✅ Restart dev server after changing .env

### Can't Login (Clerk)

- ✅ Verify Clerk account is active
- ✅ Check callback URLs in Clerk settings
- ✅ Clear browser cache & cookies
- ✅ Try incognito/private mode

### API Errors (404/401)

- ✅ Ensure backend is running (`npm run dev`)
- ✅ Check `VITE_API_URL` matches backend URL
- ✅ Verify Clerk token is being sent
- ✅ Check CORS configuration

### Stream.io Not Connecting

- ✅ Verify Stream API key is correct
- ✅ Check Stream app is created & active
- ✅ Ensure network allows WebSocket
- ✅ Check browser console for errors

---

## 📚 Next Steps

1. **Explore the Code**: Read through component files
2. **Read Documentation**: Check [Backend README](./backend/README.md) & [Frontend README](./frontend/README.md)
3. **Test API**: Use Postman to test endpoints
4. **Start Coding**: Create your first feature!

---

## 🔗 Useful Links

- [Node.js Docs](https://nodejs.org/docs)
- [React Docs](https://react.dev)
- [Express Docs](https://expressjs.com)
- [MongoDB Docs](https://docs.mongodb.com)
- [Clerk Docs](https://clerk.com/docs)
- [Stream Docs](https://getstream.io/docs)
- [Vite Docs](https://vitejs.dev)

---

## 💬 Need Help?

1. Check this guide again
2. Read relevant README files
3. Check GitHub Issues
4. Ask in community Discord
5. Open an issue on GitHub

---

**Happy Coding! 🚀**
