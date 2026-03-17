---
name: saas-wireframe-lofi
description: Generate low-fidelity (lo-fi) ASCII wireframes for SaaS web app flows and screens
input: SaaS context, screen or flow name, required elements, layout preferences, user roles
output: Text-based lo-fi wireframe(s) using ASCII box diagrams, one screen per section
---

## Purpose

Quickly generate low-fidelity (lo-fi) wireframes for SaaS web app flows and screens using text-based ASCII diagrams and established UX/UI patterns. The AI must adhere to the component specifications in this file and draw reusable layouts from `templates/`.

---

## How to Use

- Describe the SaaS context (e.g., team management, project tracking, CRM, analytics).
- Specify the flow or screen (e.g., registration, dashboard, create team, join team, onboarding).
- List all required elements (top nav, sidebar, footer, forms, tables, widgets) and their labels or actions.
- Indicate layout preferences (sidebar left/right, content center, etc.).
- Mention any special behaviors (hover states, validation, conditional content, modals, multi-page flows).
- Specify user roles if relevant (admin, manager, guest, etc.).
- The agent will ask clarifying questions if requirements are ambiguous or missing.
- When complete, the agent will suggest a file name and allow a custom name before saving.

---

## Example Prompts

- "Create a lo-fi wireframe for a user registration flow with email verification and profile completion."
- "Show a dashboard page after joining a team, with sidebar navigation and top nav."
- "Make a team join flow where the request button appears on hover for each team."
- "Design a 5-step onboarding workflow with progress indication."
- "Show an admin panel with user management and role assignment."

---

## Output Format

- Use ASCII/text diagrams for layout with clear box boundaries (`+`, `-`, `|`).
- Each list/table item appears on its own line for readability.
- Include all navigation (top nav, sidebar, footer) as needed.
- Clearly label all sections, actions, and states (success, error, pending, empty, loading).
- Indicate interactive elements (e.g., `[Request to Join]` (on hover)).
- For multi-page flows, show each page separately and indicate navigation (Next, Back, Finish).

---

## Best Practices

- Follow established SaaS UX/UI patterns and wireframe conventions.
- Keep wireframes simple — focus on structure, flow, and user journey, not visual design.
- Use clear, descriptive labels for all elements, actions, and states.
- Adapt to context (rename sidebar items, adjust layout for mobile/desktop).
- Show validation, error, and success states where relevant.
- For complex flows, provide a step-by-step breakdown with screen transitions.
- Use consistent terminology and structure across all wireframes.
- Annotate non-obvious behaviors or requirements.

---

## Component Specifications

The AI agent must use these specifications for all generated wireframes. No custom or experimental designs are allowed.

### 1. Home/Landing Page
- Clear value proposition and call-to-action (CTA)
- Brief overview of features/benefits
- Prominent sign-up/login buttons
- Visual hero section (image/illustration placeholder)

### 2. Top Navigation Bar
- Logo (top left)
- Main navigation links (dashboard, features, pricing, support)
- User avatar/profile menu (top right)
- Responsive: collapses to hamburger menu on mobile

### 3. Side Navigation/Menu
- Persistent on desktop, collapsible on mobile
- Links to main app sections (dashboard, lists, settings, admin)
- Highlight current section

### 4. Dashboard
- Overview widgets (stats, charts, recent activity)
- Quick links to key actions
- Modular layout (cards/tiles)

### 5. Lists/Tables
- Tabular data display
- Pagination, sorting, and filtering
- Bulk actions (select, delete, export)
- Row-level actions (edit, view, delete)

### 6. Search Bar/Filters
- Prominent placement above lists/tables
- Instant feedback (auto-suggest or filter)
- Clearable input

### 7. Login Form
- Email/username and password fields
- "Forgot password?" link
- Login button
- Error messages for invalid input

### 8. Registration/Sign Up Form
- Name, email, password fields
- Password strength indicator
- Terms and privacy agreement checkbox
- Sign up button
- Success/error feedback

### 9. Forgot/Reset Password
- Email input for reset link
- Confirmation message after submission
- New password entry (with confirmation)

### 10. User Profile & Settings
- Editable profile info (name, email, avatar)
- Change password option
- Notification preferences
- Account deletion (with confirmation)

### 11. Notifications/Alerts
- In-app notification bell or dropdown
- Toasts/snackbars for transient messages
- Error, success, info, and warning states

### 12. Modals/Dialogs
- For confirmations, forms, or critical info
- Dismissible (close button, click outside)
- Clear action buttons (confirm/cancel)

### 13. Forms
- Consistent input styles
- Field validation and error messages
- Submit and cancel buttons
- Loading indicator on submit

### 14. Activity Feed/Recent Activity
- Chronological list of user/system actions
- Timestamps for each entry
- Link to related items

### 15. Admin Panel
- User management (list, edit, deactivate)
- Role/permission assignment
- System settings overview

### 16. Help/Support/FAQ
- Searchable FAQ section
- Contact support form or chat
- Links to documentation/resources

### 17. Footer
- Links to terms, privacy, support
- Copyright notice
- Social media icons (optional)

### 18. Error/Empty States
- Friendly messages for no data, errors, or 404s
- Suggestions for next steps
- Illustrations/icons for clarity

### 19. Loading Indicators/Skeletons
- Spinners or skeleton screens for loading content
- Minimize perceived wait times

---

## Templates

Reusable ASCII layout templates are stored in `templates/`. Each file contains the ASCII diagram for one component, ready to be composed into full wireframe flows. To add a new template, create a new `.md` file in `templates/` following the same format.

**Available templates:**

| File | Component |
|------|-----------|
| `templates/home-landing.md` | Home / Landing Page |
| `templates/login.md` | Login Page |
| `templates/registration.md` | Registration / Sign Up Page |
| `templates/email-verification.md` | Email Verification |
| `templates/dashboard.md` | Dashboard |
| `templates/list-table.md` | List / Table View |
| `templates/detail-page.md` | Detail Page |
| `templates/profile.md` | Profile / Player |
| `templates/team-management.md` | Team Management |
| `templates/admin-panel.md` | Admin Panel |
| `templates/notifications.md` | Notifications / Alerts |
| `templates/modals.md` | Modals / Dialogs |
| `templates/forms.md` | Forms |
| `templates/activity-feed.md` | Activity Feed |
| `templates/help-support.md` | Help / Support / FAQ |
| `templates/error-empty-state.md` | Error / Empty State |
| `templates/loading-indicator.md` | Loading Indicator |
| `templates/multi-page-workflow.md` | Multi-Page Workflow |

---

## Examples

See `examples/` for complete lo-fi wireframe outputs generated using this skill:

| File | Description |
|------|-------------|
| `examples/saas-general-lofi.txt` | General SaaS app — home, dashboard, login, table, settings, admin |
| `examples/user-registration-lofi.txt` | New user registration flow with email verification and profile completion |
| `examples/post-registration-dashboard-lofi.txt` | Post-registration team dashboard |
| `examples/team-create-lofi.txt` | Create new team flow |
| `examples/team-join-lofi.txt` | Request to join a team flow |
| `examples/invoice-processing-lofi.txt` | Invoice processing workflow (multi-role) |
