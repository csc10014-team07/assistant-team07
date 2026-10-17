# Data Component (`retrieval-data`)

This directory contains static datasets used by the assistant to answer queries regarding campus offices, rooms, and opening hours.

## Data Inventory

| File | Description | Source | Owner | Update Frequency |
| :--- | :--- | :--- | :--- | :--- |
| `offices.csv` | Campus office directory with room locations and opening hours | Public campus information / HCMUS student portal (https://www.hcmus.edu.vn) | Component: `retrieval-data` (Team 07) | Per semester / Upon university announcements |

---

## File Details

### `offices.csv`

- **Description**: Tabular dataset containing campus office names, room numbers, and operating schedules used for rule-based retrieval.
- **Source**: Publicly available university directory and student handbook of VNU-HCM University of Science (HCMUS).
- **Owner**: `retrieval-data` component team (Team 07).
- **Update Frequency**: Per semester or whenever office schedules / room allocations change.
- **Schema**:
  - `name` (*string*): Official or common name of the university department/office (e.g., `Training Office`, `Student Affairs`, `Library`, `IT Helpdesk`).
  - `room` (*string*): Campus building and room identifier (e.g., `I.101`, `B.201`, `E.005`).
  - `hours` (*string*): Working days and operational hours (e.g., `Mon-Fri 07:30-16:30`, `Mon-Sat 07:00-20:00`).

#### Sample Content

```csv
name,room,hours
Training Office,I.101,Mon-Fri 07:30-16:30
Student Affairs,I.102,Mon-Fri 08:00-16:00
Library,B.201,Mon-Sat 07:00-20:00
IT Helpdesk,E.005,Mon-Fri 08:00-17:00
```

---

## Data Processing & Validation

- **Encoding**: Files must be saved in UTF-8 encoding with UNIX (`\n`) or standard Windows (`\r\n`) line endings.
- **Delimiter**: Comma-separated (`header: name,room,hours`).
- **Data Quality**:
  - No empty or null values in any column.
  - Room identifiers must follow university conventions (e.g., `<Building>.<RoomNumber>`).
  - Working hours must be clear and formatted with consistent day and time ranges.

---

## Usage in Codebase

The data is loaded dynamically in `src/assistant/rules.py` via the `load_offices()` function:

```python
from pathlib import Path
import csv

DATA_DIR = Path(__file__).resolve().parents[2] / "data"

def load_offices(path: Path = DATA_DIR / "offices.csv") -> dict[str, dict[str, str]]:
    with path.open(encoding="utf-8", newline="") as f:
        return {row["name"].lower(): row for row in csv.DictReader(f)}
```

---

## Security & Privacy Guidelines

In accordance with the team's Definition of Done:
- Only public and authorized university information may be committed.
- **Do not commit** student personal information, staff private contact details, credentials, or confidential internal data.
