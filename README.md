# Frappe CLI (Employee Check-in Tool)

A lightweight command-line interface for interacting with Frappe / ERPNext employee check-ins.

It allows you to:

* Log in to your Frappe instance
* Perform check-in / check-out actions
* View check-in records
* Calculate worked hours
* Track your current check-in state
* Manage multiple profiles

---

## ✨ Features

* Interactive login (no env vars required)
* Profile system (save and reuse credentials)
* Secure password input (supports special characters like `$`, `!`, etc.)
* Session persistence via cookies
* State-aware actions (prevents duplicate check-ins/outs)
* Colored terminal output (green / red / yellow)
* Clean CLI conventions:

  * `get-*` → read operations
  * `do-*` → actions

---

## 📦 Requirements

* Bash (Linux / macOS / WSL)
* `curl`
* `jq`

Install dependencies:

```bash
# Ubuntu / Debian
sudo apt install curl jq

# macOS (Homebrew)
brew install curl jq
```

---

## 🚀 Installation

### 1. Clone the repository

```bash
git clone https://github.com/omarha96/frappe-cli.git
cd frappe-cli
```

### 2. Make executable

```bash
chmod +x frappe
```

### 3. Move to PATH (optional but recommended)

```bash
mv frappe ~/.local/bin/
```

Or system-wide:

```bash
sudo mv frappe /usr/local/bin/
```

Now you can run:

```bash
frappe
```

---

## 🔐 Authentication

### First time login

```bash
frappe login
```

You will be prompted for:

* Host (e.g. https://your-site.com)
* Username
* Password (hidden input)

Optional:

```text
Save as profile? (y/N)
```

If you save, you can reuse it later.

---

### Using profiles

On next login:

```bash
frappe login
```

You’ll see:

```text
1. work
2. personal
```

Select a profile or press Enter to enter manually.

---

### Logout

```bash
frappe logout
```

---

## 📘 Commands

### 🔹 Get check-in records

```bash
frappe get-checking-records [limit]
```

Example:

```bash
frappe get-checking-records 10
```

---

### 🔹 Get current state

```bash
frappe get-checking-state
```

Output:

* `IN` → currently checked in (green)
* `OUT` → currently checked out (red)
* `UNKNOWN` → no records

---

### 🔹 Perform check-in

```bash
frappe do-checkin
```

* Prevents duplicate check-ins
* Shows warning if already checked in

---

### 🔹 Perform check-out

```bash
frappe do-checkout
```

* Prevents duplicate check-outs
* Warns if no prior check-in

---

### 🔹 Calculate worked hours

```bash
frappe get-hours [limit]
```

Outputs each date total duration based on check-in/out pairs, and takes optional "limit".

---

## 🎨 Output Colors

* 🟢 Green → success / active state
* 🔴 Red → errors / checked out
* 🟡 Yellow → warnings / edge cases

---

## ⚠️ Notes

### Password Storage

If you choose to save a profile, credentials are stored in:

```bash
~/.frappe/profiles
```

⚠️ Stored in plain text.

For sensitive environments, consider:

* Not saving profiles
* Restricting file permissions:

  ```bash
  chmod 600 ~/.frappe/profiles
  ```

---

### Session Storage

Session cookies are stored in:

```bash
~/.frappe/cookies.txt
```

---

### API Compatibility

This CLI assumes standard ERPNext endpoint:

```text
employee_checkin.add_log_based_on_employee_field
```

If your backend differs, adjustments may be required.

---

## 🛠 Troubleshooting

### Not logged in

```text
ERROR: Not logged in. Run: frappe login
```

Fix:

```bash
frappe login
```

---

### jq not found

```bash
sudo apt install jq
# or
brew install jq
```

---

### Permission denied

```bash
chmod +x frappe
```

---

## 📌 Example Workflow

```bash
frappe login

frappe get-checking-state
frappe do-checkin

# ... work ...

frappe do-checkout

frappe get-hours
```

---

## 📄 License

MIT License (or your preferred license)

---

## 🤝 Contributing

Feel free to open issues or submit pull requests to improve the CLI.

---

## 🚀 Future Improvements

* Encrypted profile storage
* Daily summaries
* Notifications / reminders
* Interactive mode

---
