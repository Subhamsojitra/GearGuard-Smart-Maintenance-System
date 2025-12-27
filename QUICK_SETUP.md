# 🚀 Quick Database Setup - 5 Minutes

## 📁 The File You Need

**File Path:** `supabase/migrations/20251227054837_create_gearguard_schema.sql`

This file contains ALL the SQL code to create your database!

---

## ⚡ Quick Steps

### 1️⃣ Get Supabase Credentials

1. Go to: https://supabase.com/dashboard
2. Open your project (or create new one)
3. Go to: **Settings** → **API**
4. Copy:
   - **Project URL** (looks like: `https://xxxxx.supabase.co`)
   - **anon public key** (long string)

### 2️⃣ Create .env File

In your project root folder, create file named `.env`:

```env
VITE_SUPABASE_URL=https://your-project-id.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-key-here
```

**Replace with YOUR actual values!**

### 3️⃣ Run Database Migration

1. Open Supabase Dashboard
2. Click **SQL Editor** (left sidebar)
3. Click **"New Query"**
4. Open file: `supabase/migrations/20251227054837_create_gearguard_schema.sql`
5. **Copy ALL code** (Ctrl+A, Ctrl+C)
6. **Paste** into SQL Editor (Ctrl+V)
7. Click **"Run"** button
8. Wait for ✅ "Success" message

### 4️⃣ Verify

1. In Supabase Dashboard → **Table Editor**
2. You should see 7 tables:
   - users_profile
   - maintenance_teams
   - team_members
   - equipment_categories
   - equipment
   - maintenance_requests
   - request_notes

### 5️⃣ Restart App

```bash
# Stop server (Ctrl+C)
npm run dev
```

---

## ✅ Done!

Now login and test:
- Dashboard should work
- Equipment page should work
- Teams page should work
- Requests page should work

---

## 🆘 Troubleshooting

**"Supabase is not configured"**
→ Check `.env` file exists and has correct values

**"Table does not exist"**
→ Migration didn't run - go back to step 3

**Can login but pages are blank**
→ Normal! No data yet. Try creating equipment/teams.

---

## 📍 File Locations

```
project/
├── .env                                    ← CREATE THIS
├── supabase/
│   └── migrations/
│       └── 20251227054837_create_gearguard_schema.sql  ← COPY THIS FILE'S CODE
```

That's it! 🎉


