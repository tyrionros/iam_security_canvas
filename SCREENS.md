# Screen Documentation - IAM Security Canvas

Complete reference guide for all screens in the IAM Security Canvas application.

## Table of Contents

1. [Welcome](#welcome)
2. [Dashboard](#dashboard)
3. [Users Grid](#users-grid)
4. [Accounts Grid](#accounts-grid)
5. [Contacts Grid](#contacts-grid)
6. [Bookable Resources Grid](#bookable-resources-grid)
7. [Entity Details](#entity-details)
8. [Create Entity](#create-entity)
9. [Navigation Map](#navigation-map)
10. [Data Models](#data-models)

---

## Welcome

**File:** `Welcome.pa.yaml`

**Purpose:** Application landing/splash screen on first load.

**Layout:**
- Header container with "IAM Security App" title
- Main container with responsive AutoLayout
- Professional enterprise styling

**Key Controls:**
- `GroupContainer` (AutoLayout) - Root container
- `GroupContainer` (AutoLayout) - Header section
- `Header` control - App title

**Features:**
- Centered layout for professional appearance
- Responsive design for all device sizes
- Light background with white content areas
- Entry point to Dashboard navigation

**Navigation:**
- → Dashboard (click on main area or navigate to Dashboard)

**Sample Data:** None (UI only)

---

## Dashboard

**File:** `Dashboard.pa.yaml`

**Purpose:** Main landing screen showing high-level overview and quick access to all entity management areas.

**Layout:**
- Header section with page title
- Statistics cards section (4 cards)
- Recently modified entities section
- Action buttons bar

**Key Controls:**
- `GroupContainer` (AutoLayout) - Root vertical container
- `Text` - Page title ("IAM Security Dashboard")
- `Card` - Statistics cards (Total Entities, Active, Inactive, Suspended)
- `Card` - Recently modified entity cards (clickable)
- `Button` - Action buttons (View All, Create New, Refresh)

**Features:**
- **Statistics Cards:**
  - Total Entities: 450
  - Active: 388 (green background)
  - Inactive: 45 (gray background)
  - Suspended: 17 (amber background)

- **Recently Modified Section:**
  - Shows 3 most recent entities
  - Displays Name, Type, and Last Modified timestamp
  - Cards are clickable for quick details view

- **Quick Actions:**
  - View All Entities - Navigate to entity grids
  - Create New Entity - Navigate to create form
  - Refresh - Reload data from Dataverse

**Color Scheme:**
- Background: Light gray (RGBA(245, 245, 247, 1))
- Cards: White with subtle shadows
- Active status: Green (RGBA(34, 177, 76, 1))
- Inactive status: Gray (RGBA(158, 158, 158, 1))
- Suspended status: Amber (RGBA(255, 193, 7, 1))

**Sample Data:**
```
Statistics:
- Total Entities: 450
- Active Count: 388
- Inactive Count: 45
- Suspended Count: 17

Recently Modified:
1. Alice Johnson (User) - Modified: Today
2. Contoso Inc (Account) - Modified: Yesterday
3. John Smith (Contact) - Modified: 2 days ago
```

**Navigation:**
- → Users Grid (click "View All" or entity grid buttons)
- → Entity Details (click on recent entity cards)
- → Create Entity (click "Create New Entity" button)

---

## Users Grid

**File:** `UsersGrid.pa.yaml`

**Purpose:** Display all user records in a filterable, searchable data grid.

**Layout:**
- Header with "Users" title and back button
- Filter toolbar (search + status filter)
- DataGrid showing all user records
- Action buttons bar

**Key Controls:**
- `GroupContainer` (AutoLayout) - Root vertical container
- `Text` - Page title
- `Button` - Back to Dashboard
- `TextInput` - Search field
- `ComboBox` - Status filter dropdown
- `DataGrid` - User records display
- `Button` - View Details, Create New User

**Features:**
- **Search:** Search users by name
- **Filter:** Filter by status (All, Active, Inactive, Suspended)
- **DataGrid Columns:**
  - ID
  - Name
  - Status (color-coded)
  - Owner
  - Created
  - AccessLevel

- **Sample Data (5 users):**
  - Alice Johnson (U001) - Active - Administrative
  - Bob Smith (U002) - Active - Advanced
  - Carol Davis (U003) - Inactive - Standard
  - David Wilson (U004) - Active - Basic
  - Emma Martinez (U005) - Suspended - Standard

**Color Scheme:**
- Header background: White
- DataGrid header: Green (RGBA(34, 177, 76, 1))
- Status Active: Green
- Status Inactive: Gray
- Status Suspended: Amber

**Navigation:**
- ← Back to Dashboard
- → Entity Details (select row, click "View Details")
- → Create Entity (click "Create New User")

---

## Accounts Grid

**File:** `AccountsGrid.pa.yaml`

**Purpose:** Display all account records with company information.

**Layout:** Same as Users Grid (consistent design pattern)

**Key Controls:**
- `GroupContainer` (AutoLayout) - Root vertical container
- `DataGrid` - Account records
- `TextInput` - Search accounts
- `ComboBox` - Status filter
- `Button` - Action buttons

**Features:**
- **Search:** Search accounts by company name
- **Filter:** Filter by status
- **DataGrid Columns:**
  - ID
  - Name (Company name)
  - Status (color-coded)
  - Owner
  - Created
  - AccessLevel (Enterprise, Professional, Standard)

- **Sample Data (5 accounts):**
  - Contoso Inc (A001) - Active - Enterprise
  - Fabrikam Corp (A002) - Active - Professional
  - Northwind Traders (A003) - Inactive - Standard
  - Adventure Works (A004) - Active - Professional
  - Wide World Importers (A005) - Suspended - Standard

**Navigation:**
- ← Back to Dashboard
- → Entity Details
- → Create Entity

---

## Contacts Grid

**File:** `ContactsGrid.pa.yaml`

**Purpose:** Display all contact records with contact person information.

**Layout:** Same as Users/Accounts Grids (consistent pattern)

**Key Controls:**
- `GroupContainer` (AutoLayout) - Root vertical container
- `DataGrid` - Contact records
- `TextInput` - Search contacts
- `ComboBox` - Status filter
- `Button` - Action buttons

**Features:**
- **Search:** Search contacts by name
- **Filter:** Filter by status
- **DataGrid Columns:**
  - ID
  - Name
  - Status (color-coded)
  - Owner
  - Created
  - AccessLevel

- **Sample Data (5 contacts):**
  - John Smith (C001) - Active - Standard
  - Sarah Johnson (C002) - Active - Standard
  - Michael Chen (C003) - Inactive - Basic
  - Emily Davis (C004) - Active - Standard
  - Robert Wilson (C005) - Suspended - Basic

**Navigation:**
- ← Back to Dashboard
- → Entity Details
- → Create Entity

---

## Bookable Resources Grid

**File:** `BookableResourcesGrid.pa.yaml`

**Purpose:** Display all bookable resources (meeting rooms, equipment, facilities).

**Layout:** Same as other Grid screens (consistent pattern)

**Key Controls:**
- `GroupContainer` (AutoLayout) - Root vertical container
- `DataGrid` - Resource records
- `TextInput` - Search resources
- `ComboBox` - Status filter
- `Button` - Action buttons

**Features:**
- **Search:** Search resources by name
- **Filter:** Filter by status
- **DataGrid Columns:**
  - ID
  - Name (Resource name)
  - Status (color-coded)
  - Owner
  - Created
  - AccessLevel

- **Sample Data (5 resources):**
  - Conference Room A (R001) - Active - Standard
  - Video Equipment Set (R002) - Active - Advanced
  - Printer - 3rd Floor (R003) - Inactive - Standard
  - Meeting Room B (R004) - Active - Standard
  - Executive Lounge (R005) - Suspended - Advanced

**Navigation:**
- ← Back to Dashboard
- → Entity Details
- → Create Entity

---

## Entity Details

**File:** `EntityDetails.pa.yaml`

**Purpose:** Display detailed view and edit form for a selected entity.

**Layout:**
- Header with entity name, type, and status badge
- Form container with editable fields
- Audit trail section showing change history
- Action buttons bar

**Key Controls:**
- `GroupContainer` (AutoLayout) - Root vertical container
- `Button` - Back navigation
- `Text` - Entity name and type
- `Button` - Status badge (disabled/read-only)
- `GroupContainer` - Form fields container
- `Text` - Field labels
- `TextInput` - Name, Owner (editable)
- `ComboBox` - Status, AccessLevel (editable dropdowns)
- `Text` - Created, LastModified (read-only timestamps)
- `GroupContainer` - Audit trail section
- `Text` - Audit entries (action, timestamp, actor)
- `Button` - Save, Deactivate, Delete

**Features:**
- **Editable Fields:**
  - Name
  - Status
  - Owner
  - AccessLevel

- **Read-Only Fields:**
  - ID
  - Created date
  - Last Modified timestamp
  - Entity Type

- **Status Badge:**
  - Color-coded (Green=Active, Gray=Inactive, Amber=Suspended)
  - Displays current status
  - Non-interactive (display only)

- **Audit Trail:**
  - Shows last 2 changes
  - Each entry displays:
    - Action taken (Status changed to Active, etc.)
    - Timestamp (Today at 2:30 PM, etc.)
    - Actor (who made the change)

- **Action Buttons:**
  - **Save Changes** (Green) - Save form edits
  - **Deactivate** (Amber) - Mark as inactive
  - **Delete** (Red) - Permanently remove entity

**Sample Data (Alice Johnson - User):**
```
ID: U001
Name: Alice Johnson
Type: User Account
Status: Active
Owner: admin@contoso.com
AccessLevel: Administrative
Created: Mar 15, 2024
LastModified: Today at 2:30 PM

Audit Trail:
- Status changed to Active (Today at 2:30 PM by admin@contoso.com)
- AccessLevel updated to Administrative (Yesterday at 10:15 AM by admin@contoso.com)
```

**Navigation:**
- ← Back (returns to previous grid)
- → To previous grid after save/delete

---

## Create Entity

**File:** `CreateEntity.pa.yaml`

**Purpose:** Form-based interface for creating new entities with validation.

**Layout:**
- Header with title and instructions
- Form container with input fields
- Validation messages section
- Action buttons bar

**Key Controls:**
- `GroupContainer` (AutoLayout) - Root vertical container
- `Text` - Form title and subtitle
- `GroupContainer` - Form fields container
- `Text` - Field labels
- `ComboBox` - Entity Type, Owner, Status, AccessLevel
- `TextInput` - Name/Title field, Description field (multiline)
- `GroupContainer` - Validation messages (error alerts)
- `Text` - Validation error messages
- `Button` - Create Entity, Cancel, Reset Form

**Features:**
- **Entity Type Selector:**
  - User
  - Account
  - Contact
  - Bookable Resource

- **Required Fields (marked with *):**
  - Entity Type
  - Name/Title
  - Owner
  - Status

- **Optional Fields:**
  - AccessLevel (defaults to Standard)
  - Description (multiline textarea)

- **Dropdowns:**
  - Owner: Dropdown list of valid owners
    - Admin Account (admin@contoso.com)
    - Manager Account (manager@contoso.com)
    - User Account (user@contoso.com)
  - Status: Active (default), Inactive, Suspended
  - AccessLevel: Basic, Standard (default), Advanced, Administrative

- **Validation:**
  - Shows validation message for required fields
  - Error styling (red border/background)
  - Must complete required fields before create

- **Action Buttons:**
  - **Create Entity** (Green) - Submit form and create
  - **Cancel** (Gray) - Discard form and return
  - **Reset Form** (Dark Gray) - Clear all fields

**Success/Error Handling:**
- ✅ Create success: "Entity created successfully!"
- ℹ️ Reset: "Form reset"
- ❌ Validation: "Required fields must be completed"

**Navigation:**
- ← Cancel/Back (returns to previous screen)
- → Entity Details (after successful creation)

---

## Navigation Map

```
Welcome
  ↓
Dashboard
  ├─→ Users Grid
  │    ├─→ Entity Details (select user)
  │    └─→ Create Entity (Create New User)
  │
  ├─→ Accounts Grid
  │    ├─→ Entity Details (select account)
  │    └─→ Create Entity (Create New Account)
  │
  ├─→ Contacts Grid
  │    ├─→ Entity Details (select contact)
  │    └─→ Create Entity (Create New Contact)
  │
  ├─→ Bookable Resources Grid
  │    ├─→ Entity Details (select resource)
  │    └─→ Create Entity (Create New Resource)
  │
  └─→ Create Entity (direct)

Entity Details
  ├─→ Back to Grid (save/deactivate/delete)
  └─→ Save Changes / Deactivate / Delete

Create Entity
  ├─→ Back to previous screen
  └─→ Entity Details (after creation)
```

---

## Data Models

### User Entity
```
{
  ID: String (unique identifier)
  Name: String (display name)
  Status: "Active" | "Inactive" | "Suspended"
  Owner: String (email/manager)
  Created: Date
  LastModified: Date
  AccessLevel: "Basic" | "Standard" | "Advanced" | "Administrative"
  Description: String (optional)
}
```

### Account Entity
```
{
  ID: String (unique identifier)
  Name: String (company name)
  Status: "Active" | "Inactive" | "Suspended"
  Owner: String (account manager)
  Created: Date
  LastModified: Date
  AccessLevel: "Standard" | "Professional" | "Enterprise"
  Description: String (optional)
}
```

### Contact Entity
```
{
  ID: String (unique identifier)
  Name: String (contact person name)
  Status: "Active" | "Inactive" | "Suspended"
  Owner: String (assigned to)
  Created: Date
  LastModified: Date
  AccessLevel: "Basic" | "Standard"
  Description: String (optional - email, phone, etc.)
}
```

### Bookable Resource Entity
```
{
  ID: String (unique identifier)
  Name: String (resource name/location)
  Status: "Active" | "Inactive" | "Suspended"
  Owner: String (facility/department owner)
  Created: Date
  LastModified: Date
  AccessLevel: "Standard" | "Advanced"
  Description: String (optional - capacity, details)
}
```

### Status Values
- **Active** (Green #34B14C) - Resource is available and in use
- **Inactive** (Gray #9E9E9E) - Resource is not in use
- **Suspended** (Amber #FFC107) - Resource temporarily unavailable

### Access Levels
- **Basic** - Read-only access
- **Standard** - Standard CRUD operations (default)
- **Advanced** - Advanced features + administration
- **Administrative** - Full system access

---

## Color Palette Reference

| Element | Color | Hex | RGBA |
|---------|-------|-----|------|
| Primary Background | Light Gray | #F5F5F7 | RGBA(245, 245, 247, 1) |
| Secondary Background | White | #FFFFFF | RGBA(255, 255, 255, 1) |
| Accent Primary | Matrix Green | #22B14C | RGBA(34, 177, 76, 1) |
| Accent Secondary | Professional Blue | #1A76BC | RGBA(26, 118, 188, 1) |
| Text Primary | Dark Gray | #333333 | RGBA(51, 51, 51, 1) |
| Text Secondary | Medium Gray | #666666 | RGBA(102, 102, 102, 1) |
| Border | Light Gray | #C8C8C8 | RGBA(200, 200, 200, 1) |
| Status Active | Green | #22B14C | RGBA(34, 177, 76, 1) |
| Status Inactive | Gray | #9E9E9E | RGBA(158, 158, 158, 1) |
| Status Suspended | Amber | #FFC107 | RGBA(255, 193, 7, 1) |
| Status Error | Red | #F44336 | RGBA(244, 67, 54, 1) |

---

## Screen Statistics

| Metric | Count |
|--------|-------|
| Total Screens | 8 |
| Grid Screens | 4 (Users, Accounts, Contacts, Resources) |
| Form Screens | 2 (Entity Details, Create Entity) |
| Utility Screens | 2 (Welcome, Dashboard) |
| Total Controls | 150+ |
| Responsive | 100% (AutoLayout) |

---

## File Structure

```
iam-app/
├── Welcome.pa.yaml                 # Landing screen
├── Dashboard.pa.yaml               # Main dashboard with stats
├── UsersGrid.pa.yaml               # Users entity grid
├── AccountsGrid.pa.yaml            # Accounts entity grid
├── ContactsGrid.pa.yaml            # Contacts entity grid
├── BookableResourcesGrid.pa.yaml   # Resources entity grid
├── EntityDetails.pa.yaml           # View & edit form
└── CreateEntity.pa.yaml            # Create new entity form
```

---

## Recent Updates

- **2026-05-04** - Created all 8 screens with complete YAML definitions
- **2026-05-04** - Added sample data to all grid screens
- **2026-05-04** - Implemented form validation and error handling
- **2026-05-04** - Applied consistent matrix green theme across all screens

---

**Last Updated:** May 4, 2026

**Documentation Version:** 1.0

**Total Lines of YAML:** 1,400+

For more information, see README.md and DEPLOYMENT.md
