# Singlish Transliteration Accuracy Testing

Playwright-based Python automation for testing the **Chat Sinhala** transliteration function at [pixelssuite.com/chat-translator](https://www.pixelssuite.com/chat-translator).

This project contains **50 negative test cases** (inputs where the system fails to correctly convert chat-style Singlish into Sinhala), covering all **24 Singlish input types** defined in the assignment.

---

## 📁 Project Structure

```
test_automation/
├── test_automation.py              # Main Playwright automation script
├── Assignment 1 - Test cases.xlsx  # Excel file with 50 test cases (TC ID, Input, Expected, Actual, Status)
├── get-pip.py                      # pip installer bootstrap (run if pip is missing)
└── README.md                       # This file
```

> **Note:** There is no `requirements.txt` or `create_excel.py` in this project.  
> The Excel file is already pre-filled with all 50 test cases. Just install dependencies and run.

---

## ✅ Prerequisites

- **Python 3.11 or 3.12** — [Download](https://www.python.org/downloads/)
- **pip** (bundled with Python; if missing, run `python get-pip.py`)
- **Google Chrome** or Chromium (Playwright installs Chromium automatically)

---

## 📦 Installation (One-Time)

Open a terminal in this project folder (`test_automation/`) and run:

```bash
# Step 1: Install Playwright
pip install playwright

# Step 2: Install openpyxl (for reading/writing Excel)
pip install openpyxl

# Step 3: Install Playwright browser (Chromium)
playwright install chromium
```

> If `pip` is not found, run `python get-pip.py` first, then retry Step 1.

---

## ▶️ Running the Automation

```bash
python test_automation.py ^
  --excel "Assignment 1 - Test cases.xlsx" ^
  --url "https://www.pixelssuite.com/chat-translator" ^
  --wait-ms 5000 ^
  --type-delay-ms 80 ^
  --slow-mo-ms 200 ^
  --save-every 1 ^
  --keep-open
```

### Command-Line Arguments

| Argument | Default | Description |
|---|---|---|
| `--excel` | Auto-detected | Path to the Excel test cases file |
| `--sheet` | `" Test cases"` | Sheet name inside the Excel file |
| `--url` | pixelssuite URL | URL of the Chat Sinhala translator |
| `--wait-ms` | `5000` | Milliseconds to wait after clicking Transliterate |
| `--retries` | `8` | Retries to detect output change |
| `--retry-wait-ms` | `1000` | Delay between retries (ms) |
| `--type-delay-ms` | `30` | Delay between keystrokes (ms) |
| `--timeout-ms` | `60000` | Max wait for page/element to load |
| `--slow-mo-ms` | `0` | Playwright slow-motion delay (ms) |
| `--save-every` | `0` | Save Excel every N test cases (`1` = after each) |
| `--keep-open` | flag | Keep browser open after tests finish |
| `--headless` | flag | Run browser in headless mode (no visible UI) |
| `--output` | Same as `--excel` | Output Excel file path (defaults to input file) |

---

## 📊 How It Works

1. **Opens** the Chromium browser and navigates to the Chat Sinhala translator.
2. **Reads** each row from the Excel file (columns: Input, Expected output).
3. **Types** the Singlish input into the left textarea.
4. **Clicks** the `Transliterate` button.
5. **Waits** for the Sinhala output to appear in the right textarea.
6. **Compares** actual output vs. expected output → writes `PASS` or `FAIL` to the `Status` column.
7. **Saves** results back to the same Excel file.

---

## 📋 Excel File Structure

The file `Assignment 1 - Test cases.xlsx` contains the sheet **` Test cases`** with these columns:

| Column | Description |
|--------|-------------|
| Test Case ID | Unique ID — format `Neg_XXXX` |
| Input length type | `S` (Short) or `M` (Medium) |
| Input | Singlish input string |
| Expected output | Correct Sinhala translation |
| Actual output | Auto-filled by the script |
| Status | Auto-filled: `PASS` / `FAIL` |

### Sample Test Cases

| Test Case ID | Type | Input | Status |
|---|---|---|---|
| Neg_0001 | M | aya me phato eka uuu.facebook.com eka share karanna. | FAIL |
| Neg_0002 | S | ayakathanada inne dan? | FAIL |
| Neg_0003 | M | mo uada tika karala iwara karanna thaua kachchara uda yada? | FAIL |
| Neg_0004 | S | okapaththakin thiyanno. | FAIL |
| Neg_0009 | M | ano malli, paddek e kade gihin mata thekalaironi qannaka. | FAIL |
| Neg_0010 | M | ai aya oka paratama mahama uada karanne kiyala mata theranno ne? | FAIL |
| Neg_0011 | S | olaolamanonnam. | FAIL |
| Neg_0012 | M | hari aiya, mama e uada udana karalaiwara karala thiyonnam. | FAIL |
| Neg_0015 | S | ammmall!ekanam patta... | FAIL |
| Neg_0016 | M | makak?? aya kiuuo eththida? mata ibusuarathnaka! | FAIL |

> All 50 test cases are **negative** — the system is expected to produce incorrect output, demonstrating limitations of the transliterator.

---

## 🗂️ Test Case Summary

| # | Singlish Input Type | TC IDs |
|---|---|---|
| 1 | Question forms | Neg_0001, Neg_0002 |
| 2 | Command forms | Neg_0003, Neg_0004 |
| 3 | Greetings | Neg_0005, Neg_0006 |
| 4 | Requests | Neg_0007, Neg_0008 |
| 5 | Responses | Neg_0009, Neg_0010 |
| 6 | Repeated Words | Neg_0011, Neg_0012 |
| 7 | Inputs with Punctuation Marks | Neg_0013, Neg_0014 |
| 8 | Romanization / Spelling Variants | Neg_0015, Neg_0016 |
| 9 | Isolated English Word Insertions | Neg_0017, Neg_0018 |
| 10 | Multi-Word English Phrases | Neg_0019, Neg_0020 |
| 11 | English Digital Terms | Neg_0021, Neg_0022 |
| 12 | Platform / App Names | Neg_0023, Neg_0024 |
| 13 | English Abbreviations / Acronyms | Neg_0025, Neg_0026 |
| 14 | English Clipped Forms | Neg_0027, Neg_0028 |
| 15 | Place Names Embedded | Neg_0029, Neg_0030 |
| 16 | Person Names Embedded | Neg_0031, Neg_0032 |
| 17 | Numbers and Numeric Suffixes | Neg_0033, Neg_0034 |
| 18 | Inputs with Currency | Neg_0035, Neg_0036 |
| 19 | Inputs with Time Formats | Neg_0037, Neg_0038 |
| 20 | Inputs with Dates | Neg_0039, Neg_0040 |
| 21 | Unit of Measurements | Neg_0041, Neg_0042 |
| 22 | Slang and Casual Phrasing | Neg_0043, Neg_0044 |
| 23 | Online Identifiers | Neg_0045, Neg_0046 |
| 24 | Inputs Containing Emojis | Neg_0047, Neg_0048 |
| — | Extra (Platform / App Names) | Neg_0049 |
| — | Extra (Multi-Word English Phrases) | Neg_0050 |

---

## 📝 Notes

- All 50 test cases are **negative** (expected to fail), as required by the assignment.
- TC IDs all begin with `Neg_` as per assignment guidelines.
- None of the test inputs duplicate examples from Appendix 1 or Appendix 2.
- The script targets the **Chat Sinhala** transliteration function only.
- Results are written directly back into `Assignment 1 - Test cases.xlsx`.
- The `get-pip.py` file is only needed if `pip` is not installed on your system.
