# PMP Exam Simulator

A static, front-end PMP practice simulator (Full Exams, Mini Exams, Quizzes) with a
timer, per-question tracking, section breaks, scoring, and answer review.
Hosted on GitHub Pages — no server, no database.

**Live site:** https://montassarsallami122-spec.github.io/

## Managing student access

Accounts live in **`data/users.json`**. Each entry is a student login (the `u`
field is the student's **email**):

```json
{"u":"student@example.com","h":"<sha256 hash of the password>","name":"Display Name"}
```

Passwords are **hashed** (SHA-256), so the file never stores the real password.

### To add a client
1. Open **`admin.html`** in a browser (locally, or the deployed `/admin.html`).
2. Type a display name, email, and password → click **Generate**.
3. Copy the generated line and paste it into `data/users.json` (comma-separated inside the `[ ]`).
4. `git push` — the account is live in ~1 minute.
5. Give the client their **email + password** and the site link.

### To remove access
Delete that student's line from `data/users.json` and push.

### To reset a password
Generate a new line for the same email and replace the old one.

## How progress works
Each student's attempts and best scores are saved in **their own browser**
(localStorage, namespaced per email). It is private to their device and is
**not** synced across devices, and the admin does not see it centrally.

## ⚠️ Important note on security
This is an **access gate**, not hard security. Because the site is fully static:
- The question files and `users.json` are technically downloadable by anyone.
- The login keeps casual users out of the app UI, but does not truly protect the content.

If real security (protected content, central progress tracking, admin dashboard) is
needed later, that requires a small backend (e.g. Firebase).
