# Court Listing Fetcher

A Python script to fetch court listings and cause lists from [eCourts](https://services.ecourts.gov.in/ecourtindia_v6/).  
This version is designed for assignment/demo use with robust error handling and clear instructions.

---

## Table of Contents

- [Project Description](#project-description)
- [Features](#features)
- [Environment Setup](#environment-setup)
- [Installation](#installation)
- [Usage](#usage)
- [CLI Options](#cli-options)
- [Output](#output)
- [Error Handling](#error-handling)
- [Directory Structure](#directory-structure)
- [Examples](#examples)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## Project Description

**Court Listing Fetcher** allows users to check Indian court case listings and download cause lists using simple CLI commands.  
It is suitable for students, developers, and anyone needing automated access to eCourts listings.

---

## Features

- Input case details via CNR or Case Type, Number, and Year
- Check if a case is listed today or tomorrow
- Display serial number, court name, status, and PDF download link (if available)
- Download full cause list for today
- Console output with JSON file export to `data/` directory
- Clear error messages for invalid or missing inputs
- Easy-to-use CLI flags
- Extensible codebase for future web/API integration

---

## Environment Setup

Follow these steps to prepare your development environment:

### 1. Python Version

- Requires **Python 3.6 or newer**
- Check your version:
  ```sh
  python --version
  ```

### 2. Virtual Environment (Recommended)

Create and activate a virtual environment to isolate dependencies:

```sh
python3 -m venv venv
```

**Activate the environment:**

- **Windows:**
  ```sh
  venv\Scripts\activate
  ```

- **macOS/Linux:**
  ```sh
  source venv/bin/activate
  ```

Your terminal prompt should now display `(venv)`.

### 3. Install Dependencies

With the virtual environment active, install required packages:

```sh
pip install requests beautifulsoup4
```

**Optional** (for code quality and testing):

```sh
pip install flake8 pytest
```

### 4. Verify Setup

Confirm that all dependencies are installed correctly:

```sh
python -c "import requests, bs4; print('Setup successful!')"
```

---

## Installation

Clone this repository or download the script files to your local machine:

```sh
git clone https://github.com/yourusername/court-listing-fetcher.git
cd court-listing-fetcher
```

Make the script executable (Linux/macOS):

```sh
chmod +x ecourt.py
```

---

## Usage

Run the script from the command line with the appropriate flags.

### Check Today's Listing by CNR

```sh
python ecourt.py --cnr 1234567890123456 --today
```

### Check Listing by Case Details

```sh
python ecourt.py --type CR --number 42 --year 2022 --today
```

### Download Today's Cause List

```sh
python ecourt.py --causelist
```

### Check Tomorrow's Listing

```sh
python ecourt.py --cnr 1234567890123456 --tomorrow
```

### Get Help

```sh
python ecourt.py --help
```

---

## CLI Options

| Option         | Description                                            |
|----------------|--------------------------------------------------------|
| `--cnr`        | CNR Number (16 alphanumeric characters)                |
| `--type`       | Case type (e.g., CR, CIVIL)                            |
| `--number`     | Case number                                            |
| `--year`       | Case year (4 digits)                                   |
| `--today`      | Check today's listings                                 |
| `--tomorrow`   | Check tomorrow's listings                              |
| `--causelist`  | Download today's cause list                            |

**Note:** You must provide either `--cnr` **or** all three of `--type`, `--number`, and `--year` when checking listings.

---

## Output

### Console

All case details, cause lists, and error messages are displayed in the terminal.

### Files

Results are automatically saved as JSON files in the `data/` directory:

- `case_today.json` - Today's case listing details
- `case_tomorrow.json` - Tomorrow's case listing details
- `cause_list_today.json` - Today's full cause list

---

## Error Handling

The script provides clear error messages for common issues:

- **Invalid CNR format** (not 16 characters): Displays format requirements
- **Missing case identifiers**: Prompts user to provide either CNR or all case details
- **Invalid year**: Ensures year is a valid 4-digit number
- **Network errors**: Handles connection issues gracefully
- **Unexpected errors**: Logs full traceback and exits safely

---

## Directory Structure

```
court-listing-fetcher/
├── ecourt.py
├── data/
│   ├── case_today.json
│   ├── case_tomorrow.json
│   └── cause_list_today.json
├── README.md
└── LICENSE
```

---

## Examples

### Example 1: Valid CNR Input

```sh
python ecourt.py --cnr ABCD12345678WXYZ --today
```

**Output:**
```json
{
    "case_id": "ABCD12345678WXYZ",
    "checked_on": "2025-10-15 22:18:00",
    "date_checked_for": "2025-10-15",
    "is_listed": true,
    "serial_no": "15",
    "court_name": "Courtroom 2 – Hon'ble Justice R. Verma",
    "status": "Listed for Hearing",
    "pdf_url": "https://example.com/sample_case_order.pdf"
}
```

### Example 2: Missing Required Fields

```sh
python ecourt.py --type CR --today
```

**Output:**
```
❌ Missing required case identifiers.
You must provide either:
  --cnr CNR_NUMBER  OR
  --type TYPE --number NUMBER --year YEAR
Example: --type CR --number 42 --year 2022
```

---

## Contributing

Contributions are welcome! To contribute:

1. Fork this repository
2. Create a feature branch (`git checkout -b feature/YourFeature`)
3. Commit your changes (`git commit -m 'Add YourFeature'`)
4. Push to the branch (`git push origin feature/YourFeature`)
5. Open a Pull Request

For major changes, please open an issue first to discuss proposed modifications.

---

## License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

---

## Contact

**Project Maintainer:veera6102 
**Email:** veerach010@gmail.com 
**GitHub:** [@yourusername](https://github.com/veera6102)

---

## Quick Start

1. Set up your Python environment (Python 3.6+)
2. Install dependencies: `pip install requests beautifulsoup4`
3. Run `python ecourt.py --help` to see all available options
4. Start checking case listings with your CNR or case details

---

**Note:** This is a mock/demo version designed for educational and assignment purposes. For production use with real eCourts data, additional API integration and authentication may be required.
