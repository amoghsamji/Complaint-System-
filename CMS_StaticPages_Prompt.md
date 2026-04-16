# 🎓 KLE Tech CMS — Static Web Pages Master Prompt

> **Project:** Complaint Management System (CMS) for KLE Technological University, Hubbali  
> **Course:** Web Technologies & Software Engineering — SE Review 1  
> **Team:** Dron G Kambali, Pramod S Indi, Chinmay B Sabarad, Amogh Samji, Bheemanguda  
> **Purpose:** Generate all static HTML/CSS/JS pages showing how the final product will look

---

## 🧠 Project Context (Antigravity Overview)

Build a **multi-role Complaint Management System** for KLE Technological University. The system digitizes the currently manual, paper-based grievance process. It has four roles — **Student, Faculty, Admin, and HOD** — each with a distinct portal. The system tracks complaints from submission → assignment → resolution, with urgency levels, worker assignment, and notifications.

### Core Problem Being Solved
KLE Tech currently handles complaints verbally or via paper forms — no tracking, no accountability, complaints get lost. This CMS brings transparency, speed, and digital traceability.

---

## 🎨 Design System (Apply to ALL Pages)

### Theme
- **Color Palette:** Deep navy `#0A1628` as dominant, electric blue `#2563EB` as primary action, amber `#F59E0B` as urgency/accent, clean white `#F8FAFC` for surfaces
- **Font Pairing:** `Outfit` (headings, bold, modern) + `DM Sans` (body text, readable)
- **Iconography:** Use Unicode symbols + emoji throughout for quick scanning — no need for an icon library
- **Border Radius:** 12px for cards, 8px for buttons/inputs
- **Shadows:** Soft layered shadows `box-shadow: 0 4px 24px rgba(0,0,0,0.08)`

### 🌙 Dark / Light Theme Toggle
- Place a **☀️ / 🌙 toggle button** in the top-right corner of every page's navbar
- Use CSS variables so the entire page switches:
  ```css
  :root { --bg: #F8FAFC; --surface: #FFFFFF; --text: #0A1628; --muted: #64748B; }
  [data-theme="dark"] { --bg: #0A1628; --surface: #1E293B; --text: #F8FAFC; --muted: #94A3B8; }
  ```
- A small JS snippet toggles `data-theme="dark"` on `<html>` and saves to `localStorage`

### Status Badge Colors (consistent across all pages)
| Status | Symbol | Color |
|--------|--------|-------|
| 🔴 Pending | ⏳ | Red `#EF4444` |
| 🟡 In Progress | 🔧 | Amber `#F59E0B` |
| 🟢 Resolved | ✅ | Green `#22C55E` |
| ⚪ Escalated | 🚨 | Purple `#8B5CF6` |

### Urgency Level Colors
| Level | Symbol | Color |
|-------|--------|-------|
| 🔴 High | 🔥 | Red `#EF4444` |
| 🟡 Medium | ⚡ | Amber `#F59E0B` |
| 🟢 Low | 📋 | Green `#22C55E` |

---

## 📄 PAGE LIST — Build Each as a Separate HTML File

---

### PAGE 1: `login.html` — Login Page (Shared Entry Point)

**Route:** `cms.kletech.ac.in/login`

**Layout:**
- Split screen: left side = KLE branding panel (navy bg, university logo area, tagline "Grievance. Tracked. Resolved."), right side = login form on white card
- University name: **KLE Technological University** with subtitle **Complaint Management System**

**Elements:**
- 📧 Email field (placeholder: `yourname@kletech.ac.in`)
- 🔑 Password field with show/hide 👁️ toggle
- Role auto-detected from email domain OR show role display badge (read-only) after email entry
- `Login →` primary button (full width, electric blue)
- `Forgot Password?` link below
- **❌ NO "Register / Sign Up" button** — Students and Faculty cannot self-register. Only Admin can create accounts.
- Small notice at bottom: *"New user? Contact your department admin to get access."*
- ☀️/🌙 toggle in top-right corner

---

### PAGE 2: `student-home.html` — Student Dashboard / Home

**Route:** `cms.kletech.ac.in/student/home`

**Navbar:** Logo | 🏠 Home | 📝 New Complaint | 📋 My Complaints | 👤 Profile | ☀️/🌙 | Logout

**Hero Section:**
- Welcome banner: "Welcome back, [Student Name] 👋"
- University: KLE Technological University
- Department badge + USN display

**Stats Row (4 cards with icons):**
- 📋 Total Complaints: `[N]`
- ⏳ Pending: `[N]`
- 🔧 In Progress: `[N]`
- ✅ Resolved: `[N]`

**How It Works Section (3 steps with icons):**
1. 📝 Submit your complaint with category + urgency
2. 🔧 Admin assigns it to a worker
3. ✅ You get notified when resolved

**Recent Complaints Table (last 3–5):**
- Columns: Complaint ID | Category | 🔥 Urgency | ⏳ Status | Date | Action (View →)
- Clicking any row → goes to `complaint-status.html`

**Quick Action Button:** Big CTA — `+ File a New Complaint`

---

### PAGE 3: `student-complaint-form.html` — Submit Complaint Form

**Route:** `cms.kletech.ac.in/student/new-complaint`

**Page Title:** 📝 Submit a New Complaint

**Form Fields:**
1. **Category** (dropdown with icons):
   - 🏫 Academic
   - 🍽️ Canteen
   - 🏠 Hostel
   - 🚿 Sanitation
   - 🔌 Electrical / Infrastructure
   - 🌐 Internet / Network
   - 📚 Library
   - 🚌 Transport
   - 🔒 Safety & Security
   - 📦 Other

2. **Urgency Level** (radio buttons or segmented control with color coding):
   - 🔴 High — *Needs immediate attention*
   - 🟡 Medium — *Should be resolved within 3 days*
   - 🟢 Low — *General feedback / non-urgent*

3. **Subject** — short text input (max 100 chars)

4. **Description** — textarea (placeholder: "Describe your complaint in detail. Include location, date, and specifics.")

5. **Upload Photo** 📷 — optional file upload with drag-and-drop zone

6. **Anonymous Submission** — checkbox 👤 *"Submit anonymously (your identity will be hidden from workers)"*

**Submit Button:** `Submit Complaint →` (electric blue, full width)

**Note below form:** *"You will receive an email notification at your KLE Tech email when status changes."*

---

### PAGE 4: `student-complaints-list.html` — My Complaints List

**Route:** `cms.kletech.ac.in/student/complaints`

**Page Title:** 📋 My Complaints

**Filter Bar:**
- Filter by Status: All | ⏳ Pending | 🔧 In Progress | ✅ Resolved
- Filter by Urgency: All | 🔴 High | 🟡 Medium | 🟢 Low
- Search bar 🔍

**Complaints Table / Card List:**
Each complaint row/card shows:
- Complaint ID (e.g., `CMS-2025-0042`)
- Category icon + name
- Subject (truncated)
- 🔥 Urgency badge
- ⏳ Status badge (color coded)
- Date submitted
- `View Details →` button

**Clicking any complaint → navigates to `complaint-status.html?id=CMS-2025-0042`**

---

### PAGE 5: `complaint-status.html` — Complaint Status / Detail Page

**Route:** `cms.kletech.ac.in/student/complaint-status`

**Page Title:** Complaint #CMS-2025-0042

**Layout: Two column**

**Left — Complaint Details Card:**
- Complaint ID, Date, Category
- 🔥 Urgency badge
- Full description
- Uploaded photo (if any)

**Right — Status Tracker (vertical stepper):**
```
✅ Submitted         — 12 Apr 2025, 10:30 AM
✅ Under Review      — 12 Apr 2025, 2:00 PM
🔧 Assigned to Worker — 13 Apr 2025, 9:00 AM
⏳ Resolution Pending
⬜ Resolved
```
Each step has a timestamp and description.

**Bottom — Timeline / Activity Log:**
- Chronological notes from admin/worker updates

**Back Button:** `← Back to My Complaints`

---

### PAGE 6: `faculty-home.html` — Faculty Dashboard / Home

**Route:** `cms.kletech.ac.in/faculty/home`

**Navbar:** Logo | 🏠 Home | 📝 New Complaint | 📋 My Complaints | ☀️/🌙 | Logout

**Identical structure to Student Home** but with:
- Role badge: `👨‍🏫 Faculty`
- Department shown (e.g., CSE / ECE)
- Same 4 stat cards
- Same recent complaints table
- Same quick action CTA

*(Faculty uses the exact same Complaint Form and Complaints List / Status pages as Student — same files)*

---

### PAGE 7: `admin-home.html` — Admin Dashboard / Home

**Route:** `cms.kletech.ac.in/admin/home`

**Navbar:** Logo | 🏠 Home | ⏳ Pending | 📁 History | ➕ Manage Users | ☀️/🌙 | Logout

**Welcome Banner:** "Admin Dashboard — KLE Tech CMS 🛠️"

**Stats Row (5 cards):**
- 📋 Total Complaints
- ⏳ Pending
- 🔧 In Progress
- ✅ Resolved This Month
- 👥 Total Users

**Urgency Breakdown Section:**
- Mini bar chart or colored count boxes:
  - 🔴 High Priority: [N]
  - 🟡 Medium Priority: [N]
  - 🟢 Low Priority: [N]

**Recent Activity Feed (right sidebar or bottom):**
- "CMS-2025-0042 assigned to Ramesh K — 2 hrs ago"
- "CMS-2025-0039 resolved ✅ — 5 hrs ago"
- "New complaint filed 🔴 High — 1 hr ago"

**Quick Links:**
- `⏳ View Pending Complaints`
- `📁 View Resolved History`
- `➕ Create New User`

---

### PAGE 8: `admin-pending.html` — Admin Pending Complaints

**Route:** `cms.kletech.ac.in/admin/pending`

**Page Title:** ⏳ Pending Complaints

**Filter Bar:**
- Filter by Urgency: All | 🔴 High | 🟡 Medium | 🟢 Low
- Filter by Category, Department, Date Range
- Search 🔍

**Complaints Table:**
Columns: ID | Submitter | Category | 🔥 Urgency | Department | Date | Status | `Assign →`

**Clicking `Assign →` on any complaint → opens `admin-assign.html` (worker assignment modal or page)**

---

### PAGE 9: `admin-assign.html` — Admin: Assign Complaint to Worker

**Route:** `cms.kletech.ac.in/admin/assign?id=CMS-2025-0042`

**Page Title:** 🔧 Assign Complaint — #CMS-2025-0042

**Left Panel — Complaint Summary:**
- ID, Category, Urgency badge, Description (read-only)

**Right Panel — Assign Worker:**
**Worker List Table:**
| 👷 Worker Name | Department | 📞 Phone | Active Tasks | Action |
|---------------|-----------|---------|-------------|--------|
| Ramesh Kumar  | Electrical| 98765XXXXX | 2 | `Assign` |
| Suresh Patil  | Plumbing  | 97654XXXXX | 0 | `Assign` |
| Anand Hegde   | Canteen   | 96543XXXXX | 1 | `Assign` |

**After selecting a worker:**
- Button: `📞 Call Worker` — shows phone number in a styled callout
- Button: `📲 Send Notification` — shows a confirmation dialog: *"Notification will be sent to Ramesh Kumar's registered mobile number and email."*
- Button: `✅ Confirm Assignment`

**Note:** No actual backend call — this is a static mockup showing how the UI looks.

---

### PAGE 10: `admin-history.html` — Admin Resolved Complaints History

**Route:** `cms.kletech.ac.in/admin/history`

**Page Title:** 📁 Resolved Complaints — History

**Filter Bar:** Date range picker | Category | Worker | Search

**Table:**
Columns: ID | Category | Urgency | Submitted By (role) | Assigned Worker | Resolved Date | Resolution Notes | `View →`

Table rows styled with subtle green tint for resolved items.

---

### PAGE 11: `admin-manage-users.html` — Admin: Manage Users / Create Account

**Route:** `cms.kletech.ac.in/admin/manage-users`

**Page Title:** 👥 Manage Users

**Tab Navigation:**
- 👨‍🎓 Students | 👨‍🏫 Faculty | 👷 Workers

**User List Table (per tab):**
Columns: Name | USN/ID | Email | Department | Role | Status (Active/Inactive) | Actions (Edit ✏️ | Deactivate 🚫)

**➕ Create New User Button (top right)** → opens a form/modal:

**Create Account Form:**
- Full Name
- Email (`@kletech.ac.in`)
- Role dropdown: Student / Faculty / Worker
- Department
- USN / Staff ID
- Temporary Password (auto-generated or manual)
- `Create Account` button

**Note shown on page:** *"Students and Faculty cannot self-register. Only admins can create and manage user accounts."*

---

### PAGE 12: `hod-home.html` — HOD Dashboard / Home

**Route:** `cms.kletech.ac.in/hod/home`

**Navbar:** Logo | 🏠 Home | 🚨 Escalated Complaints | ☀️/🌙 | Logout

**Welcome Banner:** "HOD Dashboard — [Department Name] 🎓"

**Stats Row (4 cards):**
- 📋 Total in Department
- 🚨 Escalated to HOD
- 🔧 In Progress
- ✅ Resolved This Month

**Department Health Section:**
- Show average resolution time for the department
- Show overdue complaints count (>5 working days unresolved)

**Recent Escalations Feed:**
- "CMS-2025-0040 — escalated 3 days ago 🚨"
- "CMS-2025-0035 — escalated 1 day ago 🚨"

---

### PAGE 13: `hod-pending.html` — HOD Escalated / Pending Complaints

**Route:** `cms.kletech.ac.in/hod/pending`

**Page Title:** 🚨 Escalated & Pending Complaints

**Complaints Table:**
Columns: ID | Category | Urgency | Days Pending | Status | `Contact Admin →`

**Clicking `Contact Admin →` on any complaint → opens `hod-admin-contact.html`**

---

### PAGE 14: `hod-admin-contact.html` — HOD: View Admin Contact for a Complaint

**Route:** `cms.kletech.ac.in/hod/admin-contact?id=CMS-2025-0040`

**Page Title:** 📞 Admin Contact — Complaint #CMS-2025-0040

**Complaint Summary (top):**
- ID, Category, Urgency badge, Days Pending

**Responsible Admin Card:**
```
┌────────────────────────────────────┐
│ 👤 Admin Name: Kavitha M           │
│ 📧 Email: kavitha@kletech.ac.in    │
│ 📞 Phone: 98XXX XXXXX              │
│ 🏢 Department: Infrastructure       │
│                                    │
│  [📞 Call Admin]  [📧 Email Admin] │
└────────────────────────────────────┘
```

*(Mirrors how admin sees worker contact — same UX pattern)*

---

## ⚙️ JS Theme Toggle Snippet (Include in Every Page)

```html
<!-- Place in <head> to prevent flash -->
<script>
  const saved = localStorage.getItem('theme') || 'light';
  document.documentElement.setAttribute('data-theme', saved);
</script>

<!-- Toggle button in navbar -->
<button id="themeToggle" onclick="toggleTheme()" title="Toggle theme">☀️</button>

<script>
  function toggleTheme() {
    const html = document.documentElement;
    const current = html.getAttribute('data-theme');
    const next = current === 'dark' ? 'light' : 'dark';
    html.setAttribute('data-theme', next);
    localStorage.setItem('theme', next);
    document.getElementById('themeToggle').textContent = next === 'dark' ? '☀️' : '🌙';
  }
  // Set correct icon on load
  document.getElementById('themeToggle').textContent = 
    document.documentElement.getAttribute('data-theme') === 'dark' ? '☀️' : '🌙';
</script>
```

---

## 🗂️ File Structure Summary

```
cms-static/
├── login.html                    ← Shared login (no register option)
├── student/
│   ├── student-home.html         ← Dashboard with stats
│   ├── student-complaint-form.html ← Submit complaint (with urgency)
│   ├── student-complaints-list.html ← All my complaints
│   └── complaint-status.html     ← Status tracker / detail view
├── faculty/
│   ├── faculty-home.html         ← Same structure as student
│   └── (shares complaint-form, list, status pages)
├── admin/
│   ├── admin-home.html           ← Full dashboard
│   ├── admin-pending.html        ← Pending complaints table
│   ├── admin-assign.html         ← Assign to worker + call/notify
│   ├── admin-history.html        ← Resolved history
│   └── admin-manage-users.html   ← Create accounts (students/faculty/workers)
└── hod/
    ├── hod-home.html             ← Department overview
    ├── hod-pending.html          ← Escalated complaints + admin contact button
    └── hod-admin-contact.html    ← Admin contact card (phone/email)
```

---

## ✅ Review Checklist — Verify Every Page Has

- [ ] ☀️/🌙 theme toggle button in navbar
- [ ] Correct navbar links for that role (no cross-role links)
- [ ] Role badge visible (Student / Faculty / Admin / HOD)
- [ ] Status badges with correct color coding and symbols
- [ ] Urgency badges with 🔴/🟡/🟢 color coding
- [ ] NO register/sign-up button on login page
- [ ] Complaint form includes Urgency field
- [ ] Admin assign page shows worker phone + call/notify buttons
- [ ] HOD pending page shows "Contact Admin" with admin's phone
- [ ] Admin manage-users page has "Create Account" form
- [ ] All navigation links point to correct file names
- [ ] Consistent typography: `Outfit` for headings, `DM Sans` for body
- [ ] All complaint ID format: `CMS-YYYY-XXXX`

---

## 🎯 Tone & Aesthetic Direction

- **Professional but approachable** — this is a university system, not a startup
- **Trust signals everywhere** — show KLE Tech branding, use institutional language
- **Clarity over cleverness** — students and faculty must understand at a glance
- **Symbols reduce cognitive load** — use emoji/Unicode icons consistently
- **Responsive** — works on mobile (students will use phones)
- **Accessible** — sufficient contrast, clear labels, logical tab order

---

*Prompt prepared for SE Review 1 — KLE Tech CMS Project, April 2025*
*Team: Dron G Kambali · Pramod S Indi · Chinmay B Sabarad · Amogh Samji · Bheemanguda*
