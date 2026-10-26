# DSA Tracker

A responsive, browser-based DSA practice tracker that combines **NeetCode 150** and **Striver Master DSA Patterns** into one checklist. Track solved questions, revision stars, notes, progress, and daily streaks.

## Features

- **269 unique questions** organized into topic groups.
- **Combined roadmap:** NeetCode (`N`), Striver (`S`), and shared questions (`B`).
- **Progress dashboard:** completion percentage, completed/remaining questions, topics completed, questions solved today, and day streak.
- **Search and filters:** search question names; filter by roadmap, completion status, starred questions, and difficulty.
- **Topic controls:** expand or collapse topic groups; topic progress bars.
- **Practice links:** LeetCode links where available, plus YouTube solution searches. Some Striver-only questions link to a web search for TakeUForward practice.
- **Revision workflow:** star questions to revisit and save personal notes with approach, mistakes, or complexity.
- **AI helper:** request a hint or note review for a question through the configured Supabase Edge Function.
- **Local persistence:** progress, timestamps, stars, notes, name, and theme are saved in browser local storage.
- **Optional cloud sync:** register/login with Supabase Auth to sync progress across sessions/devices.
- **Backup and restore:** export tracker data as JSON text, copy it, and restore from a saved backup.
- **Theme support:** switch between light and dark themes; follows system dark mode by default.
- **Responsive layout:** adapts to desktop and mobile screens.

## Tech Stack

- HTML5
- CSS3 (custom properties, responsive layout, light/dark themes)
- Vanilla JavaScript
- [Supabase JavaScript client](https://supabase.com/docs/reference/javascript) v2 (loaded from jsDelivr)
- Supabase Auth, database table, and Edge Function for optional cloud features

## Getting Started
Visit : https://dsa-tracker-weld.vercel.app/#

> The tracker can be used locally without signing in. Cloud sync and the AI helper require the corresponding Supabase setup.

## Usage

1. **Choose a question** from a topic section.
2. Mark it complete using its checkbox. The tracker records the completion timestamp.
3. Use the **☆** control to star a question for revision.
4. Open **📝** to add or edit notes. Notes are saved automatically.
5. Search or filter questions using the controls above the topic list.
6. Use **Expand all** to open topic groups.
7. Open **Backup / Restore** to copy a JSON backup or restore one previously saved.
8. Use **Theme** to switch appearance.
9. Select **Sign in to sync** to register/login and sync through Supabase.

## Roadmap Categories

The tracker includes the following topic groups:

- Arrays & hashing
- Two pointers
- Sliding window
- Stacks & queues
- Binary search
- Linked lists
- Binary trees & BSTs
- Heaps & priority queues
- Recursion & backtracking
- Tries
- Graphs: traversal & connectivity
- Graphs: paths & spanning trees
- Dynamic programming
- Greedy & intervals
- Math & geometry
- Bit manipulation
- String matching

Question source labels:
- `N` — NeetCode
- `S` — Striver
- `B` — included in both lists

Difficulty labels are shown where assigned in the tracker. A small set of Striver practice items do not have a direct LeetCode slug and use a search link instead.

## Local Data and Cloud Sync

### Local storage

The app stores tracker state in browser `localStorage`, including:

- Completed question IDs and completion timestamps
- Starred question IDs
- Notes
- Display name
- Theme preference

Local data stays in the browser profile. Clearing browser storage or using a different browser/profile may remove or make that local progress unavailable. Use Backup / Restore to keep a portable copy.

### Supabase cloud features

The application includes a Supabase project configuration and uses the Supabase JavaScript client. Cloud sync relies on:

- Supabase Auth for registration, login, logout, and password recovery
- A `progress` table to store each user's tracker snapshot
- An `admins` table for the optional admin/member view
- An `ai-helper` Edge Function for question hints and note reviews

The client expects a `progress` table with a user identifier, email, JSON progress data, and update timestamp. Configure suitable **Row Level Security (RLS)** policies so users can read/write only their own progress. The admin view additionally expects authorized user IDs in the `admins` table.

The AI helper is called at:
`/functions/v1/ai-helper`

It receives a question, mode (`hint` or `review`), and the user's note. Deploy and configure the function separately, including any required AI provider credentials and authorization checks.

### Security note

The Supabase URL and publishable/anon key are client-side configuration and are intended for browser use **only when database RLS and Edge Function authorization are correctly configured**. Never place a Supabase service-role key, private API key, or provider secret in this HTML file. Keep AI provider credentials in Edge Function secrets. Review the project's policies before making the app public.

## Project Structure

```text
.
└── index.html     # HTML, styles, question data, and client-side application logic
```

The current implementation is self-contained in one HTML file. Supabase's JavaScript client is loaded from a CDN at runtime.

## Limitations / Notes

- Cloud sync is optional; local tracking works without an account.
- Cloud sync requires a correctly configured Supabase project, schema, Auth settings, and RLS policies.
- AI hint/review actions require a deployed and configured `ai-helper` Edge Function.
- The app's admin/member panel is available only to users recognized by the configured `admins` table.
- Practice destinations depend on the question's mapping; some items use search links rather than a direct problem page.
- No automated tests or package/build configuration are included in this single-file version.

## License

No license is specified in the supplied application. Add a `LICENSE` file before distributing or reusing the project if you want to define its usage terms.

---

# 👨‍💻 Author

Ayub Adil