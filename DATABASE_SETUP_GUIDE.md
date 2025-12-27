# Complete Database Setup Guide

## 📋 What You Need

1. A Supabase account (free at https://supabase.com)
2. A Supabase project created
3. The migration SQL file

---

## 🚀 Step-by-Step Setup

### Step 1: Get Your Supabase Project

1. Go to **https://supabase.com**
2. **Sign in** (or create free account)
3. Click **"New Project"** (or select existing project)
4. Fill in:
   - **Name**: GearGuard (or any name)
   - **Database Password**: Create a strong password (save it!)
   - **Region**: Choose closest to you
   - Click **"Create new project"**
5. Wait 2-3 minutes for project to be created

### Step 2: Get Your Connection Details

1. In your Supabase project dashboard
2. Click **Settings** (gear icon) in left sidebar
3. Click **API** under Configuration
4. You'll see:
   - **Project URL**: `https://xxxxx.supabase.co` ← Copy this
   - **anon public key**: `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...` ← Copy this

### Step 3: Create .env File in Your Project

1. In your project folder, create a file named `.env` (no extension)
2. Add these two lines (replace with YOUR values):

```env
VITE_SUPABASE_URL=https://your-project-id.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-key-here
```

**Example:**
```env
VITE_SUPABASE_URL=https://abcdefghijklmnop.supabase.co
VITE_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImFiY2RlZmdoaWprbG1ub3AiLCJyb2xlIjoiYW5vbiIsImlhdCI6MTYxNjIzOTAyMiwiZXhwIjoxOTMxODE1MDIyfQ.xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

### Step 4: Run the Database Migration

This creates all your tables!

#### Method 1: Using Supabase Dashboard (Easiest) ⭐

1. In Supabase Dashboard, click **SQL Editor** in left sidebar
2. Click **"New Query"** button (top right)
3. You'll see a blank SQL editor

4. **Open this file in your project:**
   - File path: `supabase/migrations/20251227054837_create_gearguard_schema.sql`
   - Open it in any text editor (VS Code, Notepad, etc.)

5. **Copy ALL the code** from that file (Ctrl+A, then Ctrl+C)
   - It's about 490 lines of SQL code
   - Starts with `/*` and ends with `*/`

6. **Paste it** into the Supabase SQL Editor (Ctrl+V)

7. Click **"Run"** button (or press Ctrl+Enter)

8. Wait for success message: ✅ **"Success. No rows returned"**

#### Method 2: Using Supabase CLI (Advanced)

If you have Supabase CLI installed:

```bash
# Install Supabase CLI (if not installed)
npm install -g supabase

# Login to Supabase
supabase login

# Link your project
supabase link --project-ref your-project-ref

# Push migration
supabase db push
```

### Step 5: Verify Tables Were Created

1. In Supabase Dashboard, click **Table Editor** in left sidebar
2. You should see these 7 tables:
   - ✅ `users_profile`
   - ✅ `maintenance_teams`
   - ✅ `team_members`
   - ✅ `equipment_categories`
   - ✅ `equipment`
   - ✅ `maintenance_requests`
   - ✅ `request_notes`

If you see all 7 tables, your database is set up correctly! 🎉

### Step 6: Restart Your Development Server

1. **Stop** your current dev server (press Ctrl+C in terminal)
2. **Start it again:**
   ```bash
   npm run dev
   ```

### Step 7: Test the Connection

1. Open your app in browser (usually http://localhost:5173)
2. **Sign up** for a new account (or login if you already have one)
3. After login, you should see the **Dashboard** (not just login page)
4. Try clicking:
   - Dashboard → Should show statistics
   - Equipment → Should show empty list (you can add equipment)
   - Teams → Should show empty list (you can create teams)
   - Requests → Should show empty Kanban board

---

## 🔍 Troubleshooting

### Problem: "Supabase is not configured"

**Solution:**
- Check `.env` file exists in project root (same folder as `package.json`)
- Check variable names are exactly: `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY`
- Make sure there are NO spaces around the `=` sign
- Restart dev server after creating `.env`

### Problem: "relation does not exist" or "table not found"

**Solution:**
- The migration wasn't run successfully
- Go back to Step 4 and run the SQL migration again
- Check Supabase SQL Editor for any error messages

### Problem: "Permission denied" or "Row Level Security"

**Solution:**
- Make sure you ran the COMPLETE migration file (all 490 lines)
- The migration includes RLS policies - they must be created
- Check in Supabase Dashboard → Authentication → Users that your user exists

### Problem: Can login but Dashboard is empty/blank

**Solution:**
- This is normal! You just created the database, so there's no data yet
- Try creating some equipment or teams to see if it works
- Check browser console (F12) for any errors

### Problem: Migration fails with errors

**Solution:**
- Make sure you copied the ENTIRE file (from `/*` to `*/`)
- Check if tables already exist - you might need to delete them first
- Look at the error message in Supabase SQL Editor for specific issues

---

## 📁 File Location Reference

**Migration file location:**
```
project/
└── supabase/
    └── migrations/
        └── 20251227054837_create_gearguard_schema.sql  ← THIS FILE
```

**Environment file location:**
```
project/
└── .env  ← CREATE THIS FILE HERE
```

---

## ✅ Checklist

Before you start:
- [ ] Have Supabase account
- [ ] Created Supabase project
- [ ] Got Project URL and anon key

Setup steps:
- [ ] Created `.env` file with correct values
- [ ] Opened migration SQL file
- [ ] Copied all SQL code
- [ ] Pasted into Supabase SQL Editor
- [ ] Ran the migration successfully
- [ ] Verified 7 tables exist in Table Editor
- [ ] Restarted dev server
- [ ] Tested login and dashboard

---

## 🎯 Quick Reference

**Supabase Dashboard:** https://supabase.com/dashboard  
**SQL Editor:** Dashboard → SQL Editor → New Query  
**Table Editor:** Dashboard → Table Editor  
**API Settings:** Dashboard → Settings → API  

**Migration File:** `supabase/migrations/20251227054837_create_gearguard_schema.sql`  
**Environment File:** `.env` (create in project root)

---

## 💡 What the Migration Does

The SQL migration file creates:
- ✅ 7 database tables
- ✅ 21 Row Level Security (RLS) policies
- ✅ 9 performance indexes
- ✅ 1 automatic timestamp trigger
- ✅ 6 default equipment categories
- ✅ All foreign key relationships

**Total:** Complete backend database setup in one file!

---

## 🆘 Still Having Issues?

1. **Check browser console** (F12 → Console tab) for errors
2. **Check Supabase logs** (Dashboard → Logs)
3. **Verify .env file** is in correct location
4. **Make sure migration ran** without errors
5. **Check all 7 tables exist** in Table Editor

Once everything is set up, your app will be fully functional! 🚀


