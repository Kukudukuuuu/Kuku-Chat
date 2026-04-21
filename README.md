# Kuku Chat

A terminal-based social messaging application with user authentication, private messages, and group chats. Built with Python and MongoDB.

---

## Features

- User registration and login with password hashing (SHA-256)
- Private messaging
- Group chats with public and private types
- Group admin roles and member management
- Color-coded terminal output
- Full message history sorted by timestamp

---

## Requirements

- Python 3.8+
- MongoDB (local or Atlas)

### Python dependencies

```
pymongo
termcolor
```

Install with:

```bash
pip install pymongo termcolor
```

---

## Setup

**1. Clone or download the project.**

**2. Configure your MongoDB connection.**

Open `main.py` and replace the empty string in the MongoClient line with your connection URI:

```python
cluster = MongoClient("your-mongodb-uri-here")
```

For a local MongoDB instance:

```
mongodb://localhost:27017
```

For MongoDB Atlas, use the connection string from your Atlas dashboard.

**3. Run the application.**

```bash
python main.py
```

---

## MongoDB Collections

The app uses three collections inside a database named `socialmedia`:

| Collection | Purpose |
|---|---|
| `users` | Stores registered user accounts |
| `bandar` | Stores all messages (private and group) |
| `groups` | Stores group chat metadata and membership |

---

## Usage

On launch you will be prompted to log in or register. After authenticating, the main menu gives you the following options.

### Main menu

| Option | Description |
|---|---|
| View all messages | Shows all private messages and group messages from groups you belong to |
| View my messages | Shows only messages you have sent |
| Send private message | Post a message visible to all users |
| Group chats | Opens the group management submenu |
| Logout | Returns to the authentication screen |
| Exit | Closes the application |

### Group management

| Option | Description |
|---|---|
| Create new group | Create a public or private group |
| List groups | View your groups and available public groups |
| Join group | Join any public group |
| Leave group | Leave a group you are a member of |
| Send group message | Post a message to a specific group |
| View group messages | Read all messages in a specific group |

---

## Validation rules

**Username**
- 3 to 20 characters
- Letters, numbers, and underscores only
- Must be unique

**Password**
- 6 to 50 characters
- Stored as a SHA-256 hash — never in plain text

**Login**
- 3 attempts allowed before lockout for that session

---

## Project structure

```
main.py          Application entry point and all logic
README.md        This file
```

---

## Notes

- Private messages are visible to all logged-in users — this is by design for a shared bulletin-board style feed. If you need direct user-to-user private messaging, a `recipient` field would need to be added.
- Group admins cannot leave a group if they are the sole admin and other members remain. They must promote another member to admin first. Promoting members is not yet implemented in the UI — it would need to be added as a new menu option.
- Passwords are hashed with SHA-256. For production use, consider switching to `bcrypt` or `argon2` which are specifically designed for password hashing and resistant to brute-force attacks.
