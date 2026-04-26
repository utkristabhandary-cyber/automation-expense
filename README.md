
# WhatsApp Expense Bot

An automated expense tracker that monitors WhatsApp messages and extracts expense data into an Excel spreadsheet.

## 📋 Overview

This bot uses Selenium WebDriver to automate WhatsApp Web and intelligently parse expense messages, automatically logging them to an Excel file for easy tracking and analysis.

## ✨ Features

- **Automated Message Monitoring** - Continuously monitors incoming WhatsApp messages
- **Smart Expense Parsing** - Extracts expense data from specifically formatted messages
- **Excel Integration** - Automatically saves parsed expenses to `expenses.xlsx`
- **Timestamp Tracking** - Records date and time for each expense entry
- **Error Handling** - Gracefully handles parsing errors and connection issues

## 📋 Message Format

Messages must follow this format to be recognized:

```
[quantity] [item] [unit_price] rs total [total_price]
```

### Examples:
```
2 apples 50 rs total 100
5 books 200 rs total 1000
3 coffee 150 rs total 450
```

## 🛠️ Prerequisites

- Python 3.6+
- Google Chrome browser
- ChromeDriver (matching your Chrome version)
- WhatsApp Account

## 📦 Required Packages

Install the required dependencies:

```bash
pip install selenium pandas openpyxl
```

## ⚙️ Configuration

Before running the bot, update the configuration in the script:

```python
EXCEL_FILE = "expenses.xlsx"              # Output Excel file path
CHROME_PROFILE_PATH = r"C:\Users\User\whatsapp_profile"  # Your Chrome profile path
```

### Chrome Profile Setup

1. Create a folder for your Chrome profile (or use an existing one)
2. Update `CHROME_PROFILE_PATH` to point to this folder
3. This allows the bot to use your WhatsApp session without re-scanning QR code

## 🚀 Usage

1. Run the script:
```bash
python whatsapp_expense_bot.py
```

2. Wait for WhatsApp Web to load
3. The script will prompt you to manually open your own chat:
```
👉 Open YOUR OWN CHAT manually, then press ENTER...
```

4. Once you press ENTER, the bot will start monitoring messages

5. Send messages in the specified format to your chat (e.g., send to yourself)

6. The bot will parse, process, and save them to `expenses.xlsx`

## 📊 Output

The script creates/updates `expenses.xlsx` with the following columns:

| Date | Time | Item | Quantity | Price | Total |
|------|------|------|----------|-------|-------|
| 2024-01-15 | 14:30:45 | apples | 2 | 50 | 100 |
| 2024-01-15 | 14:31:20 | coffee | 3 | 150 | 450 |

## 🔍 How It Works

1. **Connection** - Opens WhatsApp Web using Selenium
2. **Monitoring** - Continuously scans for new outgoing messages
3. **Parsing** - Uses regex to extract quantity, item, price, and total from messages
4. **Storage** - Appends parsed data to the Excel file with timestamp
5. **Loop** - Repeats every 5 seconds

## ⚠️ Important Notes

- The script monitors **outgoing messages only** (messages you send)
- Messages are tracked using a set to avoid duplicate entries
- Unrecognized message formats are logged with "⚠️ Format not matched"
- The script runs continuously until manually stopped (Ctrl+C)
- Ensure your Chrome profile path exists before running

## 🐛 Troubleshooting

### Chrome Not Opening
- Verify Chrome is installed and up to date
- Check that ChromeDriver version matches your Chrome version
- Ensure `CHROME_PROFILE_PATH` exists

### Messages Not Being Detected
- Verify messages follow the exact format: `[qty] [item] [price] rs total [total]`
- Ensure you're sending messages in your own chat (the one opened manually)
- Check browser console for JavaScript errors

### Excel File Errors
- Ensure `expenses.xlsx` path is writable
- Close Excel if it's open while the bot is running
- Verify `openpyxl` is installed: `pip install openpyxl`

## 📝 License

This project is provided as-is for personal use.

## 👤 Author

Automation Bot - Expense Tracker

---

**Happy tracking! 📊**
