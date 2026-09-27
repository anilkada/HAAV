# HAAV — Academic Management System
### Aditya University | C++ OOP Project: Student Record Manager

---

## 🚀 How to Run in VS Code

### Option 1 — Live Server (Recommended)
1. Open VS Code
2. Install the **Live Server** extension by Ritwick Dey (Extensions → search "Live Server")
3. Open the project folder in VS Code
4. Right-click `haav.html` → **"Open with Live Server"**
5. Browser opens automatically at `http://127.0.0.1:5500/haav.html`

### Option 2 — Direct Browser
1. Simply **double-click** `haav.html` in your file explorer
2. It opens directly in your default browser — no server needed
3. All features work offline (data saved in browser localStorage)

### Option 3 — VS Code Simple Browser
1. Open `haav.html` in VS Code
2. Press `Ctrl+Shift+P` → type "Simple Browser" → Enter
3. Type the file path or `http://127.0.0.1:5500/haav.html`

---

## 🔑 Demo Login Credentials

> ⚠️ FICTIONAL DATA ONLY — For demonstration purposes

### Student Demo
| Field | Value |
|-------|-------|
| Roll Number | `25B11AI442` |
| Password | `Student@12345` |
| Name | Anil Kumar |
| Programme | B.Tech (AIML) · II Year · Sem III |

### Faculty Demo
| Field | Value |
|-------|-------|
| Faculty ID | `AU-FAC-001` |
| Password | `Faculty@12345` |
| Name | Dr. Arjun Rao |
| Department | AIML · Associate Professor |

> ℹ️ No public registration. No admin login on the login page.
> All accounts are institution-controlled.

---

## 📁 Project Structure

```
haav-project/
│
├── haav.html          ← Complete application (single file, self-contained)
└── README.md          ← This file
```

The entire system runs from a **single HTML file**:
- No build tools required
- No npm install required
- No backend server required
- Works in any modern browser
- All data persisted to browser localStorage

---

## 🏗️ Architecture

```
haav.html
├── CSS (embedded)
│   ├── Layout: Sidebar + Main Content
│   ├── Components: Cards, Badges, Buttons, Tables, Forms
│   ├── Modals, Toasts, Timetable Grid
│   └── Responsive (mobile/tablet/desktop)
│
├── External CDN (loaded from internet)
│   ├── Tailwind CSS (cdn.tailwindcss.com)
│   └── Chart.js 4.4.1 (cdnjs.cloudflare.com)
│
└── JavaScript (embedded)
    ├── SEED DATA
    │   ├── 30 fictional students (25B11AI401–25B11AI444)
    │   ├── 8 fictional faculty (AU-FAC-001 to AU-FAC-008)
    │   ├── 16 subjects (Sem 1–3)
    │   ├── Attendance records
    │   ├── Marks / grades
    │   ├── Timetable (Mon–Sat)
    │   ├── 10 announcements
    │   ├── 9 examinations
    │   ├── Fee structures
    │   ├── Backlogs
    │   └── Academic history (Sem 1 & 2)
    │
    ├── DB MODULE (localStorage abstraction)
    │   ├── Auto-seeds on first load
    │   └── Persists all changes
    │
    ├── AUTH MODULE
    │   ├── Role detection from ID format
    │   ├── Session persistence
    │   └── Logout
    │
    ├── STUDENT PAGES (13)
    │   Dashboard · Profile · Attendance · Performance
    │   Examinations · Timetable · Fees · Registration
    │   Backlogs · Academic History · Announcements
    │   Notifications · Settings
    │
    └── FACULTY PAGES (8)
        Dashboard · My Classes · Students
        Mark Attendance · Marks Entry · Examinations
        Timetable · Announcements · Profile
```

---

## 🔐 Authentication Logic

```
Login ID entered
    │
    ├── Starts with digit?  (e.g. 25B11AI442)
    │       └── → STUDENT role
    │
    └── Starts with AU-FAC-? (e.g. AU-FAC-001)
            └── → FACULTY role

No public registration.
No admin login on login screen.
```

---

## 📊 Attendance Shortage Algorithm (C++ OOP Core)

```cpp
// C++ Implementation (Student Record Manager)
int requiredClassesToReachTarget(int attended, int conducted, float target = 75.0) {
    float current = (float)attended / conducted * 100;
    if (current >= target) return 0;
    // Solve: (attended + X) / (conducted + X) >= target/100
    // X >= (target/100 * conducted - attended) / (1 - target/100)
    return ceil((target/100.0 * conducted - attended) / (1 - target/100.0));
}

// JavaScript equivalent in HAAV:
const att_need = (a, c, t=75) => {
    if (att_pct(a,c) >= t) return 0;
    return Math.max(0, Math.ceil((t/100*c - a) / (1 - t/100)));
};

// Example (demo student — DBMS):
// attended=22, conducted=30, target=75%
// X = ceil((0.75*30 - 22) / (1-0.75)) = ceil(0.5/0.25) = ceil(2) = 2 classes
```

---

## 💡 Sample Data Overview

| Category | Count |
|----------|-------|
| Students | 30 (Roll: 25B11AI401–25B11AI444) |
| Faculty | 8 (AU-FAC-001 to AU-FAC-008) |
| Departments | 3 (AIML, CSE, ECE) |
| Subjects | 16 (across Sems 1–3) |
| Announcements | 10 |
| Examinations | 9 |

### Student Profiles (Demo Variety)

| Roll | Name | Profile |
|------|------|---------|
| 25B11AI442 | Anil Kumar | Demo · DBMS shortage · 1 backlog · fees pending |
| 25B11AI401 | Ravi Kiran Reddy | High achiever · 9.1 CGPA · full attendance |
| 25B11AI403 | Divya Nair | Good marks · low attendance in DBMS |
| 25B11AI409 | Rohit Verma | Multiple attendance shortages · 2 backlogs |
| 25B11AI404 | Sai Teja Varma | Good academic · fees pending |

---

## 🎨 UI Design

| Element | Specification |
|---------|--------------|
| Background | White / Light Grey (#f8fafc) |
| Primary Accent | Indigo (#4f46e5) |
| Sidebar | Dark Slate (#1e293b) |
| Success | Green (#16a34a) |
| Warning | Amber (#d97706) |
| Critical | Red (#dc2626) |
| Typography | System font stack (-apple-system) |

---

## ⚙️ Requirements

- Modern browser: Chrome, Firefox, Edge, Safari
- Internet connection (for Tailwind CSS + Chart.js CDN on first load)
- VS Code + Live Server (for hot reload during development)

---

## 📝 Notes

- All data resets on "Clear localStorage" (browser dev tools)
- To reset seed data: open browser console → `localStorage.clear()` → refresh
- Charts require Chart.js CDN to be loaded (needs internet)
- This is a demonstration system with fictional data only

---

*HAAV · Academic Management System · Aditya University · 2026-27*
*C++ OOP Project: Student Record Manager*
