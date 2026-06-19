#  Expense Tracker

A command-line expense tracking application built with **pure Python** and **OOP principles**. Stores data in both CSV and JSON formats, supports interactive menus locally, and runs in demo mode on Kaggle/Colab with no input required.

---

## Skills Demonstrated

| Skill | Usage |
|---|---|
| **Python Fundamentals** | Dataclasses, type hints, properties, list comprehensions, `defaultdict` |
| **OOP** | `Expense` model, `StorageManager` persistence layer, `ExpenseTracker` controller |
| **CSV Storage** | `csv.DictWriter` / `DictReader` for structured tabular output |
| **JSON Storage** | Full metadata export (`last_updated`, `count`); preferred format on load |

---

## Features

-  **Add expenses** — category, description, amount, date, currency; validates all inputs
-  **View reports** — filterable by month, category, or amount range
-  **Monthly summaries** — total, average, count, top category per month
-  **Delete entries** — by ID, with confirmation
-  **Dual storage** — saves to both `expenses.csv` and `expenses.json` on every write
-  **Interactive menu** — full CLI menu for local use
-  **Demo mode** — auto-runs with 26 sample entries (Kaggle/Colab compatible)

---

## Installation

```bash
# Clone the repository
git clone https://github.com/your-username/expense-tracker.git
cd expense-tracker

# Install dependencies (rich is optional — plain-text fallback built in)
pip install rich
```

---

## Usage

**Local (interactive menu):**
```python
# Edit these two lines at the top of expense_tracker.py
DEMO_MODE   = False
STORAGE_DIR = Path(".")    # saves to current folder
```
```bash
python expense_tracker.py
```

**Kaggle / Colab (demo mode):**
```python
# Default settings — just run the cell
DEMO_MODE   = True
STORAGE_DIR = Path("/kaggle/working")
```

---

## Project Structure

```
expense-tracker/
│
├── expense_tracker.py          # Main application (local + Kaggle)
├── expenses.csv                # Generated on run (CSV storage)
├── expenses.json               # Generated on run (JSON storage)
└── README.md
```

---

## Sample Output

```
══════════════════════════════════════════════════════════════
  EXPENSE TRACKER  —  DEMO MODE
══════════════════════════════════════════════════════════════

  ── STEP 1: Adding 26 sample expenses …

    ✔  [0001] 2024-04-01  Housing         USD 1,200.00  Monthly rent
    ✔  [0002] 2024-04-03  Utilities          USD 85.50  Electricity bill
    ✔  [0003] 2024-04-05  Food               USD 45.20  Weekly groceries
    ...

  Total entries: 26
  Total spent  : $5,190.67

══════════════════════════════════════════════════════════════
  Spending by Category  (All Time)
══════════════════════════════════════════════════════════════

  Category           Amount     Share   Bar
  Housing         $3,600.00    69.4%   █████████████
  Shopping          $650.00    12.5%   ██
  Food              $331.20     6.4%   █
  Utilities         $255.50     4.9%
  Healthcare        $170.00     3.3%

══════════════════════════════════════════════════════════════
  Monthly Summaries
══════════════════════════════════════════════════════════════

  Month     Expenses   Total Spent   Average   Top Category
  2024-06   8          $1,785.69     $223.21   Housing
  2024-05   9          $1,756.29     $195.14   Housing
  2024-04   9          $1,648.69     $183.19   Housing
```

**Interactive menu (local):**
```
  ┌─────────────────────────────┐
  │    EXPENSE TRACKER MENU     │
  ├─────────────────────────────┤
  │  1  Add expense             │
  │  2  View all expenses       │
  │  3  Filter by month         │
  │  4  Category report         │
  │  5  Monthly summaries       │
  │  6  Delete expense          │
  │  7  Total spent             │
  │  0  Exit                    │
  └─────────────────────────────┘
```

---

## Data Model

### `Expense` (dataclass)
| Field | Type | Description |
|---|---|---|
| `id` | int | Auto-incrementing unique ID |
| `date` | str | ISO date `YYYY-MM-DD` |
| `category` | str | One of 9 predefined categories |
| `description` | str | Free-text label |
| `amount` | float | Positive value, rounded to 2dp |
| `currency` | str | Default `USD` |

### Supported Categories
`Food` · `Transport` · `Housing` · `Entertainment` · `Healthcare` · `Education` · `Shopping` · `Utilities` · `Other`

---

## Architecture

```
ExpenseTracker          ← controller (add, delete, filter, report)
    │
    ├── Expense         ← dataclass model (validation, properties)
    │
    └── StorageManager  ← persistence layer (CSV + JSON read/write)
```

---

## Dependencies

```
rich>=13.0   # optional — plain-text fallback included
```

> No external dependencies required for core functionality.
