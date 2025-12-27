# Fix: "Policy already exists" Error

## What Happened?

You tried to run the migration again, but some policies already exist from a previous run.

## ✅ Quick Fix - Option 1: Use Fixed Migration File

I've created a fixed version that handles this automatically:

1. In Supabase SQL Editor, click **"New Query"**
2. Open this file: `supabase/migrations/20251227054837_create_gearguard_schema_fixed.sql`
3. Copy ALL the code
4. Paste into SQL Editor
5. Click **"Run"**

This version will:
- Drop existing policies first (if they exist)
- Then create everything fresh
- Safe to run multiple times

---

## ✅ Quick Fix - Option 2: Drop Policies Manually

If you want to fix the original file, run this first:

```sql
-- Drop all existing policies
DROP POLICY IF EXISTS "Users can view all profiles" ON users_profile;
DROP POLICY IF EXISTS "Users can update own profile" ON users_profile;
DROP POLICY IF EXISTS "Users can insert own profile" ON users_profile;
DROP POLICY IF EXISTS "Anyone can view teams" ON maintenance_teams;
DROP POLICY IF EXISTS "Admins and managers can create teams" ON maintenance_teams;
DROP POLICY IF EXISTS "Admins and managers can update teams" ON maintenance_teams;
DROP POLICY IF EXISTS "Admins can delete teams" ON maintenance_teams;
DROP POLICY IF EXISTS "Anyone can view team members" ON team_members;
DROP POLICY IF EXISTS "Admins and managers can manage team members" ON team_members;
DROP POLICY IF EXISTS "Admins and managers can update team members" ON team_members;
DROP POLICY IF EXISTS "Admins and managers can delete team members" ON team_members;
DROP POLICY IF EXISTS "Anyone can view categories" ON equipment_categories;
DROP POLICY IF EXISTS "Admins and managers can create categories" ON equipment_categories;
DROP POLICY IF EXISTS "Admins and managers can update categories" ON equipment_categories;
DROP POLICY IF EXISTS "Anyone can view equipment" ON equipment;
DROP POLICY IF EXISTS "Authenticated users can create equipment" ON equipment;
DROP POLICY IF EXISTS "Users can update equipment" ON equipment;
DROP POLICY IF EXISTS "Admins can delete equipment" ON equipment;
DROP POLICY IF EXISTS "Anyone can view requests" ON maintenance_requests;
DROP POLICY IF EXISTS "Authenticated users can create requests" ON maintenance_requests;
DROP POLICY IF EXISTS "Users can update their requests or assigned requests" ON maintenance_requests;
DROP POLICY IF EXISTS "Users can delete their own requests or admins can delete any" ON maintenance_requests;
DROP POLICY IF EXISTS "Anyone can view notes" ON request_notes;
DROP POLICY IF EXISTS "Authenticated users can create notes" ON request_notes;
DROP POLICY IF EXISTS "Users can update their own notes" ON request_notes;
DROP POLICY IF EXISTS "Users can delete their own notes or admins can delete any" ON request_notes;
```

Then run the original migration file again.

---

## ✅ Quick Fix - Option 3: Check What's Already Created

If you just want to continue:

1. Go to **Table Editor** in Supabase Dashboard
2. Check which tables exist:
   - If all 7 tables exist → You're done! ✅
   - If some are missing → Use Option 1 (fixed file)

The error happened because policies were created, but the migration might have stopped partway through.

---

## 🎯 Recommended: Use Fixed File

**Best approach:** Use the fixed migration file I created:
- `supabase/migrations/20251227054837_create_gearguard_schema_fixed.sql`

It's safe to run multiple times and will handle everything automatically!

---

## Verify It Worked

After running the fixed migration:

1. Go to **Table Editor**
2. You should see all 7 tables:
   - ✅ users_profile
   - ✅ maintenance_teams
   - ✅ team_members
   - ✅ equipment_categories
   - ✅ equipment
   - ✅ maintenance_requests
   - ✅ request_notes

3. Test your app - everything should work now! 🎉


