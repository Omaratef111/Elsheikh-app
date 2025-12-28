# Elsheikh Accounting Management Application

A comprehensive desktop accounting management system built with Python and Tkinter for managing memberships, walk-ins, sales persons, commissions, and financial reporting.

## 📋 Table of Contents

- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Building the Executable](#building-the-executable)
- [Auto-Update System](#auto-update-system)
- [Project Structure](#project-structure)
- [Configuration](#configuration)
- [Troubleshooting](#troubleshooting)

## ✨ Features

### Core Functionality
- **Membership Management**: Track subscriptions, plans, payments, and client information
- **Walk-ins Management**: Handle daily walk-in customers and payments
- **In Body Plans**: Special tracking for In Body membership plans
- **Sales Persons**: Track sales performance and calculate commissions
- **Monthly Commission Tracking**: View commissions by month with plan-specific rates
- **Client Management**: Comprehensive client database with transaction history
- **Refunds Processing**: Handle full and partial refunds for memberships

### Financial Features
- **Dashboard**: Real-time metrics, charts, and financial overview
- **Reports**: Detailed reports by date range, payment method, transaction type
- **Payment Methods**: Support for Visa, Cash, CIB, Bank Transfer, Paymob, Addwins
- **Split Payments**: Handle "Both" payment methods by splitting into separate transactions
- **Payment Batches**: Group and manage payment terminal batches
- **Tax Management**: Calculate and track VAT and other taxes
- **Total Refunds Tracking**: Monitor all refunded amounts

### Advanced Features
- **Data Import**: Import subscriptions and walk-ins from Excel files
- **Data Comparison**: Compare imported data with existing records
- **Backup & Restore**: Backup and restore database functionality
- **Auto-Update System**: Automatic update checking and installation via GitHub
- **Modern UI**: Clean, modern interface with dark sidebar and light content area
- **Export Options**: Export data to Excel (XLSX) and PDF formats

## 📦 Requirements

### Python Version
- Python 3.8 or higher

### Required Packages
Install all dependencies using:
```bash
pip install -r requirements.txt
```

**Key Dependencies:**
- `pandas` - Data processing and analysis
- `openpyxl` - Excel file handling
- `matplotlib` - Data visualization and charts
- `reportlab` - PDF generation
- `Pillow` - Image processing
- `emoji` - Emoji support
- `pygame` - Audio playback (for startup sound)

### Optional (for building executable)
- `pyinstaller` - For creating standalone .exe file

## 🚀 Installation

### From Source

1. **Clone or download the repository**
   ```bash
   git clone <repository-url>
   cd accounting_app
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Run the application**
   ```bash
   python main.py
   ```

### From Executable

1. Download `ElsheikhAccounting.exe` from the releases
2. Run the executable (no installation required)
3. The application will create necessary folders on first run

## 💻 Usage

### First Run
- On first launch, you'll see a welcome dialog
- The app will automatically check for data files in the `data/` folder
- If Excel files are found, you'll be prompted to import them

### Main Features

#### Dashboard
- View key metrics: Total Revenue, Transactions, Total Refunds, Payment Methods
- See growth rate, average daily revenue, peak revenue day, retention rate
- Interactive charts: Payment Method breakdown, Revenue trends, Pie charts
- Payment method and transaction type breakdowns

#### Memberships
- View all membership subscriptions
- Filter by date range, payment method, status, plan
- Edit membership details
- Process refunds (full or partial)
- Export to Excel

#### Walk-ins
- Manage daily walk-in customers
- Track payments and cancellations
- Filter and search functionality

#### Sales Persons
- View sales performance by person
- **Monthly Commission Tracking**: 
  - Current Month Commission (default view)
  - All Months Commission (historical view)
- **Commission Rates Management**: Set commission rates per plan
- View detailed sales breakdown
- Export reports

#### Reports
- Generate comprehensive reports
- Filter by date range, payment method, transaction type
- Export to Excel and PDF

#### Settings
- Configure application settings
- **Check for Updates**: Manual update check button
- View current version information

## 🔨 Building the Executable

### Using the Batch File (Windows)

1. **Run the build script**
   ```bash
   build_exe.bat
   ```

2. **Find your executable**
   - Location: `dist/ElsheikhAccounting.exe`
   - The executable is standalone and includes all dependencies

### Manual Build

```bash
pyinstaller --clean --noconsole --onefile --name ElsheikhAccounting --icon "app_icon.ico" --version-file "file_version_info.txt" --add-data "app_icon.ico;." --add-data "startup_sound.wav;." --add-data "database;database" --add-data "data;data" --add-data "templates;templates" --hidden-import pandas --hidden-import openpyxl --hidden-import matplotlib --hidden-import reportlab --hidden-import PIL main.py
```

## 🔄 Auto-Update System

The application includes an automatic update system that checks for new versions via GitHub.

### Setup

1. **Create a GitHub repository** for hosting updates (see `GITHUB_UPDATE_SETUP.md`)

2. **Configure the update URL** in `config.py`:
   ```python
   UPDATE_CHECK_URL = "https://raw.githubusercontent.com/YOUR_USERNAME/REPO_NAME/main/version.json"
   ```

3. **How it works:**
   - App checks for updates 2 seconds after startup (non-blocking)
   - If a newer version is found, shows update dialog
   - User can download and install immediately or later
   - Updates are downloaded to `updates/` folder
   - Installer launches automatically

### Manual Update Check

- Go to **Settings** page
- Click **"🔄 Check for Updates"** button

For detailed setup instructions, see [GITHUB_UPDATE_SETUP.md](GITHUB_UPDATE_SETUP.md)

## 📁 Project Structure

```
accounting_app/
├── main.py                 # Application entry point
├── config.py              # Configuration settings
├── requirements.txt       # Python dependencies
├── build_exe.bat         # Build script for executable
├── modules/              # Core business logic
│   ├── database.py      # Database management
│   ├── data_processor.py
│   ├── reporting_engine.py
│   ├── sales_person_manager.py
│   ├── update_checker.py  # Auto-update system
│   └── ...
├── ui/                   # User interface
│   ├── main_window.py   # Main application window
│   ├── pages/           # Page components
│   ├── update_dialog.py # Update notification dialog
│   └── ...
├── data/                # Data files (Excel imports)
│   ├── subscriptions/
│   └── walk_ins/
├── database/            # SQLite database
├── templates/           # JSON templates
└── dist/               # Built executables
```

## ⚙️ Configuration

### Version Management
Edit `config.py` to update the application version:
```python
VERSION = "1.5"
```

### Update Settings
```python
UPDATE_CHECK_URL = "https://raw.githubusercontent.com/username/repo/main/version.json"
```

### Database Path
Database is automatically created at:
```
database/accounting.db
```

### Data Directories
- Subscriptions: `data/subscriptions/`
- Walk-ins: `data/walk_ins/`
- Backups: Created automatically in `backups/` folder

## 🐛 Troubleshooting

### Application Won't Start
- Check Python version (3.8+ required)
- Verify all dependencies are installed: `pip install -r requirements.txt`
- Check logs in `logs/app.log`

### Database Issues
- Database is automatically created on first run
- If corrupted, delete `database/accounting.db` and restart (data will be lost)

### Import Errors
- Ensure Excel files are in correct format
- Check file paths in `data/subscriptions/` and `data/walk_ins/`
- Verify Excel files are not open in another program

### Update Check Fails
- Verify `UPDATE_CHECK_URL` is set correctly in `config.py`
- Check internet connection
- Ensure GitHub repository is accessible
- See `GITHUB_UPDATE_SETUP.md` for detailed troubleshooting

### Performance Issues
- Large datasets may take time to load
- Use date filters to limit data range
- Database indexes are automatically created for performance

## 📝 Version History

### Version 1.5 (Current)
- Monthly commission tracking system
- Plan-specific commission rates
- Total refunds tracking on dashboard
- Auto-update system integration
- Improved UI and performance

### Previous Versions
- See `backups/` folder for version history

## 📄 License

Copyright (C) 2025 Elsheikh Accounting. All rights reserved.

## 👤 Author

Dr. Omar Atef Elsheikh

## 📧 Support

For issues, questions, or feature requests, please contact through the application's Telegram link (available in welcome dialog).

## 🙏 Acknowledgments

Built with:
- Python & Tkinter
- SQLite for database
- Pandas for data processing
- Matplotlib for visualization
- ReportLab for PDF generation

---

**Note**: This is a beta version for testing. Please report any issues or suggestions for improvement.

