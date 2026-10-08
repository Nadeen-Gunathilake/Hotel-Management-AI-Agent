# Hotel Management AI Agent

A chat-based AI assistant for hotel front desk staff. Staff type normal sentences and the assistant manages customer records — adding, viewing, updating and deleting them - using function calling tools backed by a local SQLite database.

---

## Features

- **Add** a new customer record through natural conversation
- **View** a customer by ID or name — handles no match and duplicate names
- **Update** one or more fields of an existing customer
- **Delete** a customer with confirmation before anything is removed
- **List** all registered customers
- **Search** customers by check-in date
- **Check** room availability
- Permanent storage — records survive restarts
- Input validation via SQLite constraints with friendly error messages

---

## Tech Stack

| Layer | Tool |
|---|---|
| Language | Python |
| AI Model | GPT-4o (OpenAI) |
| Storage | SQLite |
| Interface | Gradio |
| Environment | python-dotenv |

---

## Setup

### 1. Clone the Repository

```bash
git clone https://github.com/Nadeen-Gunathilake/Hotel-Management-AI-Agent
cd hotel-agent
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Add Your API Key

Create a `.env` file in the root:

```
OPENAI_API_KEY=sk-xxxxxxxxxxxxxxxxxxxxxxxx
```

### 4. Run the Notebook

Open `src/hotel.ipynb` and run all cells. The database and rooms are initialized automatically on first run.

---

## Customer Data Fields

| Field | Type | Required | Rules |
|---|---|---|---|
| Customer ID | Integer | Auto | Created automatically. Unique. Never changes. |
| Full name | Text | Yes | Cannot be empty. |
| Phone number | Text | Yes | 9 to 15 digits. May start with +. |
| Email | Text | No | Must look like a real email address. |
| Room number | Text | Yes | For example 101 or A12. |
| Check-in date | Date | Yes | Format YYYY-MM-DD. |
| Check-out date | Date | Yes | Format YYYY-MM-DD. Must be after check-in. |
| Special requests | Text | No | Free text, for example "late check-in". |

---

## Example Conversations

**Adding a customer:**
```
Staff: Register a new guest, Jane Smith, room 204.
Agent: Happy to help. What is Jane's phone number, and her check-in and check-out dates?
Staff: 0712345678, from 2026-10-01 to 2026-10-04.
Agent: Saved! Customer #1: Jane Smith, room 204, 1 to 4 October 2026.
```

**Deleting a customer:**
```
Staff: Delete customer 1.
Agent: Do you really want to delete Jane Smith (room 204)? Please reply yes or no.
Staff: yes
Agent: Done. Customer #1 has been deleted.
```

---

## Available Tools

| Tool | Description |
|---|---|
| `get_customer_details` | Find a customer by ID or name |
| `save_customer_details` | Save a new customer record |
| `update_customer_details` | Update one or more fields |
| `delete_customer` | Delete after confirmation |
| `check_rooms` | Check room availability |
| `list_all_customers` | List all registered customers |
| `search_by_checkin_date` | Find customers by check-in date |
