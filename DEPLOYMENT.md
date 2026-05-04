# Deployment Guide - IAM Security Canvas

This guide provides step-by-step instructions for deploying the IAM Security Canvas application to your Power Apps environment.

## Table of Contents

1. [Pre-Deployment Checklist](#pre-deployment-checklist)
2. [Deployment Steps](#deployment-steps)
3. [Testing & Validation](#testing--validation)
4. [Publishing](#publishing)
5. [Sharing & Access](#sharing--access)
6. [User Onboarding](#user-onboarding)
7. [Troubleshooting](#troubleshooting)
8. [Post-Deployment](#post-deployment)

---

## Pre-Deployment Checklist

Before deploying, ensure you have completed the following:

- [ ] **Dataverse Environment Ready**
  - [ ] Dataverse tables created (Users, Accounts, Contacts, Bookable Resources)
  - [ ] Tables have required columns (ID, Name, Status, Owner, Created, LastModified, AccessLevel, Description)
  - [ ] Sample data populated for testing

- [ ] **Power Apps Environment**
  - [ ] Power Apps license assigned to deploying user (Per User or Pay-as-you-go)
  - [ ] Dataverse environment provisioned and accessible
  - [ ] Environment URL and organization ID noted

- [ ] **Application Ready**
  - [ ] All screens created in Power Apps Designer
  - [ ] DataGrid controls configured for each entity
  - [ ] Forms implemented for create/edit operations
  - [ ] Action buttons (Create, Edit, Deactivate, Delete) configured
  - [ ] Navigation between screens tested
  - [ ] Matrix green theme applied consistently
  - [ ] No broken formulas or errors in Power Fx

- [ ] **Documentation**
  - [ ] README.md reviewed and up-to-date
  - [ ] Configuration details documented
  - [ ] User guide prepared (if applicable)

---

## Deployment Steps

### Step 1: Verify App Configuration

#### In Power Apps Designer:

1. Navigate to https://make.powerapps.com
2. Select your environment (e.g., "Default")
3. Open the **IAM Security Canvas** app
4. Verify the app loads without errors

**Checklist:**
- [ ] App opens without errors
- [ ] All screens are visible in the screen navigator (left panel)
- [ ] Data sources show all 4 Dataverse tables connected
- [ ] No red warning icons or error messages

### Step 2: Test Data Connectivity

#### Verify Dataverse Connections:

1. Click **Data** in the left panel
2. Verify all four tables are listed:
   - [ ] Users
   - [ ] Accounts
   - [ ] Contacts
   - [ ] Bookable Resources

3. For each table, click to expand and verify columns are visible

**Expected Result:** All tables listed with correct columns displayed.

### Step 3: Validate Screen Functionality

#### Test Dashboard Screen:
1. Preview the app (click **Preview** button or press F5)
2. Verify the Dashboard screen loads
3. Check for quick-access cards and summary statistics
4. Verify "View All Entities" navigation buttons work

**Expected Result:** Dashboard displays without errors, cards are visible.

#### Test Entity Management Screens:
For each management screen (Users, Accounts, Contacts, Bookable Resources):

1. **DataGrid Display:**
   - [ ] DataGrid displays all records from the corresponding Dataverse table
   - [ ] Columns are properly formatted
   - [ ] Search/filter controls are functional
   - [ ] Sorting works (click column headers)

2. **Create Functionality:**
   - [ ] "Create New Entity" button opens the create form
   - [ ] Form fields are editable and accept input
   - [ ] Validation shows required field errors when fields are empty
   - [ ] "Create" button saves new record to Dataverse
   - [ ] Success message/navigation occurs after creation

3. **Edit Functionality:**
   - [ ] Select a record from DataGrid
   - [ ] Click "Edit" or "View Details" button
   - [ ] Form loads with existing data
   - [ ] Fields are editable
   - [ ] "Save" button updates the record in Dataverse

4. **Deactivate/Delete Functionality:**
   - [ ] "Deactivate" button sets record status to "Inactive"
   - [ ] "Delete" button shows confirmation dialog
   - [ ] Confirmation dialog has "Yes" and "No" options
   - [ ] Confirmed deletion removes record from Dataverse

5. **Navigation:**
   - [ ] Back buttons return to previous screens
   - [ ] Menu navigation works between all screens
   - [ ] No dead links or broken navigation

### Step 4: Verify Styling & Theme

1. Open each screen and verify:
   - [ ] Background colors match matrix green theme
   - [ ] Text colors are readable (green on dark or dark on light)
   - [ ] Buttons have consistent styling
   - [ ] Cards and containers have proper borders/shadows
   - [ ] Layout is responsive and centered

**Matrix Green Theme Verification:**
- Primary background: Black (#000000)
- Accent colors: Bright green (#00ff00, #39ff14)
- Text colors: Green and dark gray
- Status colors: Green (Active), Gray (Inactive), Amber (Suspended)

### Step 5: Performance Testing

1. In Preview mode, open the app
2. Test performance with the following:
   - [ ] Load time is acceptable (< 5 seconds for dashboard)
   - [ ] DataGrid loads quickly with 100+ records
   - [ ] Search/filter is responsive
   - [ ] Form submission is quick
   - [ ] Navigation between screens is smooth

**Performance Targets:**
- Dashboard load: < 3 seconds
- DataGrid load: < 2 seconds per 100 records
- Form submission: < 1 second
- Navigation transition: < 500ms

### Step 6: Save the App

1. In Power Apps Designer, click **File**
2. Select **Save**
3. Wait for the save confirmation message
4. Verify no errors appear in the notification panel

**Expected Result:** "Saved" confirmation appears in the top right.

---

## Testing & Validation

### Functional Testing Checklist

#### User Management:
- [ ] Create a new user record
- [ ] Edit the user record
- [ ] View user details
- [ ] Deactivate user
- [ ] Filter users by status
- [ ] Search for specific user

#### Account Management:
- [ ] Create a new account
- [ ] Edit account details
- [ ] Associate contacts to account
- [ ] Change account status
- [ ] Delete account with confirmation

#### Contact Management:
- [ ] Create contact record
- [ ] Link contact to account
- [ ] Edit contact information
- [ ] Mark contact as inactive
- [ ] Search contacts by name

#### Bookable Resources:
- [ ] Create bookable resource
- [ ] Set availability/capacity
- [ ] Edit resource details
- [ ] Deactivate resource
- [ ] View resource allocation

### Data Validation Testing

- [ ] Required fields show validation errors when empty
- [ ] Email fields validate email format (if applicable)
- [ ] Date fields accept only valid dates
- [ ] Dropdown fields show available options
- [ ] Status field restricts to valid values (Active, Inactive, Suspended)

### Cross-Browser Testing

Test in multiple browsers (if applicable):
- [ ] Chrome/Edge (latest version)
- [ ] Firefox (latest version)
- [ ] Safari (if supporting Mac users)

---

## Publishing

### Publish the App

1. In Power Apps Designer, click **File**
2. Select **Publish** (top right area)
3. Wait for the "Publish succeeded" message
4. Confirm the version number has incremented

**Expected Result:** Green success notification appears.

### Publish to Managed Solution (Optional - For production):

If deploying to production, consider packaging as a Managed Solution:

1. Go to Power Apps Admin Center
2. Navigate to **Solutions**
3. Click **New Solution**
4. Add the IAM Security Canvas app to the solution
5. Export as Managed Solution
6. Import to target environment

**Note:** This step is optional for testing environments.

---

## Sharing & Access

### Share with Users

#### Method 1: Direct Sharing (Individual Users)

1. In Power Apps, open the **IAM Security Canvas** app
2. Click **Share** button (top right)
3. Enter user email addresses or groups
4. Select permission level:
   - **Player** - Can use the app (recommended for end users)
   - **Editor** - Can edit the app (only for admins)
5. Click **Share**

#### Method 2: Security Group

1. Create an Azure AD Security Group (e.g., "IAM Admins")
2. Add users to the group
3. Share the app with the security group
4. All members automatically have access

#### Method 3: Share Link

1. Click **Share** button
2. Copy the **Share link**
3. Send link to users via email
4. Users can open the app directly from the link

### Permission Levels

| Permission | Can Use App | Can Edit App | Can Share |
|-----------|-----------|----------|----------|
| Player | ✅ | ❌ | ❌ |
| Editor | ✅ | ✅ | ✅ |
| Owner | ✅ | ✅ | ✅ |

**Recommendation:** Grant "Player" access to end users, "Editor" to admins only.

### Assign Roles (Optional - For Dataverse Access)

If using Dataverse security roles:

1. Go to Power Platform Admin Center
2. Select your environment
3. Go to **Dataverse** → **Security Roles**
4. Create or assign roles for:
   - **IAM Admin** - Full create, read, update, delete (CRUD)
   - **IAM Viewer** - Read-only access
   - **IAM Contributor** - Create and edit own records
5. Assign security roles to users

---

## User Onboarding

### User Training Materials

Prepare documentation for end users:

1. **Quick Start Guide**
   - How to access the app
   - Basic navigation
   - How to view entity records

2. **Feature Documentation**
   - How to create entities
   - How to edit records
   - How to deactivate entities
   - Status meanings (Active, Inactive, Suspended)

3. **Common Tasks**
   - Searching for a user
   - Updating user information
   - Creating a new account
   - Assigning access levels

### Rollout Plan

#### Phase 1: Pilot (1-2 weeks)
- [ ] Select 5-10 power users for testing
- [ ] Gather feedback
- [ ] Fix any issues
- [ ] Document learnings

#### Phase 2: Department Rollout (2-4 weeks)
- [ ] Train department heads
- [ ] Expand access to department teams
- [ ] Monitor usage and issues
- [ ] Provide support

#### Phase 3: Full Rollout
- [ ] Train all users
- [ ] Enable access organization-wide
- [ ] Establish support process
- [ ] Monitor adoption metrics

### Support Resources

1. **Help Documentation**
   - Link to README.md in GitHub
   - FAQs document
   - Video tutorials (optional)

2. **Support Contact**
   - Designate support team member
   - Email or Teams channel for questions
   - Response time SLA (e.g., 24 hours)

3. **Feedback Channel**
   - Mechanism to report issues
   - Feature request process
   - Bug report template

---

## Troubleshooting

### Common Issues & Solutions

#### Issue: DataGrid shows no data

**Causes:**
- Dataverse table not connected
- Table has no records
- Security permissions restrict access

**Solutions:**
1. Verify table is connected in Data panel
2. Check Dataverse table has data (via Dataverse admin center)
3. Verify user has read permissions on the table

#### Issue: Forms won't save data

**Causes:**
- Dataverse connection is broken
- User lacks write permissions
- Required fields are empty

**Solutions:**
1. Test connection by refreshing DataGrid
2. Verify user has write permissions
3. Check form validation messages
4. Review Power Fx formulas in OnSelect event

#### Issue: App loading slowly

**Causes:**
- Large dataset in DataGrid (1000+ rows)
- Slow network connection
- Complex formulas

**Solutions:**
1. Add filtering to DataGrid (show only recent records)
2. Use pagination for large datasets
3. Optimize formulas (avoid nested loops)
4. Check network performance

#### Issue: Navigation between screens broken

**Causes:**
- Screen name changed but button formula not updated
- Typo in navigation formula
- Screen doesn't exist

**Solutions:**
1. Verify all screen names match navigation formulas
2. Check button OnSelect formulas for Navigate() commands
3. Test each navigation path individually

#### Issue: Styling/Colors not displaying correctly

**Causes:**
- RGBA color values incorrect
- CSS overflow issues
- Browser cache

**Solutions:**
1. Verify RGBA values are in range 0-255 for RGB, 0-1 for Alpha
2. Clear browser cache (Ctrl+Shift+Delete)
3. Test in different browser
4. Verify containers have proper height/width

### Debug Mode

To enable debug mode in Power Apps:

1. In Power Apps Designer, press **Ctrl+Alt+D**
2. Open **Developer Tools** (F12)
3. Check Console for error messages
4. Review Network tab for data source calls

---

## Post-Deployment

### Monitor & Optimize

#### Week 1 (Post-Launch):
- [ ] Monitor error logs
- [ ] Collect user feedback
- [ ] Address critical issues immediately
- [ ] Track usage metrics

#### Month 1:
- [ ] Analyze user adoption rates
- [ ] Identify feature gaps
- [ ] Plan improvements
- [ ] Document common questions

#### Ongoing:
- [ ] Regular maintenance updates
- [ ] Security patches
- [ ] Performance optimization
- [ ] Feature enhancements

### Update Management

When deploying updates:

1. **Development**: Make changes in a dev environment
2. **Testing**: Validate changes thoroughly
3. **Staging**: Deploy to staging environment
4. **Production**: Schedule update during maintenance window
5. **Rollback Plan**: Have a version to revert to if needed

### Version Control

Track app versions in GitHub:

1. Create a `CHANGELOG.md` file
2. Document all releases
3. Tag releases in Git

**Example:**
```
## v1.1.0 - 2026-05-10
- Added batch deactivation feature
- Fixed DataGrid performance with 1000+ records
- Updated matrix green theme colors

## v1.0.0 - 2026-05-04
- Initial release
- Core CRUD operations
- Four entity management screens
```

### Backup & Recovery

1. **Regular Backups**
   - Export app periodically
   - Store backups in secure location
   - Document backup schedule

2. **Recovery Procedure**
   - Document how to restore from backup
   - Test recovery process quarterly
   - Maintain recovery time objective (RTO)

---

## Success Criteria

Your deployment is successful when:

✅ **Functionality**
- All screens load and display data
- CRUD operations work for all entities
- Navigation is smooth and intuitive
- Validation works as expected

✅ **Performance**
- App loads in < 5 seconds
- DataGrid displays records quickly
- Actions complete within 2 seconds

✅ **User Adoption**
- 80%+ of target users accessing app within first month
- Minimal support tickets
- Positive user feedback

✅ **Data Quality**
- All Dataverse tables consistently updated
- No data loss or corruption
- Audit trail maintained

✅ **Security**
- Only authorized users have access
- Data access controlled by Dataverse roles
- No sensitive data exposed

---

## Contact & Support

For deployment assistance or issues:

- **Repository**: https://github.com/tyrionros/iam_security_canvas
- **Documentation**: See README.md
- **Issues**: Report in GitHub Issues section

---

**Last Updated:** May 4, 2026

**Deployment Guide Version:** 1.0
