# LocateLib

A library catalogue and shelf locator for **Sarala Birla University, Ranchi**.
Students search for a book and see exactly which rack, shelf and slot it sits on, and whether it is in right now. Library staff log in to issue and return books, track due dates and calculate fines.

> Live site:

## Why this project

Finding a book in a large library usually means asking the librarian or walking every rack. LocateLib puts the catalogue online and shows each book's physical position on a shelf map, so a student can walk straight to it.

## Features

**For students (no login)**
- Search by title, author, book ID, DDC call number or shelf code
- Filter by subject and availability, and sort by ID, title, shelf or DDC
- Shelf map of three racks with colour-coded book spines. Selecting a book shows its rack, shelf and slot
- See whether a book is on the shelf or issued, and when it is due back
- Library assistant that answers questions such as "Where is Python Crash Course?" or "Show free slots"
- Light and dark mode, a print-friendly catalogue, and a layout that works on phones

**For library staff (login required)**
- Issue and return books, with a due date 14 days after issue
- Overdue tracking with a fine of ₹2 per day
- Limit of 3 books per student, enforced in the database
- Add, edit and delete books, with a check that no two books share a shelf slot
- Circulation ledger with active, overdue and returned records
- Export the catalogue to CSV
- Live updates: a change made at the desk appears in every open browser without a refresh

## Tech stack

| Part | Technology |
| -- | --  |
| Front end | HTML, CSS and vanilla JavaScript in a single file (`index.html`) |
| Database and login | [Supabase](https://supabase.com) (PostgreSQL, Auth, Realtime) |
| Hosting | Vercel |

## Project structure

```
.
├── index.html       # the whole front end
├── supabase-setup.sql   # tables, security rules, functions and starter books
└── README.md
```

## Getting started

### 1. Create a Supabase project
Create a free project at [supabase.com](https://supabase.com).

### 2. Set up the database
Open **SQL Editor**, paste the contents of `supabase-setup.sql` and run it. This creates:
- the `books` and `issues` tables
- a `loan_dates` view, so the public can see due dates without student details
- Row Level Security policies
- the `issue_book` and `return_book` functions
- 10 starter books

### 3. Create a staff account
Go to **Authentication → Users → Add user** and create a login for the librarian. Then turn **off** "Allow new users to sign up" in the Auth settings. Any logged-in user is treated as staff, so only create accounts for real staff.

### 4. Add your project keys
Open `locatelib.html` and fill in the two constants near the top of the last `<script>` block:

```js
const SUPABASE_URL='https://your-project-id.supabase.co';
const SUPABASE_ANON_KEY='your-anon-or-publishable-key';
```

Both values are in **Project Settings → API**.

### 5. Run it
Open `index.html` in a browser. It needs an internet connection to reach Supabase.

If the keys are missing, the page opens in a read-only demo mode with sample data and shows a notice.

## Deploying

Because the site is a single static file, you can host it for free.

## Security

- The page uses only the Supabase **anon (publishable) key**, which is designed to be public. Access is controlled by Row Level Security in the database, not by hiding the key.
- Public visitors can read books and due dates. They cannot see student names or roll numbers, and they cannot change any data.
- Issuing, returning, adding, editing and deleting require a logged-in staff user. The 3-book limit and the unique shelf slot are enforced by the database.
- It bypasses every security rule.
- Do not commit real student data to a public repository.

## How the assistant works

The library assistant does not call an AI service. It uses keyword matching and scoring over the catalogue data, so it works without extra keys or cost. The logic is in the `find()` and `ask()` functions.

## Ideas for the future

- Roles for staff, so a student volunteer can issue books but not delete them
- Reservations and email reminders for overdue books
- Barcode or QR scanning for issue and return
- Support for more than three racks, and a shelf layout editor
- Monthly circulation reports

## Credits

- University name and logo belong to Sarala Birla University and are used here for a college project.
- Built by Anurag Kumar, Btech in CSE (2026-2030).

## License

This project is licensed under the MIT License. You are free to use, copy, modify, and distribute the project code, subject to the terms and conditions of the MIT License.

**Third-Party Assets & Services:**
- The Sarala Birla University name and logo are the property of Sarala Birla University and are used solely for educational and academic project purposes. They are not covered by this project's MIT License.
- Supabase is used as the backend service. Its services are subject to Supabase's own terms and policies.
- Third-party libraries and dependencies remain subject to their respective licenses.

See the `LICENSE` file for the full MIT License.
