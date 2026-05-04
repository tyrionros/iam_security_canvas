# IAM Security Canvas

A Power Apps Canvas application for managing Identity & Access Management (IAM) entities with a matrix green cyberpunk theme.

## Overview

IAM Security Canvas is a centralized platform for enterprise administrators to efficiently manage, monitor, and audit identity entities across systems. The application provides a clean, intuitive interface for managing four core Dataverse entities:

- **Users** - User accounts and credentials
- **Accounts** - Organization accounts and memberships
- **Contacts** - Contact information and relationships
- **Bookable Resources** - Resources available for scheduling and allocation

## Features

✅ **Entity Management**
- View all entities in responsive data grids
- Create new entities with validation
- Edit and modify existing entity records
- Deactivate entities with audit trail tracking

✅ **Matrix Green Theme**
- Dark backgrounds (#000000, #1a1a1a)
- Bright green/lime accents (#00ff00, #39ff14)
- High-contrast cyberpunk aesthetic
- Professional enterprise dashboard styling

✅ **Dataverse Integration**
- Direct connection to Dataverse tables
- Real-time data synchronization
- Full CRUD operations
- Status tracking (Active, Inactive, Suspended)

✅ **Responsive Design**
- Multi-device support (desktop, tablet, phone)
- AutoLayout containers for responsive behavior
- Touch-friendly controls

## Project Structure

```
iam_security_canvas/
├── README.md                      # This file
├── .mcp.json                      # Canvas Authoring MCP configuration
├── .claude/
│   ├── settings.json              # Claude Code settings
│   └── settings.local.json        # Local settings override
├── iam-app/
│   ├── App.pa.yaml                # Main app configuration
│   └── Screen1.pa.yaml            # Default screen
├── entity-management/
│   ├── App.pa.yaml                # Entity management app config
│   └── canvas-app-plan.md         # Design specifications
└── matrix-green-scheme/           # Legacy design planning
```

## Setup Instructions

### Prerequisites

- **Power Apps Studio** (online or desktop)
- **.NET 10 SDK** or higher (for Canvas Authoring MCP)
- **Claude Code** with Canvas Authoring MCP configured
- **Dataverse environment** with the following tables:
  - Users
  - Accounts
  - Contacts
  - Bookable Resources

### Configuration

#### 1. MCP Server Setup

The Canvas Authoring MCP server is configured in `.mcp.json`:

```bash
claude mcp add --scope project canvas-authoring \
  -e CANVAS_ENVIRONMENT_ID=3a770202-3461-e3a2-b731-94cc35e6be5b \
  -e CANVAS_APP_ID=9e1c256c-272a-47ef-915b-ee4f0e79765d \
  -e CANVAS_CLUSTER_CATEGORY=prod \
  -- dnx Microsoft.PowerApps.CanvasAuthoring.McpServer --yes --prerelease --source https://api.nuget.org/v3/index.json
```

#### 2. Enable Coauthoring

In Power Apps Designer:
1. Open the app
2. Go to **Settings** → **Updates** → **Coauthoring**
3. Toggle **Coauthoring** ON
4. Save the app

#### 3. Connect Dataverse Tables

In Power Apps Designer:
1. Click **Data** (left panel)
2. Add connections for each Dataverse table:
   - Users
   - Accounts
   - Contacts
   - Bookable Resources

### Building the Screens

Create the following screens in Power Apps Designer:

#### Dashboard
- Display quick-access entity cards
- Show summary statistics (total entities, active count, pending audits)
- Navigation buttons to management areas

#### Entity Management Screens (for each entity)
Each screen should include:

**Data Grid Section:**
- DataGrid control displaying all records
- Columns: ID, Name, Status, Owner, Created, LastModified, AccessLevel
- Search/filter functionality
- Row selection

**Form Section:**
- EntityForm for create/edit operations
- Fields: Name, Owner (dropdown), Status (dropdown), AccessLevel, Description
- Input validation
- Success/error messaging

**Action Buttons:**
- Create Entity (primary, green button)
- Edit Entity (secondary)
- Deactivate Entity (red button)
- Delete Entity (with confirmation)
- Back/Navigation buttons

### Color Palette

#### Matrix Green Theme

| Element | Color | Hex | RGBA |
|---------|-------|-----|------|
| Primary Background | Black | #000000 | RGBA(0, 0, 0, 1) |
| Secondary Background | Dark Charcoal | #1a1a1a | RGBA(26, 26, 26, 1) |
| Accent (Bright Green) | Lime | #00ff00 | RGBA(0, 255, 0, 1) |
| Accent (Matrix Green) | Neon Green | #39ff14 | RGBA(57, 255, 20, 1) |
| Text Primary | Dark Gray | #333333 | RGBA(51, 51, 51, 1) |
| Text Secondary | Medium Gray | #666666 | RGBA(102, 102, 102, 1) |
| Status Active | Green | #22b14c | RGBA(34, 177, 76, 1) |
| Status Inactive | Gray | #9e9e9e | RGBA(158, 158, 158, 1) |
| Status Suspended | Amber | #ffc107 | RGBA(255, 193, 7, 1) |
| Status Error | Red | #f44336 | RGBA(244, 67, 54, 1) |

## Development

### Claude Code Integration

This project uses Claude Code with the Canvas Authoring MCP plugin for AI-assisted app development.

#### Available MCP Tools:
- `list_controls` - List all available Power Apps controls
- `list_data_sources` - List connected data sources
- `list_apis` - List available connectors
- `describe_control` - Get detailed control properties
- `sync_canvas` - Sync app state from coauthoring session
- `compile_canvas` - Validate app YAML files

### Making Changes

1. Keep Power Apps Designer tab open (coauthoring must be active)
2. Use Claude Code to plan and implement changes
3. Test in Power Apps Designer
4. Sync changes back to the repository

## Dataverse Entities

### Users Table
- **ID** - Unique identifier
- **Name** - User name/display name
- **Status** - Active, Inactive, Suspended
- **Owner** - User's manager/owner
- **AccessLevel** - Basic, Standard, Advanced, Administrative
- **Created** - Creation date
- **LastModified** - Last modification date
- **Description** - User details

### Accounts Table
- Similar structure with account-specific fields
- Parent organization references

### Contacts Table
- Contact information (email, phone)
- Organization association
- Relationship tracking

### Bookable Resources Table
- Resource availability
- Scheduling information
- Capacity management

## Power Fx Formulas

### Color Constants
```powerapps
MatrixGreen = RGBA(34, 177, 76, 1)
MatrixGreenDark = RGBA(27, 142, 61, 1)
MatrixGreenLight = RGBA(76, 209, 118, 1)
AppBgColor = RGBA(245, 245, 247, 1)
ContentBgColor = RGBA(255, 255, 255, 1)
```

### Status Color Function
```powerapps
GetStatusColor(status: Text): Color =
  If(
    status = "Active", RGBA(34, 177, 76, 1),
    status = "Inactive", RGBA(158, 158, 158, 1),
    status = "Suspended", RGBA(255, 193, 7, 1),
    RGBA(158, 158, 158, 1)
  )
```

### Date Formatting
```powerapps
FormatDate(dateValue: Date): Text =
  Text(dateValue, "mmm d, yyyy")
```

## Known Limitations

- Manual screen creation in Power Apps Designer (YAML generation requires refinement)
- Audit trail tracking implemented via mock collections (can be connected to actual audit tables)
- Batch operations not yet implemented

## Future Enhancements

- [ ] Batch operations for bulk updates
- [ ] Advanced filtering and search
- [ ] Custom audit trail with detailed change tracking
- [ ] Role-based access control (RBAC)
- [ ] Export to Excel/PDF functionality
- [ ] Mobile-optimized views
- [ ] Dark mode toggle
- [ ] Approval workflows

## Contributing

1. Create a feature branch from `main`
2. Make changes in Power Apps Designer
3. Sync changes back to the repository
4. Submit a pull request

## License

This project is proprietary and confidential.

## Support

For issues, questions, or feature requests, please contact the development team.

---

**Repository:** https://github.com/tyrionros/iam_security_canvas

**Last Updated:** May 4, 2026
