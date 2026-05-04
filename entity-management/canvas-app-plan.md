# Canvas App Plan: IAM Security Entity Management

## App Requirements

This is an IAM (Identity & Access Management) Security Entity Management application designed for enterprise administrators to efficiently manage, monitor, and audit identity entities across systems. The app provides a centralized platform for viewing entities in a grid-based format with quick-access cards, detailed entity management through forms, and a streamlined interface for cross-system administration.

Key user stories:
- View all entities in a responsive data grid with sorting and filtering
- Navigate to entity details with a clean, accessible form interface
- Create new entities through a dedicated form screen
- Manage entity lifecycle with clear state transitions
- Monitor entity status and access patterns
- Audit trail visibility for compliance requirements

## Working Directory

All `.pa.yaml` files are written to:
`/c/Users/JanMichaelSullano/IAM_Security_Canvas/entity-management`

## Discovery Summary

- Controls available: 50+ — notable for this app: ModernCard, DataGrid, EntityForm, ModernText, ModernButton, GroupContainer (AutoLayout variant)
- Data sources: None connected (will use mock data collections)
- Connectors: None connected (future connector integration pattern prepared)

## Screens

| Screen | File | Purpose | Key Controls |
|--------|------|---------|--------------|
| Dashboard | Dashboard.pa.yaml | Landing screen with quick-access entity cards and summary statistics | ModernCard, ModernText, ModernButton, GroupContainer |
| Entity Grid | EntityGrid.pa.yaml | Tabular view of all entities with sorting, filtering, and selection | DataGrid, ModernButton, ModernText, GroupContainer |
| Entity Details | EntityDetails.pa.yaml | Detailed view and edit form for selected entity with full audit trail | EntityForm, ModernText, ModernButton, GroupContainer |
| Create Entity | CreateEntity.pa.yaml | Form-driven creation of new entities with validation and confirmation | EntityForm, ModernButton, ModernText, GroupContainer |

## Aesthetic Direction

The app uses a **data-dense, professional enterprise dashboard** aesthetic with clear information hierarchy, strategic color coding for status, and high-contrast elements for accessibility.

### Color Palette

- **Primary Background:** RGBA(245, 245, 247, 1) — Light neutral gray, professional and clean
- **Secondary Background:** RGBA(255, 255, 255, 1) — Pure white for content areas and cards
- **Accent Color (Primary Actions):** RGBA(34, 177, 76, 1) — Matrix green, signifies "active," "secure," and "approved" states
- **Accent Color (Secondary):** RGBA(26, 118, 188, 1) — Professional blue for navigation and secondary actions
- **Text Primary:** RGBA(51, 51, 51, 1) — Dark gray for maximum readability
- **Text Secondary:** RGBA(102, 102, 102, 1) — Medium gray for supporting text
- **Border Color:** RGBA(200, 200, 200, 1) — Subtle gray for visual separation
- **Status Colors:**
  - Active/Success: RGBA(34, 177, 76, 1) — Matrix green
  - Warning/Attention: RGBA(255, 193, 7, 1) — Amber
  - Error/Inactive: RGBA(244, 67, 54, 1) — Red
  - Neutral/Pending: RGBA(158, 158, 158, 1) — Gray

### Typography Scale

- **Page Headers:** 28px, FontWeight.Bold, RGBA(51, 51, 51, 1)
- **Section Headers:** 20px, FontWeight.Bold, RGBA(51, 51, 51, 1)
- **Subheaders/Labels:** 14px, FontWeight.Semibold, RGBA(102, 102, 102, 1)
- **Body Text:** 14px, FontWeight.Normal, RGBA(51, 51, 51, 1)
- **Small/Caption Text:** 12px, FontWeight.Normal, RGBA(102, 102, 102, 1)

### Layout Strategy

**VerticalAutoLayout with responsive containers:** All screens use `GroupContainer` with `Variant: AutoLayout` and `LayoutDirection: =LayoutDirection.Vertical` as the root container. This ensures:

1. **Responsive design:** Screens adapt to various device sizes
2. **Logical flow:** Content stacks vertically with semantic ordering
3. **Consistent spacing:** `LayoutGap` property maintains uniform distances between sections
4. **Scrollability:** Tall content areas use `LayoutOverflowY: =LayoutOverflow.Scroll` for graceful overflow handling
5. **Nested horizontal layouts:** Header rows and button groups use horizontal AutoLayout for side-by-side alignment

**Child spacing:** Padding is applied at the container level (PaddingTop/Bottom/Left/Right) with interior gaps managed by `LayoutGap`. This creates breathing room and visual hierarchy.

### Visual Details

- **Shadows:** ModernCard uses `DropShadow: =DropShadow.Semilight` for subtle elevation
- **Borders:** GroupContainers use `BorderThickness: =1` with `BorderColor: =RGBA(200, 200, 200, 1)` for visual definition
- **Border Radius:** Cards and containers use `BorderRadius: =8` (or equivalent via RadiusTopLeft/Right/BottomLeft/Right) for modern, approachable appearance
- **Transparency:** Status badges and overlay hints use RGBA alpha < 1 for layering without obscuring content

## Named Variables and Shared State

All screen builders must use these exact variable names for consistency:

### App-Level Variables (initialized in App.OnVisible)

```
selectedEntity: {ID: "", Name: "", Status: "", Owner: "", Created: "", LastModified: "", AccessLevel: ""}
isLoading: false
searchQuery: ""
filterStatus: "All"
currentScreen: "Dashboard"
```

### Collections (mock data)

```
entityCollection: [{ID, Name, Status, Owner, Created, LastModified, AccessLevel, Description}]
statusOptions: [{Value: "Active", Display: "Active"}, {Value: "Inactive", Display: "Inactive"}, {Value: "Suspended", Display: "Suspended"}]
```

### Screen-Specific Variables

Each screen initializes its own variables in `OnVisible`:

- **Dashboard:** recentEntities, totalActiveCount, pendingAuditCount
- **EntityGrid:** sortField, sortDirection, filteredEntities
- **EntityDetails:** isEditMode, unsavedChanges
- **CreateEntity:** formData, validationErrors

## Control Definitions

### ModernCard

```
Control ModernCard
Family: React

Input Properties (21):
  - AccessibleLabel: Text
  - BorderRadius: Number
  - ContentLanguage: Text
  - Description: Text
  - DisplayMode: Enum (Disabled, Edit, View)
  - DropShadow: Enum (Bold, ExtraBold, Light, None, Regular, Semibold, Semilight)
  - HeaderImage: Image
  - HeaderImageAccessibleLabel: Text
  - Height: Number
  - Image: Image
  - ImageAccessibleLabel: Text
  - ImagePlacement: Enum (AfterHeader, BeforeHeader)
  - ImagePosition: Enum (Center, Fill, Fit, Stretch, Tile)
  - LayoutDirection: Enum (Horizontal, Vertical)
  - OnSelect: Boolean
  - Subtitle: Text
  - Title: Text
  - Visible: Boolean
  - Width: Number
  - X: Number
  - Y: Number

Additional input properties if a child of a Vertical or Horizontal GroupContainer:
  - LayoutMinWidth: Number
  - LayoutMaxWidth: Number
  - LayoutMinHeight: Number
  - LayoutMaxHeight: Number
  - FillPortions: Number
  - AlignInContainer: Enum (SetByContainer, Start, Center, End, Stretch)

Additional input properties if a child of a Grid GroupContainer:
  - LayoutGridColumnStart: Number
  - LayoutGridColumnEnd: Number
  - LayoutGridRowStart: Number
  - LayoutGridRowEnd: Number

Output Properties (20):
  - AccessibleLabel: Text
  - BorderRadius: Number
  - ContentLanguage: Text
  - Description: Text
  - DisplayMode: Enum
  - DropShadow: Enum
  - HeaderImage: Image
  - HeaderImageAccessibleLabel: Text
  - Height: Number
  - Image: Image
  - ImageAccessibleLabel: Text
  - ImagePlacement: Enum
  - ImagePosition: Enum
  - LayoutDirection: Enum
  - Subtitle: Text
  - Title: Text
  - Visible: Boolean
  - Width: Number
  - X: Number
  - Y: Number
```

### DataGrid

```
Control DataGrid
Family: Classic

Input Properties (25):
  - BorderColor: Color
  - BorderStyle: Enum (Dashed, Dotted, None, Solid)
  - BorderThickness: Number
  - Color: Color
  - ContentLanguage: Text
  - Fill: Color
  - Font: Enum (Arial, Courier New, Dancing Script, Georgia, Great Vibes, Lato, Lato Black, Lato Hairline, Lato Light, Open Sans, Open Sans Condensed, Patrick Hand, Segoe UI, Verdana)
  - FontWeight: Enum (Bold, Lighter, Normal, Semibold)
  - HeadingColor: Color
  - HeadingFill: Color
  - HeadingFont: Enum (same font options as Font)
  - HeadingFontWeight: Enum (Bold, Lighter, Normal, Semibold)
  - HeadingSize: Number
  - Height: Number
  - HoverColor: Color
  - HoverFill: Color
  - Items: Table
  - NoDataText: Text
  - SelectedColor: Color
  - SelectedFill: Color
  - Size: Number
  - Visible: Boolean
  - Width: Number
  - X: Number
  - Y: Number

Additional input properties if a child of a Vertical or Horizontal GroupContainer:
  - LayoutMinWidth: Number
  - LayoutMaxWidth: Number
  - LayoutMinHeight: Number
  - LayoutMaxHeight: Number
  - FillPortions: Number
  - AlignInContainer: Enum (SetByContainer, Start, Center, End, Stretch)

Additional input properties if a child of a Grid GroupContainer:
  - LayoutGridColumnStart: Number
  - LayoutGridColumnEnd: Number
  - LayoutGridRowStart: Number
  - LayoutGridRowEnd: Number

Output Properties (25):
  - BorderColor: Color
  - BorderStyle: Enum
  - BorderThickness: Number
  - Color: Color
  - ContentLanguage: Text
  - Fill: Color
  - Font: Enum
  - FontWeight: Enum
  - HeadingColor: Color
  - HeadingFill: Color
  - HeadingFont: Enum
  - HeadingFontWeight: Enum
  - HeadingSize: Number
  - Height: Number
  - HoverColor: Color
  - HoverFill: Color
  - NoDataText: Text
  - Selected: Record
  - SelectedColor: Color
  - SelectedFill: Color
  - Size: Number
  - Visible: Boolean
  - Width: Number
  - X: Number
  - Y: Number
```

### EntityForm

```
Control EntityForm
Family: Classic

Input Properties (26):
  - BorderColor: Color
  - BorderStyle: Enum (Dashed, Dotted, None, Solid)
  - BorderThickness: Number
  - ContentLanguage: Text
  - DataSource: Table
  - DisabledTextColor: Color
  - Fill: Color
  - Font: Enum (Arial, Courier New, Dancing Script, Georgia, Great Vibes, Lato, Lato Black, Lato Hairline, Lato Light, Open Sans, Open Sans Condensed, Patrick Hand, Segoe UI, Verdana)
  - FontWeight: Enum (Bold, Lighter, Normal, Semibold)
  - Height: Number
  - InputBackgroundColor: Color
  - InputTextColor: Color
  - Item: Record
  - OnFailure: Boolean
  - OnFieldSelect: Boolean
  - OnSuccess: Boolean
  - Pattern: Enum (CardList, Details, List, None)
  - PrimaryColor1: Color
  - PrimaryColor2: Color
  - PrimaryColor3: Color
  - SelectableFields: Record
  - TextColor: Color
  - Visible: Boolean
  - Width: Number
  - X: Number
  - Y: Number

Additional input properties if a child of a Vertical or Horizontal GroupContainer:
  - LayoutMinWidth: Number
  - LayoutMaxWidth: Number
  - LayoutMinHeight: Number
  - LayoutMaxHeight: Number
  - FillPortions: Number
  - AlignInContainer: Enum (SetByContainer, Start, Center, End, Stretch)

Additional input properties if a child of a Grid GroupContainer:
  - LayoutGridColumnStart: Number
  - LayoutGridColumnEnd: Number
  - LayoutGridRowStart: Number
  - LayoutGridRowEnd: Number

Output Properties (23):
  - BorderColor: Color
  - BorderStyle: Enum
  - BorderThickness: Number
  - ContentLanguage: Text
  - DisabledTextColor: Color
  - Fill: Color
  - Font: Enum
  - FontWeight: Enum
  - Height: Number
  - InputBackgroundColor: Color
  - InputTextColor: Color
  - Mode: Enum
  - PrimaryColor1: Color
  - PrimaryColor2: Color
  - PrimaryColor3: Color
  - Selected: Record
  - SelectedField: Record
  - TextColor: Color
  - Unsaved: Boolean
  - Visible: Boolean
  - Width: Number
  - X: Number
  - Y: Number
```

### ModernText

```
Control ModernText
Family: React

Input Properties (32):
  - Align: Enum (Center, Justify, Left, Right)
  - AutoHeight: Boolean
  - BorderColor: Color
  - BorderStyle: Enum (Dashed, Dotted, None, Solid)
  - BorderThickness: Number
  - Color: Color
  - ContentLanguage: Text
  - DisplayMode: Enum (Disabled, Edit, View)
  - Fill: Color
  - Font: Enum (Arial, Courier New, Dancing Script, Georgia, Great Vibes, Lato, Lato Black, Lato Hairline, Lato Light, Open Sans, Open Sans Condensed, Patrick Hand, Segoe UI, Verdana)
  - FontWeight: Enum (Bold, Lighter, Normal, Semibold)
  - Height: Number
  - Italic: Boolean
  - OnSelect: Boolean
  - PaddingBottom: Number
  - PaddingLeft: Number
  - PaddingRight: Number
  - PaddingTop: Number
  - RadiusBottomLeft: Number
  - RadiusBottomRight: Number
  - RadiusTopLeft: Number
  - RadiusTopRight: Number
  - Size: Number
  - Strikethrough: Boolean
  - Text: Text
  - Underline: Boolean
  - VerticalAlign: Enum (Bottom, Middle, Top)
  - Visible: Boolean
  - Width: Number
  - Wrap: Boolean
  - X: Number
  - Y: Number

Additional input properties if a child of a Vertical or Horizontal GroupContainer:
  - LayoutMinWidth: Number
  - LayoutMaxWidth: Number
  - LayoutMinHeight: Number
  - LayoutMaxHeight: Number
  - FillPortions: Number
  - AlignInContainer: Enum (SetByContainer, Start, Center, End, Stretch)

Additional input properties if a child of a Grid GroupContainer:
  - LayoutGridColumnStart: Number
  - LayoutGridColumnEnd: Number
  - LayoutGridRowStart: Number
  - LayoutGridRowEnd: Number

Output Properties (31):
  - Align: Enum
  - AutoHeight: Boolean
  - BorderColor: Color
  - BorderStyle: Enum
  - BorderThickness: Number
  - Color: Color
  - ContentLanguage: Text
  - DisplayMode: Enum
  - Fill: Color
  - Font: Enum
  - FontWeight: Enum
  - Height: Number
  - Italic: Boolean
  - PaddingBottom: Number
  - PaddingLeft: Number
  - PaddingRight: Number
  - PaddingTop: Number
  - RadiusBottomLeft: Number
  - RadiusBottomRight: Number
  - RadiusTopLeft: Number
  - RadiusTopRight: Number
  - Size: Number
  - Strikethrough: Boolean
  - Text: Text
  - Underline: Boolean
  - VerticalAlign: Enum
  - Visible: Boolean
  - Width: Number
  - Wrap: Boolean
  - X: Number
  - Y: Number
```

### ModernButton

```
Control ModernButton
Family: React

Input Properties (37):
  - AccessibleLabel: Text
  - Align: Enum (Center, Justify, Left, Right)
  - Appearance: Enum (Outline, Primary, Secondary, Subtle, Transparent)
  - BasePaletteColor: Color
  - BorderColor: Color
  - BorderStyle: Enum (Dashed, Dotted, None, Solid)
  - BorderThickness: Number
  - Color: Color
  - ContentLanguage: Text
  - DisplayMode: Enum (Disabled, Edit, View)
  - Font: Enum (Arial, Courier New, Dancing Script, Georgia, Great Vibes, Lato, Lato Black, Lato Hairline, Lato Light, Open Sans, Open Sans Condensed, Patrick Hand, Segoe UI, Verdana)
  - FontWeight: Enum (Bold, Lighter, Normal, Semibold)
  - Height: Number
  - Icon: Text
  - IconRotation: Number
  - IconStyle: Enum (Filled, Outline)
  - Italic: Boolean
  - Layout: Enum (IconAfter, IconBefore, IconOnly, TextOnly)
  - OnSelect: Boolean
  - PaddingBottom: Number
  - PaddingLeft: Number
  - PaddingRight: Number
  - PaddingTop: Number
  - RadiusBottomLeft: Number
  - RadiusBottomRight: Number
  - RadiusTopLeft: Number
  - RadiusTopRight: Number
  - Size: Number
  - Strikethrough: Boolean
  - Text: Text
  - Tooltip: Text
  - Underline: Boolean
  - VerticalAlign: Enum (Bottom, Middle, Top)
  - Visible: Boolean
  - Width: Number
  - X: Number
  - Y: Number

Additional input properties if a child of a Vertical or Horizontal GroupContainer:
  - LayoutMinWidth: Number
  - LayoutMaxWidth: Number
  - LayoutMinHeight: Number
  - LayoutMaxHeight: Number
  - FillPortions: Number
  - AlignInContainer: Enum (SetByContainer, Start, Center, End, Stretch)

Additional input properties if a child of a Grid GroupContainer:
  - LayoutGridColumnStart: Number
  - LayoutGridColumnEnd: Number
  - LayoutGridRowStart: Number
  - LayoutGridRowEnd: Number

Output Properties (31):
  - AccessibleLabel: Text
  - Align: Enum
  - BasePaletteColor: Color
  - BorderColor: Color
  - BorderStyle: Enum
  - BorderThickness: Number
  - Color: Color
  - ContentLanguage: Text
  - DisplayMode: Enum
  - Font: Enum
  - FontWeight: Enum
  - Height: Number
  - Italic: Boolean
  - PaddingBottom: Number
  - PaddingLeft: Number
  - PaddingRight: Number
  - PaddingTop: Number
  - RadiusBottomLeft: Number
  - RadiusBottomRight: Number
  - RadiusTopLeft: Number
  - RadiusTopRight: Number
  - Size: Number
  - Strikethrough: Boolean
  - Text: Text
  - Tooltip: Text
  - Underline: Boolean
  - VerticalAlign: Enum
  - Visible: Boolean
  - Width: Number
  - X: Number
  - Y: Number
```

### GroupContainer

```
Control GroupContainer
Family: Classic

Variants (3):
  - AutoLayout
  - GridLayout
  - ManualLayout

Input Properties (all variants, 20):
  - BorderColor: Color
  - BorderStyle: Enum (Dashed, Dotted, None, Solid)
  - BorderThickness: Number
  - ContentLanguage: Text
  - DropShadow: Enum (Bold, ExtraBold, Light, None, Regular, Semibold, Semilight)
  - EnableChildFocus: Boolean
  - Fill: Color
  - Height: Number
  - PaddingBottom: Number
  - PaddingLeft: Number
  - PaddingRight: Number
  - PaddingTop: Number
  - RadiusBottomLeft: Number
  - RadiusBottomRight: Number
  - RadiusTopLeft: Number
  - RadiusTopRight: Number
  - Visible: Boolean
  - Width: Number
  - X: Number
  - Y: Number

Additional input properties for Vertical or Horizontal AutoLayout:
  - LayoutAlignItems: Enum (Center, End, Start, Stretch)
  - LayoutDirection: Enum (Horizontal, Vertical)
  - LayoutGap: Number
  - LayoutJustifyContent: Enum (Center, End, SpaceBetween, Start)
  - LayoutOverflowX: Enum (Hide, Scroll)
  - LayoutOverflowY: Enum (Hide, Scroll)
  - LayoutWrap: Boolean

Additional input properties for GridLayout:
  - ChildTabPriority: Boolean
  - LayoutGap: Number
  - LayoutGridColumnMinWidth: Number
  - LayoutGridColumns: Number
  - LayoutGridRowMinHeight: Number
  - LayoutGridRows: Number
  - LayoutOverflowX: Enum (Hide, Scroll)
  - LayoutOverflowY: Enum (Hide, Scroll)

Additional input properties for ManualLayout:
  - ChildTabPriority: Boolean

Additional input properties if a child of a Vertical or Horizontal GroupContainer:
  - LayoutMinWidth: Number
  - LayoutMaxWidth: Number
  - LayoutMinHeight: Number
  - LayoutMaxHeight: Number
  - FillPortions: Number
  - AlignInContainer: Enum (SetByContainer, Start, Center, End, Stretch)

Additional input properties if a child of a Grid GroupContainer:
  - LayoutGridColumnStart: Number
  - LayoutGridColumnEnd: Number
  - LayoutGridRowStart: Number
  - LayoutGridRowEnd: Number

Output Properties (25):
  - BorderColor: Color
  - BorderStyle: Enum
  - BorderThickness: Number
  - ChildTabPriority: Boolean
  - ContentLanguage: Text
  - DropShadow: Enum
  - EnableChildFocus: Boolean
  - Fill: Color
  - Height: Number
  - LayoutGridColumnMinWidth: Number
  - LayoutGridColumns: Number
  - LayoutGridRowMinHeight: Number
  - LayoutGridRows: Number
  - PaddingBottom: Number
  - PaddingLeft: Number
  - PaddingRight: Number
  - PaddingTop: Number
  - RadiusBottomLeft: Number
  - RadiusBottomRight: Number
  - RadiusTopLeft: Number
  - RadiusTopRight: Number
  - Visible: Boolean
  - Width: Number
  - X: Number
  - Y: Number
```

## Per-Screen Specifications

### Dashboard

- **File:** Dashboard.pa.yaml
- **Purpose:** Landing screen showing quick-access entity cards with at-a-glance status summaries, actionable shortcuts, and system-wide statistics. Designed for rapid orientation and immediate access to high-priority entities.
- **Layout:** VerticalAutoLayout root container (`GroupContainer` with `Variant: AutoLayout`, `LayoutDirection: =LayoutDirection.Vertical`)
- **Key Controls:**
  - **Header Section (Horizontal Container):** Title + Search bar
  - **Quick Stats Cards (Horizontal Container):** ModernCard controls showing total entities, active count, pending audits
  - **Recent Entities Section (Vertical Container):** ModernCard array of 5 most recently modified entities with click-to-navigate
  - **Action Buttons (Horizontal Container):** "View All Entities" (primary), "Create New Entity" (secondary), "Refresh" (tertiary)
- **Data Binding:**
  - `entityCollection` populated with mock data in App.OnStart
  - `recentEntities` filtered and sorted by LastModified in screen OnVisible
  - `totalActiveCount` calculated from entityCollection with status filter
  - `pendingAuditCount` tracked from audit metadata
- **Navigation:**
  - ModernCard OnSelect → Navigate to EntityDetails with selectedEntity set
  - "View All Entities" button → Navigate to EntityGrid screen
  - "Create New Entity" button → Navigate to CreateEntity screen
- **State:** 
  - OnVisible initializes recentEntities, totalActiveCount, pendingAuditCount
  - Screen variables: recentEntities (Table), totalActiveCount (Number), pendingAuditCount (Number)

### Entity Grid

- **File:** EntityGrid.pa.yaml
- **Purpose:** Comprehensive tabular view of all entities with multi-column display, sorting, and filtering capabilities. Designed for power users who need to scan, filter, and bulk-select entities for batch operations.
- **Layout:** VerticalAutoLayout root with dual-section structure: filter toolbar + scrollable data grid
- **Key Controls:**
  - **Filter Toolbar (Horizontal Container):** Search input, Status dropdown filter, Sort order toggle
  - **DataGrid Control:** All entities with columns: ID, Name, Status (color-coded), Owner, Created, LastModified, AccessLevel
  - **Action Button Bar (Horizontal Container):** "View Details" (primary, enabled on selection), "Create New" (secondary), "Back to Dashboard" (tertiary)
- **Data Binding:**
  - Items: `Filter(entityCollection, If(searchQuery <> "", Name @> searchQuery, true) && If(filterStatus <> "All", Status = filterStatus, true))`
  - DataGrid Selected property binds to app-level selectedEntity
  - Status column uses conditional color coding (Active: green, Inactive: gray, Suspended: amber)
- **Navigation:**
  - DataGrid row click → Navigate to EntityDetails with selectedEntity populated
  - "View Details" button → Navigate to EntityDetails (guard: check if entity selected)
  - "Create New" button → Navigate to CreateEntity
  - "Back to Dashboard" button → Navigate back to Dashboard
- **State:**
  - OnVisible initializes sortField, sortDirection, filteredEntities
  - Real-time filtering on search and filter dropdowns via Set() calls
  - Screen variables: sortField (Text), sortDirection (Text), filteredEntities (Table)

### Entity Details

- **File:** EntityDetails.pa.yaml
- **Purpose:** Read-only or editable detail view of a selected entity with full form display, audit trail, and edit/save/cancel workflow. Designed for in-depth examination and modification of entity attributes.
- **Layout:** VerticalAutoLayout root with three sections: header + scrollable form + action buttons
- **Key Controls:**
  - **Header Section (Horizontal Container):** Back button + Entity name as title + Status badge (color-coded)
  - **EntityForm Control:** Full entity form with fields for ID, Name, Status, Owner, Created, LastModified, AccessLevel, Description (read-only by default)
  - **Audit Trail Section (Vertical Container, expandable):** ModernText showing last 5 audit log entries with timestamps
  - **Action Button Bar (Horizontal Container):** "Edit" (primary, conditional), "Save" (appears in edit mode), "Cancel" (appears in edit mode), "Delete" (secondary, red), "Back" (tertiary)
- **Data Binding:**
  - EntityForm Item: selectedEntity (record from entityCollection)
  - EntityForm DisplayMode: toggles based on isEditMode variable (Edit/View)
  - Audit trail populated from mock auditLog collection filtered by selectedEntity.ID
  - Status badge color: conditional RGBA based on selectedEntity.Status
- **Navigation:**
  - Back button → Navigate to EntityGrid
  - Edit button → Set isEditMode = true, enable form editing
  - Save button → Update selectedEntity in entityCollection, Set isEditMode = false
  - Delete button → Show confirmation dialog, remove from entityCollection, navigate to EntityGrid
  - Cancel button → Reset form values, Set isEditMode = false
- **State:**
  - OnVisible: Load selectedEntity details, initialize isEditMode = false, load audit trail
  - Screen variables: isEditMode (Boolean), unsavedChanges (Boolean), auditTrail (Table), editedEntity (Record)

### Create Entity

- **File:** CreateEntity.pa.yaml
- **Purpose:** Form-driven interface for creating new entities with guided input fields, inline validation, and confirmation. Designed to streamline entity creation with minimal errors.
- **Layout:** VerticalAutoLayout root with centered, constrained form section and action buttons
- **Key Controls:**
  - **Header Section (Horizontal Container):** Title "Create New Entity" + subtitle "Enter entity details below"
  - **EntityForm Control:** Form with editable fields for Name, Owner (dropdown from users), Status (dropdown), AccessLevel (dropdown), Description (multi-line text)
  - **Validation Messages (Vertical Container, conditional):** ModernText showing validation errors for required fields
  - **Action Button Bar (Horizontal Container):** "Create" (primary, enabled only when valid), "Cancel" (secondary), "Reset Form" (tertiary)
- **Data Binding:**
  - EntityForm Item: formData record (initialized empty in OnVisible)
  - EntityForm Pattern: "Details" for clean single-form presentation
  - Validation errors: formData.Name <> "" && formData.Owner <> "" && formData.Status <> "" evaluated on each field change
  - Owner dropdown: items bound to mock users collection
  - Status dropdown: items bound to statusOptions collection
  - AccessLevel dropdown: hardcoded options (Basic, Standard, Advanced, Administrative)
- **Navigation:**
  - Create button → Validate formData, add new record to entityCollection, show success toast, navigate to EntityDetails with new entity
  - Cancel button → Discard formData, navigate back to EntityGrid (guard: ask for confirmation if unsavedChanges = true)
  - Reset Form button → Clear formData, reset validation errors
- **State:**
  - OnVisible: Initialize formData as empty record, set validationErrors to false
  - Form field OnChange: Update formData property and re-evaluate validationErrors
  - Screen variables: formData (Record), validationErrors (Boolean), createdEntityID (Text)

## TechnicalGuide Key Conventions

All screen builders must adhere to these YAML syntax rules:

### Formula Prefix

All formulas must begin with `=` prefix. Without it, Power Fx interprets the value as plain text.

```yaml
# CORRECT
Text: =firstName & " " & lastName
Visible: =isEnabled

# WRONG - no formula evaluation
Text: firstName & " " & lastName
```

### Multi-line Formulas

Use `|-` block scalar for formulas spanning multiple lines. The `=` prefix goes on the FIRST content line, not the `|-` line:

```yaml
# CORRECT
OnSelect: |-
  =Set(x, 1);
  Set(y, 2);
  Set(z, 3)

# WRONG - = on the |- line
OnSelect: =|-
  Set(x, 1);
  Set(y, 2)

# WRONG - missing = on first line
OnSelect: |-
  Set(x, 1);
  Set(y, 2)
```

### String Quoting Rules

Strings containing `: ` (colon followed by space) must be wrapped in quotes because YAML treats `key: value` as a mapping:

```yaml
# CORRECT
Text: ="Enter value: test"
HintText: ="Label: Please enter your name"

# WRONG - YAML interprets "value:" as a mapping key
Text: =Enter value: test
```

### Record Literal Syntax

Power Fx record literals like `{Value: "Tab1"}` must ALWAYS be wrapped in quotes in YAML. YAML parses `Value:` as a mapping key before Power Fx sees the formula:

```yaml
# CORRECT - outer quotes make the whole string YAML-safe
Default: "={Value: ""Tab1""}"

# ALSO CORRECT - single quotes avoid escaping inner quotes
Default: '={Value: "Tab1"}'

# WRONG - YAML parses Value: as a mapping key
Default: ={Value: "Tab1"}
```

This applies to any inline record literal: `Default`, `Selected`, inline `Items`, formula parameters, etc.

### Enum Escaping

Enum values or names containing spaces, special characters, or starting with numbers must be escaped with single quotes:

```yaml
# CORRECT - enum value starting with number
Precision: =DecimalPrecision.'2'

# CORRECT - enum with spaces in value
Status: ='Account Status'.Active

# CORRECT - control/enum with dots in name
Appearance: ='ButtonCanvas.Appearance'.Transparent
```

### RGBA Color Constants

Use explicit RGBA() function calls with exact values. Never abbreviate or use placeholders. All colors are specified as `RGBA(Red, Green, Blue, Alpha)` where Red/Green/Blue are 0-255 and Alpha is 0-1:

```yaml
# CORRECT
Fill: =RGBA(245, 245, 247, 1)
FontColor: =RGBA(51, 51, 51, 1)
BasePaletteColor: =RGBA(34, 177, 76, 1)

# ALSO CORRECT - using app-level named formula for consistency
Fill: =AppBgColor
BasePaletteColor: =MatrixGreen
```

For this app, all color references are defined as named formulas in App.Formulas (see App.pa.yaml).

### Conditional Properties

Nearly any property can use conditional formulas with If():

```yaml
DisplayMode: =If(isDisabled, DisplayMode.Disabled, DisplayMode.Edit)
Visible: =searchQuery <> "" && matchingResults > 0
FontColor: =If(status = "Active", RGBA(34, 177, 76, 1), RGBA(158, 158, 158, 1))
```

### AutoLayout Spacing and Sizing

For AutoLayout containers, children use `FillPortions` instead of absolute Width:

```yaml
# CORRECT - FillPortions = 1 means take 1 proportional unit of space
FillPortions: =1

# CORRECT - FillPortions = 0 means fixed size, must set Width/Height
FillPortions: =0
Width: =200
Height: =40
```

Parent container controls spacing with `LayoutGap` and alignment with `LayoutAlignItems` and `LayoutJustifyContent`:

```yaml
Properties:
  LayoutDirection: =LayoutDirection.Horizontal
  LayoutGap: =16                              # 16 pixel spacing between children
  LayoutAlignItems: =LayoutAlignItems.Center # Vertical center alignment
  LayoutJustifyContent: =LayoutJustifyContent.SpaceBetween
```

### Scrollable Containers

For tall content that may overflow, enable vertical scrolling:

```yaml
LayoutOverflowY: =LayoutOverflow.Scroll
Height: =Parent.Height - 100                 # Constrain height to enable scrolling
```

### State Initialization

All screen variables must be initialized in screen `OnVisible`:

```yaml
OnVisible: |-
  =Set(selectedIndex, 0);
  Set(isLoading, false);
  Set(filteredList, entityCollection);
  Set(sortOrder, "ascending")
```

Never assume variable state persists between screen navigations.

### Date/Time Text Conversion

Always specify format strings in lowercase (mm, dd, yyyy, hh, etc.):

```yaml
Text: =Text(varDate, "dddd, mmmm d, yyyy")    # "Monday, January 15, 2024"
Text: =Text(Now(), "hh:mm:ss")                # "14:30:00"
```

---

This comprehensive plan document provides all information needed for screen builders to implement screens in parallel without calling MCP tools. Every screen builder should read this document in full before beginning implementation.
