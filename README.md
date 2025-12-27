# GearGuard: The Ultimate Maintenance Tracker

A comprehensive full-stack maintenance management system built with React, TypeScript, Tailwind CSS, and Supabase.

## Features

### 1. Equipment Management
- Track all company assets (machines, vehicles, computers)
- Organize by department and employee
- Assign maintenance teams and default technicians
- Track warranty information and purchase dates
- View equipment status (active, inactive, scrapped)
- Smart buttons showing active maintenance requests count
- Search and filter equipment

### 2. Maintenance Teams
- Create and manage specialized maintenance teams
- Assign team members and designate team leads
- View team workload and active requests
- Manage team member permissions

### 3. Maintenance Requests
- Kanban board with drag-and-drop functionality
- Four stages: New, In Progress, Repaired, Scrapped
- Two types: Corrective (breakdown) and Preventive (routine)
- Priority levels: Low, Medium, High, Critical
- Auto-fill team and category from selected equipment
- Visual indicators for overdue requests
- Assign technicians to requests
- Track duration and completion dates

### 4. Calendar View
- Monthly calendar view for preventive maintenance
- Schedule maintenance tasks by clicking dates
- View upcoming maintenance at a glance
- Filter by date range

### 5. Dashboard & Reports
- Total equipment count
- Active maintenance requests
- Team statistics
- Overdue requests tracking
- Requests by stage (visual charts)
- Requests by type (corrective vs preventive)
- Requests by team distribution

### 6. Authentication & Security
- Email/password authentication via Supabase
- Role-based access control (Admin, Manager, Technician, User)
- Row Level Security (RLS) policies
- Secure data access patterns

## Project Structure

```
project/
├── src/
│   ├── components/          # Reusable UI components
│   │   ├── Layout.tsx       # Main layout with sidebar navigation
│   │   └── Modal.tsx        # Modal component for forms
│   ├── contexts/            # React contexts
│   │   └── AuthContext.tsx  # Authentication context and hooks
│   ├── hooks/               # Custom React hooks
│   ├── lib/                 # Library configurations
│   │   └── supabase.ts      # Supabase client setup
│   ├── pages/               # Page components
│   │   ├── Dashboard.tsx    # Dashboard with statistics
│   │   ├── Equipment.tsx    # Equipment management
│   │   ├── Teams.tsx        # Team management
│   │   ├── Requests.tsx     # Maintenance requests Kanban
│   │   ├── CalendarView.tsx # Calendar for preventive maintenance
│   │   └── Login.tsx        # Authentication page
│   ├── types/               # TypeScript type definitions
│   │   ├── database.ts      # Supabase database types
│   │   └── index.ts         # Application types
│   ├── utils/               # Utility functions
│   ├── App.tsx              # Main application component
│   ├── main.tsx             # Application entry point
│   └── index.css            # Global styles
├── .env                     # Environment variables
├── package.json             # Dependencies and scripts
└── README.md                # This file
```

## Database Schema

### Tables
1. **users_profile** - Extended user profiles with roles
2. **maintenance_teams** - Maintenance team definitions
3. **team_members** - Team membership associations
4. **equipment_categories** - Equipment classification
5. **equipment** - Company assets and equipment
6. **maintenance_requests** - Maintenance work requests
7. **request_notes** - Notes and updates on requests

### Key Relationships
- Equipment → Category (many-to-one)
- Equipment → Maintenance Team (many-to-one)
- Equipment → Default Technician (many-to-one)
- Maintenance Request → Equipment (many-to-one)
- Maintenance Request → Team (many-to-one)
- Maintenance Request → Assigned User (many-to-one)
- Team Members → Team (many-to-one)
- Team Members → User (many-to-one)

## Getting Started

### Prerequisites
- Node.js 18+ installed
- Supabase account and project

### Installation

1. Install dependencies:
```bash
npm install
```

2. Configure environment variables in `.env`:
```
VITE_SUPABASE_URL=your_supabase_url
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
```

3. The database schema has already been created via Supabase migrations.

4. Start the development server:
```bash
npm run dev
```

5. Build for production:
```bash
npm run build
```

## Key Workflows

### Workflow 1: The Breakdown (Corrective Maintenance)
1. User creates a new maintenance request
2. Select equipment → System auto-fills category and team
3. Request starts in "New" stage
4. Manager/Technician assigns themselves
5. Drag card to "In Progress"
6. Complete work and record duration
7. Drag to "Repaired" stage

### Workflow 2: The Routine Checkup (Preventive Maintenance)
1. Manager creates preventive maintenance request
2. Set scheduled date
3. Request appears on calendar view
4. Technician works on scheduled date
5. Complete and move to "Repaired"

### Workflow 3: Equipment Scrapping
1. When request is moved to "Scrapped" stage
2. System automatically marks equipment as scrapped
3. Equipment status updates to reflect disposal

## Smart Features

### Auto-Fill Logic
- When selecting equipment in a request, the system automatically fills:
  - Equipment category
  - Maintenance team (from equipment's default team)

### Smart Buttons
- Equipment detail view shows active maintenance request count
- Click to view all requests for that specific equipment
- Badge indicates number of open requests

### Visual Indicators
- Red indicators for overdue requests
- Color-coded priority levels
- Status badges for equipment and requests
- Team member avatars

### Drag-and-Drop
- Intuitive Kanban board
- Drag requests between stages
- Auto-saves on drop
- Visual feedback during drag

## User Roles

### Admin
- Full access to all features
- Can delete any data
- Manage teams and equipment

### Manager
- Create and manage teams
- Create and assign requests
- View all data
- Cannot delete teams

### Technician
- View assigned requests
- Update request status
- Add equipment
- View calendar

### User
- Create maintenance requests
- View own requests
- View equipment

## Technology Stack

- **Frontend**: React 18, TypeScript, Tailwind CSS
- **Backend**: Supabase (PostgreSQL, Authentication, RLS)
- **Build Tool**: Vite
- **Icons**: Lucide React
- **Styling**: Tailwind CSS with custom design system

## Security

- Row Level Security (RLS) enabled on all tables
- Authenticated-only access to data
- Role-based permissions
- Secure API key handling
- No exposed secrets in frontend code

## Performance Optimizations

- Efficient database queries with joins
- Indexed columns for fast searches
- Optimized re-renders with React hooks
- Lazy loading of data
- Responsive design for all screen sizes

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## License

This project is private and proprietary.

## Support

For issues or questions, contact the development team.
