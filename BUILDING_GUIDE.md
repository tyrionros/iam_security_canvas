# Step-by-Step Building Guide - IAM Security Canvas

Complete instructions for manually building all screens in Power Apps Designer.

## Table of Contents

1. [Before You Start](#before-you-start)
2. [Dashboard Screen](#dashboard-screen)
3. [Users Grid Screen](#users-grid-screen)
4. [Accounts Grid Screen](#accounts-grid-screen)
5. [Contacts Grid Screen](#contacts-grid-screen)
6. [Bookable Resources Grid Screen](#bookable-resources-grid-screen)
7. [Entity Details Screen](#entity-details-screen)
8. [Create Entity Screen](#create-entity-screen)
9. [Navigation Setup](#navigation-setup)
10. [Theme Application](#theme-application)

---

## Before You Start

### Open Power Apps Designer

1. Navigate to https://make.powerapps.com
2. Select your environment
3. Open the **IAM Security Canvas** app
4. Click **Edit** to enter the designer

### Color Palette (Save These!)

Keep these colors handy for styling:

| Color Name | Hex | Use |
|-----------|-----|-----|
| Primary Background | #F5F5F7 | Screen backgrounds |
| White | #FFFFFF | Card/container backgrounds |
| Matrix Green | #22B14C | Active status, primary buttons |
| Professional Blue | #1A76BC | Secondary buttons |
| Dark Gray | #333333 | Primary text |
| Medium Gray | #666666 | Secondary text |
| Light Gray | #C8C8C8 | Borders |
| Status Active | #22B14C | Active badge |
| Status Inactive | #9E9E9E | Inactive badge |
| Status Suspended | #FFC107 | Suspended badge |

---

## Dashboard Screen

**Purpose:** Main landing screen with statistics and quick access to entity grids.

### Step 1: Create Screen Container

1. Click **+** in the left tree to add a new screen
2. Rename it to **"Dashboard"**
3. Set Screen **Fill** to color #F5F5F7 (Light gray)

### Step 2: Add Header Section

1. Insert **Rectangle** control
   - Width: `Parent.Width`
   - Height: `60`
   - Fill: White (#FFFFFF)
   - Border: Light gray (#C8C8C8), 1px
   - Corner radius: 8px

2. Add **Text** label inside
   - Text: `"IAM Security Dashboard"`
   - Font size: 28pt, Bold
   - Color: Dark gray (#333333)
   - X, Y position: (24, 8)

### Step 3: Add Statistics Cards (4 Cards)

Create 4 card components. Repeat for each:

#### Card 1: Total Entities

1. Insert **Rectangle** (card background)
   - Width: Auto, Height: 120px
   - Fill: White (#FFFFFF)
   - Shadow: Subtle
   - Corner radius: 8px

2. Add **Text** (title)
   - Text: `"Total Entities"`
   - Font size: 14pt, Semibold
   - Color: Dark gray (#333333)

3. Add **Text** (value)
   - Text: `"450"`
   - Font size: 28pt, Bold
   - Color: Matrix green (#22B14C)

#### Card 2: Active Count

Same structure as Card 1, but:
- Background Fill: Matrix green with 10% opacity
- Title: `"Active"`
- Value: `"388"`
- Value Color: Matrix green (#22B14C)

#### Card 3: Inactive Count

- Background Fill: Gray with 10% opacity
- Title: `"Inactive"`
- Value: `"45"`
- Value Color: Gray (#9E9E9E)

#### Card 4: Suspended Count

- Background Fill: Amber with 10% opacity
- Title: `"Suspended"`
- Value: `"17"`
- Value Color: Amber (#FFC107)

### Step 4: Add Recently Modified Section

1. Insert **Rectangle** (container)
   - Width: Parent.Width - 32px
   - Height: Auto
   - Fill: White
   - Border: 1px light gray
   - Corner radius: 8px
   - Padding: 20px

2. Add **Text** (section title)
   - Text: `"Recently Modified Entities"`
   - Font size: 20pt, Bold
   - Color: Dark gray

3. Add 3 **Card** or **Rectangle** items:
   - **Item 1:** "Alice Johnson (User) - Modified: Today"
   - **Item 2:** "Contoso Inc (Account) - Modified: Yesterday"
   - **Item 3:** "John Smith (Contact) - Modified: 2 days ago"

4. Set OnSelect for each card:
   - `Navigate(EntityDetails)`

### Step 5: Add Action Buttons

1. Insert **Button** (View All Entities)
   - Text: `"View All Entities"`
   - Fill: Matrix green (#22B14C)
   - Text Color: White
   - OnSelect: `Navigate(UsersGrid)`

2. Insert **Button** (Create New)
   - Text: `"Create New Entity"`
   - Fill: Professional blue (#1A76BC)
   - Text Color: White
   - OnSelect: `Navigate(CreateEntity)`

3. Insert **Button** (Refresh)
   - Text: `"Refresh"`
   - Fill: Light gray (#C8C8C8)
   - Text Color: Dark gray
   - OnSelect: `Refresh(Users); Refresh(Accounts); Refresh(Contacts); Refresh('Bookable Resources')`

---

## Users Grid Screen

**Purpose:** Display all users in a searchable, filterable data grid.

### Step 1: Create Screen

1. Add new screen, name it **"UsersGrid"**
2. Set Fill to light gray (#F5F5F7)

### Step 2: Add Header

1. **Rectangle** header (Height: 60px)
   - Fill: White
   - Border: 1px light gray
   - Corner radius: 8px

2. **Text** "Users" (24pt, Bold, Dark gray)

3. **Button** "← Back to Dashboard"
   - OnSelect: `Navigate(Dashboard)`

### Step 3: Add Filter Toolbar

1. **Rectangle** (Height: 50px)
   - Fill: White
   - Border: 1px light gray
   - Corner radius: 8px

2. **Text input** "Search users..."
   - Placeholder: "Search users..."
   - Width: Fill available space
   - Store in variable: `searchQuery`

3. **Dropdown** "Status Filter"
   - Items: `["All", "Active", "Inactive", "Suspended"]`
   - Default: "All"
   - Store in variable: `filterStatus`

### Step 4: Add DataGrid

1. Insert **Data Grid** control
   - Data source: **Users** (Dataverse table)
   - Columns to display:
     - ID
     - Name
     - Status (set color based on status)
     - Owner
     - Created
     - AccessLevel

2. **Add filtering formula:**
   - Filter settings: 
     - Include records where Name contains `searchQuery`
     - AND Status equals `filterStatus` (if not "All")

3. **Set row OnSelect:**
   - `Set(selectedEntity, ThisItem)`
   - `Navigate(EntityDetails)`

### Step 5: Add Action Buttons

1. **Button** "View Details"
   - OnSelect: `Navigate(EntityDetails)`
   - Disable if no row selected

2. **Button** "Create New User"
   - OnSelect: `Navigate(CreateEntity)`

3. **Button** "Back to Dashboard"
   - OnSelect: `Navigate(Dashboard)`

---

## Accounts Grid Screen

**Repeat the same process as Users Grid but:**

1. Screen name: **"AccountsGrid"**
2. Header text: **"Accounts"**
3. Data source: **Accounts** (Dataverse table)
4. Search placeholder: "Search accounts..."
5. DataGrid columns: ID, Name, Status, Owner, Created, AccessLevel
6. Create button text: "Create New Account"

---

## Contacts Grid Screen

**Repeat the same process as Users Grid but:**

1. Screen name: **"ContactsGrid"**
2. Header text: **"Contacts"**
3. Data source: **Contacts** (Dataverse table)
4. Search placeholder: "Search contacts..."
5. DataGrid columns: ID, Name, Status, Owner, Created, AccessLevel
6. Create button text: "Create New Contact"

---

## Bookable Resources Grid Screen

**Repeat the same process as Users Grid but:**

1. Screen name: **"BookableResourcesGrid"**
2. Header text: **"Bookable Resources"**
3. Data source: **Bookable Resources** (Dataverse table)
4. Search placeholder: "Search resources..."
5. DataGrid columns: ID, Name, Status, Owner, Created, AccessLevel
6. Create button text: "Create New Resource"

---

## Entity Details Screen

**Purpose:** View and edit individual entity records.

### Step 1: Create Screen

1. Add new screen, name it **"EntityDetails"**
2. Set Fill to light gray (#F5F5F7)

### Step 2: Add Header

1. **Rectangle** header
   - Height: 80px
   - Fill: White
   - Border: 1px light gray

2. **Button** "← Back"
   - OnSelect: `Back()`

3. **Text** (Entity Name)
   - Text: `selectedEntity.Name`
   - Font size: 24pt, Bold
   - Color: Dark gray

4. **Text** (Entity Type)
   - Text: `"User Account"` (or dynamic based on selection)
   - Font size: 12pt, Normal
   - Color: Medium gray

5. **Button** (Status Badge)
   - Text: `selectedEntity.Status`
   - Background color based on status:
     - Active: Matrix green
     - Inactive: Gray
     - Suspended: Amber
   - Disabled: true (read-only display)

### Step 3: Add Form Container

1. **Rectangle** (form background)
   - Fill: White
   - Border: 1px light gray
   - Corner radius: 8px
   - Padding: 24px

2. Add form fields as **Text Inputs** or **Dropdowns**:
   - **ID** (Text Input, read-only)
   - **Name** (Text Input, editable)
   - **Status** (Dropdown: Active, Inactive, Suspended)
   - **Owner** (Text Input, editable)
   - **AccessLevel** (Dropdown: Basic, Standard, Advanced, Administrative)
   - **Created** (Text, read-only)
   - **LastModified** (Text, read-only)

### Step 4: Add Audit Trail Section

1. **Rectangle** (audit background)
   - Fill: Light gray (#F5F5F7)
   - Border: 1px light gray
   - Height: Auto

2. **Text** "Audit Trail"
   - Font size: 14pt, Bold
   - Color: Dark gray

3. Add **Text items** showing:
   - "Status changed to Active - Today at 2:30 PM by admin@contoso.com"
   - "AccessLevel updated to Administrative - Yesterday at 10:15 AM by admin@contoso.com"

### Step 5: Add Action Buttons

1. **Button** "Save Changes"
   - Fill: Matrix green (#22B14C)
   - OnSelect: `Patch(Users, selectedEntity, {Name: NameInput.Value, Status: StatusDropdown.Value, ...}); Notify("Changes saved", NotificationType.Success)`

2. **Button** "Deactivate"
   - Fill: Amber (#FFC107)
   - OnSelect: `Patch(Users, selectedEntity, {Status: "Inactive"}); Notify("Entity deactivated", NotificationType.Information)`

3. **Button** "Delete"
   - Fill: Red (#F44336)
   - OnSelect: `If(Confirm("Are you sure?"), Remove(Users, selectedEntity); Navigate(UsersGrid))`

---

## Create Entity Screen

**Purpose:** Form for creating new entity records.

### Step 1: Create Screen

1. Add new screen, name it **"CreateEntity"**
2. Set Fill to light gray (#F5F5F7)

### Step 2: Add Header

1. **Rectangle** (Height: Auto)
   - Fill: White
   - Border: 1px light gray
   - Corner radius: 8px
   - Padding: 24px

2. **Text** "Create New Entity"
   - Font size: 28pt, Bold
   - Color: Dark gray

3. **Text** "Fill in the details below to create a new entity"
   - Font size: 14pt, Normal
   - Color: Medium gray

### Step 3: Add Form Container

1. **Rectangle** (form background)
   - Fill: White
   - Border: 1px light gray
   - Corner radius: 8px
   - Padding: 24px

2. Add input fields:

   **Entity Type** (Dropdown)
   - Items: ["User", "Account", "Contact", "Bookable Resource"]
   - Default: "User"
   - Required: Yes

   **Name/Title** (Text Input)
   - Placeholder: "Enter name or title"
   - Required: Yes

   **Owner** (Dropdown)
   - Items: User list from Users table
   - Required: Yes

   **Status** (Dropdown)
   - Items: ["Active", "Inactive", "Suspended"]
   - Default: "Active"
   - Required: Yes

   **Access Level** (Dropdown)
   - Items: ["Basic", "Standard", "Advanced", "Administrative"]
   - Default: "Standard"
   - Optional

   **Description** (Text Input - Multiline)
   - Placeholder: "Enter optional description"
   - Optional
   - Mode: Multiline

### Step 4: Add Validation Messages

1. **Rectangle** (error container - visible only if validation fails)
   - Fill: Light red (#FFF8F8)
   - Border: 1px red (#F44336)
   - Corner radius: 4px
   - Visible: `validationErrors`

2. **Text** "* Required fields must be completed before creating"
   - Color: Red (#F44336)
   - Font size: 11pt

### Step 5: Add Action Buttons

1. **Button** "Create Entity"
   - Fill: Matrix green (#22B14C)
   - Text Color: White
   - OnSelect: 
     ```
     If(
       And(NameInput.Value <> "", OwnerDropdown.Value <> "", StatusDropdown.Value <> ""),
       Patch(Users, Defaults(Users), {
         Name: NameInput.Value,
         Owner: OwnerDropdown.Value,
         Status: StatusDropdown.Value,
         AccessLevel: AccessLevelDropdown.Value,
         Description: DescriptionInput.Value
       });
       Notify("Entity created successfully!", NotificationType.Success);
       Navigate(EntityDetails),
       Set(validationErrors, true)
     )
     ```

2. **Button** "Cancel"
   - Fill: Light gray (#C8C8C8)
   - OnSelect: `Back()`

3. **Button** "Reset Form"
   - Fill: Medium gray (#666666)
   - OnSelect: `Set(validationErrors, false); Reset(NameInput); Reset(OwnerDropdown); Reset(StatusDropdown)`

---

## Navigation Setup

### Link Welcome to Dashboard

1. Open **Welcome** screen
2. Click main container
3. Set **OnSelect**: `Navigate(Dashboard)`

### Link All Grid Screens to Dashboard

1. Open each grid screen (Users, Accounts, Contacts, Resources)
2. Set **Back button OnSelect**: `Navigate(Dashboard)`
3. Set **View All/Create buttons** to navigate to respective screens

### Link Dashboard to Grids

1. Open **Dashboard** screen
2. Set stat cards OnSelect: `Navigate(UsersGrid)` (or respective grid)
3. Set "View All Entities" button: `Navigate(UsersGrid)`
4. Set "Create New Entity" button: `Navigate(CreateEntity)`

### Link Entity Details to Back

1. Open **EntityDetails** screen
2. Set **Back button**: `Back()` (returns to previous screen)
3. Set **Save/Delete buttons**: Return to appropriate grid

---

## Theme Application

### Apply Matrix Green Accent to All Screens

For each screen:

1. **Primary buttons** (Create, Save, View): Fill = `Color.Green` or #22B14C
2. **Status badges:**
   - Active: Green
   - Inactive: Gray
   - Suspended: Amber
3. **Headers:** Dark gray text on white background
4. **Borders:** 1px light gray (#C8C8C8)
5. **Corner radius:** 8px for major containers, 4px for inputs

### Typography Standards

- **Page headers:** 28pt, Bold, Dark gray
- **Section headers:** 20pt, Bold, Dark gray
- **Labels:** 14pt, Semibold, Dark gray
- **Body text:** 14pt, Normal, Dark gray
- **Captions:** 12pt, Normal, Medium gray

---

## Testing Checklist

After building all screens:

- [ ] Welcome screen loads and navigates to Dashboard
- [ ] Dashboard displays statistics correctly
- [ ] All grid screens load data from Dataverse
- [ ] Search filtering works on all grids
- [ ] Status filter works on all grids
- [ ] Clicking grid rows navigates to Entity Details
- [ ] Entity Details shows correct record data
- [ ] Save, Deactivate, Delete buttons work
- [ ] Create Entity form validates required fields
- [ ] Create Entity successfully adds new records
- [ ] All navigation back buttons work
- [ ] Matrix green theme applied consistently
- [ ] Colors match specification for all statuses

---

## Pro Tips

1. **Use Variables:** Store `selectedEntity`, `searchQuery`, `filterStatus` as global variables
2. **Reuse Containers:** Create a template Rectangle for cards to maintain consistency
3. **Test as You Go:** Preview each screen before moving to the next
4. **Naming Convention:** Keep control names descriptive (e.g., `UsersGrid_DataGrid`, `Dashboard_StatsCard1`)
5. **Backup:** Save frequently in Power Apps

---

## When You're Done

1. **Save the app** in Power Apps Designer
2. **Tell me:** "I've finished building all screens"
3. **I will:** Sync your app to GitHub and commit all changes

**Let me know when you start building!** 🚀

---

**Last Updated:** May 4, 2026

**Guide Version:** 1.0
