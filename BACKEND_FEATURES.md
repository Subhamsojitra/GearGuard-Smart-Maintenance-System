# GearGuard Backend - Complete Documentation

## Backend Architecture: **Supabase (BaaS - Backend as a Service)**

This project uses **Supabase** as the complete backend solution, providing:
- PostgreSQL Database
- Authentication Service
- Row Level Security (RLS)
- REST API (Auto-generated)
- Real-time Subscriptions
- Storage (available but not used in this project)

---

## Total Backend Features: **35+**

---

## 1. Database Schema (7 Tables)

### ✅ **users_profile**
- Extended user profile information
- Links to Supabase Auth users
- Role-based access (admin, manager, technician, user)
- Fields: id, full_name, email, role, avatar_url, created_at

### ✅ **maintenance_teams**
- Team definitions for maintenance groups
- Fields: id, name, description, created_at, created_by

### ✅ **team_members**
- Many-to-many relationship between users and teams
- Team lead designation
- Fields: id, team_id, user_id, is_lead, created_at
- Unique constraint on (team_id, user_id)

### ✅ **equipment_categories**
- Equipment classification system
- Pre-populated with 6 default categories
- Fields: id, name, description, created_at

### ✅ **equipment**
- Company assets and equipment tracking
- Comprehensive equipment details
- Fields: id, name, serial_number (unique), category_id, department, assigned_employee, location, purchase_date, warranty_expiry, maintenance_team_id, default_technician_id, status, notes, created_at, created_by

### ✅ **maintenance_requests**
- Core maintenance work requests
- Full lifecycle tracking
- Fields: id, subject, description, equipment_id, team_id, type, priority, stage, scheduled_date, completed_date, duration_hours, assigned_to, created_by, created_at, updated_at

### ✅ **request_notes**
- Notes and updates on maintenance requests
- Audit trail functionality
- Fields: id, request_id, note, created_by, created_at

---

## 2. Database Relationships (10 Relationships)

### ✅ Foreign Key Constraints
1. `users_profile.id` → `auth.users.id` (CASCADE DELETE)
2. `maintenance_teams.created_by` → `users_profile.id`
3. `team_members.team_id` → `maintenance_teams.id` (CASCADE DELETE)
4. `team_members.user_id` → `users_profile.id` (CASCADE DELETE)
5. `equipment.category_id` → `equipment_categories.id`
6. `equipment.maintenance_team_id` → `maintenance_teams.id`
7. `equipment.default_technician_id` → `users_profile.id`
8. `equipment.created_by` → `users_profile.id`
9. `maintenance_requests.equipment_id` → `equipment.id` (CASCADE DELETE)
10. `maintenance_requests.team_id` → `maintenance_teams.id`
11. `maintenance_requests.assigned_to` → `users_profile.id`
12. `maintenance_requests.created_by` → `users_profile.id`
13. `request_notes.request_id` → `maintenance_requests.id` (CASCADE DELETE)
14. `request_notes.created_by` → `users_profile.id`

---

## 3. Row Level Security (RLS) Policies (21 Policies)

### ✅ **users_profile** (3 policies)
- ✅ SELECT: All authenticated users can view all profiles
- ✅ UPDATE: Users can only update their own profile
- ✅ INSERT: Users can only insert their own profile

### ✅ **maintenance_teams** (4 policies)
- ✅ SELECT: All authenticated users can view teams
- ✅ INSERT: Only admins and managers can create teams
- ✅ UPDATE: Only admins and managers can update teams
- ✅ DELETE: Only admins can delete teams

### ✅ **team_members** (4 policies)
- ✅ SELECT: All authenticated users can view team members
- ✅ INSERT: Only admins and managers can add members
- ✅ UPDATE: Only admins and managers can update members
- ✅ DELETE: Only admins and managers can remove members

### ✅ **equipment_categories** (3 policies)
- ✅ SELECT: All authenticated users can view categories
- ✅ INSERT: Only admins and managers can create categories
- ✅ UPDATE: Only admins and managers can update categories

### ✅ **equipment** (4 policies)
- ✅ SELECT: All authenticated users can view equipment
- ✅ INSERT: Authenticated users can create equipment (must be creator)
- ✅ UPDATE: Users can update their own equipment OR admins/managers can update any
- ✅ DELETE: Only admins can delete equipment

### ✅ **maintenance_requests** (4 policies)
- ✅ SELECT: All authenticated users can view requests
- ✅ INSERT: Authenticated users can create requests (must be creator)
- ✅ UPDATE: Users can update their own requests, assigned requests, team member requests, OR admins/managers can update any
- ✅ DELETE: Users can delete their own requests OR admins can delete any

### ✅ **request_notes** (4 policies)
- ✅ SELECT: All authenticated users can view notes
- ✅ INSERT: Authenticated users can create notes (must be creator)
- ✅ UPDATE: Users can only update their own notes
- ✅ DELETE: Users can delete their own notes OR admins can delete any

---

## 4. Database Indexes (9 Indexes)

### ✅ Performance Optimization
1. ✅ `idx_equipment_category` - Fast category lookups
2. ✅ `idx_equipment_team` - Fast team lookups
3. ✅ `idx_equipment_status` - Fast status filtering
4. ✅ `idx_requests_equipment` - Fast equipment-request joins
5. ✅ `idx_requests_team` - Fast team-request joins
6. ✅ `idx_requests_stage` - Fast stage filtering
7. ✅ `idx_requests_assigned` - Fast assigned user lookups
8. ✅ `idx_requests_scheduled` - Fast date range queries
9. ✅ `idx_team_members_user` - Fast user-team lookups
10. ✅ `idx_team_members_team` - Fast team-member lookups

---

## 5. Database Functions & Triggers (2 Features)

### ✅ **Automatic Timestamp Updates**
- ✅ Function: `update_updated_at_column()`
- ✅ Trigger: `update_maintenance_requests_updated_at`
- Automatically updates `updated_at` field on maintenance_requests table

### ✅ **Default Data Seeding**
- ✅ Pre-populated equipment categories:
  - Machinery
  - Vehicles
  - IT Equipment
  - HVAC
  - Electrical
  - Plumbing

---

## 6. Authentication Backend (5 Features)

### ✅ **Supabase Auth Integration**
- ✅ Email/Password authentication
- ✅ User registration with email verification
- ✅ Session management
- ✅ Password reset (via Supabase)
- ✅ JWT token-based authentication

### ✅ **User Profile Creation**
- ✅ Automatic profile creation on signup
- ✅ Role assignment during registration
- ✅ Profile linked to auth.users

---

## 7. API Endpoints (Auto-generated by Supabase)

### ✅ **REST API** (via Supabase Client)
All CRUD operations available through Supabase client:

#### Equipment Operations
- ✅ `GET /rest/v1/equipment` - List all equipment
- ✅ `GET /rest/v1/equipment?id=eq.{id}` - Get single equipment
- ✅ `POST /rest/v1/equipment` - Create equipment
- ✅ `PATCH /rest/v1/equipment?id=eq.{id}` - Update equipment
- ✅ `DELETE /rest/v1/equipment?id=eq.{id}` - Delete equipment

#### Maintenance Requests Operations
- ✅ `GET /rest/v1/maintenance_requests` - List all requests
- ✅ `GET /rest/v1/maintenance_requests?select=*,equipment(*),maintenance_teams(*)` - Get with relations
- ✅ `POST /rest/v1/maintenance_requests` - Create request
- ✅ `PATCH /rest/v1/maintenance_requests?id=eq.{id}` - Update request
- ✅ `DELETE /rest/v1/maintenance_requests?id=eq.{id}` - Delete request

#### Teams Operations
- ✅ `GET /rest/v1/maintenance_teams` - List all teams
- ✅ `POST /rest/v1/maintenance_teams` - Create team
- ✅ `PATCH /rest/v1/maintenance_teams?id=eq.{id}` - Update team
- ✅ `DELETE /rest/v1/maintenance_teams?id=eq.{id}` - Delete team

#### Team Members Operations
- ✅ `GET /rest/v1/team_members` - List all team members
- ✅ `POST /rest/v1/team_members` - Add member to team
- ✅ `PATCH /rest/v1/team_members?id=eq.{id}` - Update member (e.g., set as lead)
- ✅ `DELETE /rest/v1/team_members?id=eq.{id}` - Remove member from team

#### User Profile Operations
- ✅ `GET /rest/v1/users_profile` - List all profiles
- ✅ `GET /rest/v1/users_profile?id=eq.{id}` - Get single profile
- ✅ `PATCH /rest/v1/users_profile?id=eq.{id}` - Update profile

#### Equipment Categories Operations
- ✅ `GET /rest/v1/equipment_categories` - List all categories
- ✅ `POST /rest/v1/equipment_categories` - Create category
- ✅ `PATCH /rest/v1/equipment_categories?id=eq.{id}` - Update category

#### Request Notes Operations
- ✅ `GET /rest/v1/request_notes` - List all notes
- ✅ `POST /rest/v1/request_notes` - Create note
- ✅ `PATCH /rest/v1/request_notes?id=eq.{id}` - Update note
- ✅ `DELETE /rest/v1/request_notes?id=eq.{id}` - Delete note

---

## 8. Advanced Query Features

### ✅ **Supabase Query Builder**
- ✅ Select with joins (`.select('*, equipment(*), teams(*)')`)
- ✅ Filtering (`.eq()`, `.in()`, `.gte()`, `.lte()`)
- ✅ Ordering (`.order()`)
- ✅ Pagination (`.range()`)
- ✅ Count queries (`.select('id', { count: 'exact', head: true })`)
- ✅ Maybe single (`.maybeSingle()`)
- ✅ Complex filtering with multiple conditions

### ✅ **Real-time Subscriptions** (Available but not implemented)
- Supabase supports real-time subscriptions
- Can be enabled for live updates
- Example: `supabase.from('maintenance_requests').on('*', payload => {...})`

---

## 9. Data Validation & Constraints

### ✅ **Database Constraints**
- ✅ Unique constraints: `serial_number` on equipment, `email` on users_profile
- ✅ Check constraints: `role` enum, `status` enum, `type` enum, `priority` enum, `stage` enum
- ✅ NOT NULL constraints on required fields
- ✅ Foreign key constraints with CASCADE DELETE where appropriate
- ✅ Default values for timestamps and status fields

---

## 10. Security Features

### ✅ **Authentication Security**
- ✅ JWT-based authentication
- ✅ Secure password hashing (handled by Supabase)
- ✅ Session management
- ✅ Token refresh mechanism

### ✅ **Data Security**
- ✅ Row Level Security (RLS) on all tables
- ✅ Role-based access control (RBAC)
- ✅ Policy-based permissions
- ✅ Secure API key handling
- ✅ No SQL injection (parameterized queries via Supabase client)

---

## 11. Migration System

### ✅ **Database Migrations**
- ✅ Migration file: `20251227054837_create_gearguard_schema.sql`
- ✅ Complete schema creation
- ✅ Idempotent migrations (IF NOT EXISTS)
- ✅ Can be run multiple times safely

---

## Backend Summary

### **Technology Stack:**
- **Database**: PostgreSQL (via Supabase)
- **Backend Service**: Supabase (BaaS)
- **Authentication**: Supabase Auth
- **API**: REST API (auto-generated)
- **Security**: Row Level Security (RLS)
- **Real-time**: Available via Supabase Realtime

### **Backend Capabilities:**
- ✅ Complete CRUD operations for all entities
- ✅ Complex relational queries with joins
- ✅ Role-based access control
- ✅ Secure data access patterns
- ✅ Automatic timestamp management
- ✅ Data validation and constraints
- ✅ Performance optimization with indexes
- ✅ Scalable architecture
- ✅ Production-ready security

### **No Custom Backend Code Required:**
This project uses Supabase's managed backend, so there's:
- ❌ No Express.js server
- ❌ No custom API routes
- ❌ No database connection management
- ❌ No authentication middleware
- ❌ No server deployment needed

All backend functionality is provided by Supabase's managed services!

---

## Setup Requirements

To use the backend, you need:
1. ✅ Supabase account (free tier available)
2. ✅ Create a new Supabase project
3. ✅ Run the migration file in Supabase SQL Editor
4. ✅ Get project URL and anon key
5. ✅ Configure environment variables:
   ```
   VITE_SUPABASE_URL=your_project_url
   VITE_SUPABASE_ANON_KEY=your_anon_key
   ```

The backend is **fully functional** once Supabase is configured!


