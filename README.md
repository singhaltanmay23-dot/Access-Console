# Access Console

Access Console is a lightweight, single-file web application built with vanilla web technologies for client-side user registration, security hashing demonstration, and record management. It features an interactive cyber-themed interface, live cryptographic feedback, and a structured dashboard for inspecting registered credentials.

---

## How to Run the Project

Because the entire application is bundled into a single file with no external dependencies or build tools, getting started is straightforward:

1. **Clone or Download the Repository:**
Clone this repository to your local machine or download the `access-console.html` file.

2. **Open the File:**
Double-click `access-console.html` or open it using any modern web browser (Google Chrome, Firefox, Safari, Microsoft Edge, Brave).

3. **Local Storage Note:**
Open the file directly from your local filesystem or host it via a local web server (e.g., `npx serve` or Python's `python -m http.server`) to ensure data persists properly across page refreshes via the browser's `localStorage`.

---

## Features Implemented

1. **User Registration Form:**
* Collects a **Username**, **Email**, and **Password**.
* Enforces field validation, requiring non-empty values, valid email formatting, and a minimum password length of 6 characters.

2. **Client-Side Cryptographic Hashing:**
* Hashes passwords using modern SHA-256 encryption via the browser's native cryptography capabilities.
* Generates a unique, cryptographically random 16-byte salt per user to prevent rainbow table attacks.

3. **Records Dashboard:**
* Presents all stored users in a structured tabular layout.
* Displays user indices, usernames, emails, truncated password hashes, and action controls.

4. **Record Deletion:**
* Users can remove individual records from storage with the click of a button.

5. **Persistent Storage:**
* Automatically serializes and saves users to `localStorage` under the key `access_console_users_v1` so records persist across browser reloads.

---

## Additional Features Added

1. **Live Hash Ticker:**
* Computes and displays a real-time SHA-256 hash as the user types their password into the input field.
* Includes race-condition handling using request counters to ensure rapid typing does not cause outdated hash calculations to render.

2. **Dynamic Password Strength Meter:**
* Analyzes password complexity (length, casing combinations, digits, and special characters) to render a dynamic 4-stage color progress bar (Weak, Medium, Strong).

3. **Interactive Live Form Validation:**
* Debounced real-time validation checks for existing duplicate usernames or email addresses as the user types.
* Animated feedback indicators (checking spinners, checkmarks, error crosses, and helper messages) for each input field.

4. **Record Search & Filter:**
* Instant real-time search across existing records filtering by username or email.
* Includes a keyboard shortcut (`/`) to focus the search input directly when viewing the dashboard.

5. **Table Sorting:**
* Multi-directional sorting (ascending/descending) on the **Username** and **Email** table columns with custom caret indicator transitions.

6. **Toast Notification & Undo Support:**
* Non-blocking toast notification stack for alerts, errors, and confirmations.
* Deleting a record provides an inline **Undo** button in the toast notification to recover mistakenly deleted entries within 5 seconds.

7. **One-Click Hash Copying:**
* Dedicated button next to each hash to copy the full `salt:hash` string directly to the clipboard with animated confirmation feedback.

8. **Password Visibility Toggle:**
* Eye icon toggle to switch between masked password characters and plain text.

---

## Concepts Learned

1. **Web Cryptography API (`window.crypto.subtle`):**
* Gained practical experience generating cryptographically secure pseudo-random values (`crypto.getRandomValues`) and computing digests (`SubtleCrypto.digest`) asynchronously using Promises.

2. **Race Condition Prevention in Asynchronous UI:**
* Handled out-of-order asynchronous hash resolutions by introducing monotonic request IDs to guarantee only the latest keystroke updates the DOM.

3. **Debouncing & Non-Blocking Asynchronous Checks:**
* Implemented debounced timers (`setTimeout` / `clearTimeout`) to prevent costly or jarring validation checks on every keystroke.

4. **State Management without Frameworks:**
* Structured application state (records, sorting direction, search queries, active tab) and mapped it cleanly to declarative DOM rendering without external libraries like React or Vue.

5. **Accessible & Fluid UI Engineering:**
* Utilized CSS grid, flexbox, custom properties (CSS variables), keyframe animations, and media queries (`prefers-reduced-motion`) to craft a polished, accessible design.
