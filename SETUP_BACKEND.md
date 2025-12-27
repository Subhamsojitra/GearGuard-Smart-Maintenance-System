# Backend Setup Guide - Connect Your Database

## Current Status
✅ **Supabase Auth is working** (login/signup works)  
❌ **Database tables are missing** (other features don't work)

## Why Other Features Don't Work

When you try to use features like Dashboard, Equipment, or Requests, the app tries to query database tables like:
- `users_profile`
- `equipment`
- `maintenance_requests`
- `maintenance_teams`
- etc.

These tables don't exist yet because the database migration hasn't been run!

---

## Step-by-Step Setup

### Step 1: Get Your Supabase Credentials

1. Go to [https://supabase.com](https://supabase.com)
2. Sign in to your account
3. Open your project (or create a new one)
4. Go to **Settings** → **API**
5. Copy these values:
   - **Project URL** (looks like: `https://xxxxx.supabase.co`)
   - **anon/public key** (long string starting with `eyJ...`)

### Step 2: Create .env File

Create a file named `.env` in your project root (same folder as `package.json`) with:

```env
VITE_SUPABASE_URL=https://your-project-id.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-key-here
```

**Important:** Replace `your-project-id` and `your-anon-key-here` with your actual values!

### Step 3: Run the Database Migration

You need to create all the database tables. Here's how:

#### Option A: Using Supabase Dashboard (Easiest)

1. Go to your Supabase project dashboard
2. Click on **SQL Editor** in the left sidebar
3. Click **New Query**
4. Open the file: `supabase/migrations/20251227054837_create_gearguard_schema.sql`
5. Copy **ALL** the contents of that file
6. Paste it into the SQL Editor
7. Click **Run** (or press Ctrl+Enter)
8. Wait for it to complete (should see "Success. No rows returned")

#### Option B: Using Supabase CLI (Advanced)

If you have Supabase CLI installed:

```bash
supabase db push
```

### Step 4: Verify Tables Are Created

1. In Supabase Dashboard, go to **Table Editor**
2. You should see these tables:
   - ✅ `users_profile`
   - ✅ `maintenance_teams`
   - ✅ `team_members`
   - ✅ `equipment_categories`
   - ✅ `equipment`
   - ✅ `maintenance_requests`
   - ✅ `request_notes`

### Step 5: Restart Your Dev Server

After creating the `.env` file, restart your development server:

1. Stop the current server (Ctrl+C)
2. Run: `npm run dev`
3. The app should now work!

---

## Troubleshooting

### Issue: "Error fetching profile" or tables not found

**Solution:** The migration hasn't been run. Go back to Step 3 and run the SQL migration.

### Issue: "Supabase is not configured"

**Solution:** 
- Check that `.env` file exists in project root
- Check that variable names are exactly: `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY`
- Restart the dev server after creating `.env`

### Issue: Login works but can't see dashboard

**Solution:** 
- Database tables are missing
- Run the migration (Step 3)
- Check browser console for errors

### Issue: "Permission denied" errors

**Solution:**
- Make sure you're logged in
- Check that Row Level Security (RLS) policies were created (they're in the migration file)
- Verify your user has a profile in `users_profile` table

---

## Quick Test

After setup, test if it works:

1. **Login/Signup** ✅ (should already work)
2. **Dashboard** - Should show statistics (may be 0 if no data)
3. **Equipment** - Should show empty list (can add equipment)
4. **Teams** - Should show empty list (can create teams)

---

## What the Migration Does

The migration file creates:
- 7 database tables
- 21 Row Level Security policies
- 9 performance indexes
- 1 automatic timestamp trigger
- 6 default equipment categories

**Total:** ~490 lines of SQL that sets up your entire backend!

---

## Need Help?

If you're stuck:
1. Check browser console (F12) for error messages
2. Check Supabase Dashboard → Logs for backend errors
3. Verify all tables exist in Table Editor
4. Make sure `.env` file is in the correct location

Once the migration is run, all features should work! 🚀


