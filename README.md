# meal-planner

# How It Works

## 1. User Interaction

**Trigger:** The workflow starts when a Telegram message is received.

**User Registration:**

- If the user doesn't exist in the database, they are added with their `id` and `first_name`.
- Missing profile fields are checked:
  - `weight`
  - `height`
  - `meal_freq`
  - `preferences`

---

## 2. Branching Logic

**If Missing Info:**

- The AI Agent prompts the user to provide missing details.
- Information is updated in the database via the **users updater** tool.

**If Profile Complete:**

- **AI Agent1** can handle:
  - Updating profile info.
  - Creating a personalized daily meal plan based on the user's details.

---

## 3. Core Tools & Components

- **Telegram Trigger** – Listens for incoming messages.
- **PostgreSQL** – Stores and retrieves user data.
- **AI Agents** – Powered by GPT-4.1-mini with memory via PostgreSQL.
- **Custom Tools:**
  - `search tool` – Queries user data from PostgreSQL.
  - `users updater` – Updates user profile fields.
  - `meal planner` – Generates daily meal plans.
- **Memory Management** – Maintains conversation history for continuity.

---

## 4. AI Agent Instructions

### AI Agent (Profile Completion Mode)

1. Use `search tool` to find missing fields.
2. Ask the user for missing data.
3. Update the profile using `users updater`.

### AI Agent1 (Full Service Mode)

1. Update fields when requested.
2. Retrieve user details to generate a personalized meal plan using `meal planner`.

---

## 5. Data Flow

Telegram Trigger
→ Add/check user in PostgreSQL
→ Check Missing Info
→ Missing fields? → AI Agent (Profile Completion) → Response via Telegram
→ All fields present? → AI Agent1 (Full Service) → Response via Telegram
