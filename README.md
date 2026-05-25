# ⛽ FuelTracker

**Android app to log and analyze vehicle refueling history.**

FuelTracker is a personal app to keep detailed track of every fill-up — car, motorcycle, or any combustion vehicle. No account, no servers, no subscriptions. All data is stored locally on your device.

> 🚀 **Coming soon to Google Play Store**

---

## 📱 Screenshots

> *Coming soon*

---

## ✨ Features

- **Complete refuel logging:** date & time (auto-detected and editable), liters, total price or price per liter (automatic two-way calculation), odometer reading, location and free notes
- **Full / partial tank indicator** for accurate consumption calculations
- **Multiple vehicles** with custom name, type, engine, fuel type, color and icon
- **Configurable units:** distance (km / miles), volume (liters / US gal / UK gal), with automatic consumption unit derived from your selection
- **28 currencies supported** (€, $, £, R$, ¥, ₹, ₽ and more) plus custom currency option
- **Automatic statistics:** L/100km consumption, km between refuels, average price per liter, monthly spending
- **Interactive charts:** consumption trend, km per refuel, and price per liter evolution
- **Full history** with search and filters by vehicle, month and gas station
- **Edit and delete** any record with automatic cascading recalculation
- **CSV export** compatible with Excel — format adapts to device locale (separator and decimal symbol)
- **CSV import** with smart parser: auto-detects separator, locale and boolean values in 6 languages; supports "add without duplicates", "add all" and "replace" modes
- **Fully localized UI:** English and Spanish, with automatic detection from device settings
- **Light / dark / auto theme** following system preference, manually overridable
- **Android Adaptive Icons** support for a clean look on any launcher
- **100% offline** — no internet connection required at any time

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Language | Kotlin |
| UI | Jetpack Compose + Material Design 3 |
| Database | Room Database |
| Architecture | MVVM (ViewModel + StateFlow + Repository) |
| Navigation | Navigation Compose |
| Charts | Vico for Compose |
| Preferences | DataStore |
| Min SDK | Android 8.0 (API 26) |
| Target SDK | Android 14 (API 34) |

---

## 🗂️ Project Structure

```text
app/
├── data/
│   ├── database/          # Room Database, DAOs and entities
│   └── repository/        # VehicleRepository, RefuelRepository
├── domain/
│   ├── model/             # Domain models
│   └── usecase/           # Business logic (consumption, CSV, statistics)
├── ui/
│   ├── theme/             # Color tokens, typography and theme
│   ├── navigation/        # Navigation graph
│   ├── screens/           # Home, History, Charts, Form, Settings
│   └── components/        # Reusable composables
└── utils/                 # CsvExporter, CsvImporter, DateFormatter, NumberFormatter
```

---

## 🚀 Build & Install

### Prerequisites

- Android Studio Ladybug or later
- JDK 17+
- Android SDK with API 34

### Steps

```bash
# 1. Clone the repository
git clone https://github.com/fcr929/Fuel-Tracker.git
cd Fuel-Tracker

# 2. Open in Android Studio
#    File → Open → select the project folder

# 3. Build the debug APK
./gradlew assembleDebug

# 4. Output APK located at:
#    app/build/outputs/apk/debug/app-debug.apk
```

### Install directly on device

```bash
# With the device connected via USB and USB debugging enabled:
./gradlew installDebug
```

---

## 📊 Consumption Calculation Logic

Fuel consumption is calculated **only** between consecutive refuels marked as a **full tank**, using the odometer as an absolute reference:

```text
Consumption (L/100km) = (Liters_N / (Odometer_N - Odometer_N-1)) × 100
```

Partial refuels are excluded from consumption calculations, but their kilometers are correctly accumulated since the odometer is an absolute value.

Editing or deleting any record triggers an **automatic cascading recalculation** of all affected subsequent records.

All values are stored internally in **km and liters** regardless of the unit settings — conversions are applied only at the display layer, ensuring data consistency across unit changes.

---

## 📄 CSV Export Format

The exported file adapts automatically to the device locale:

| Setting | European locales (es, fr, de…) | English locale (en) |
|---|---|---|
| Column separator | `;` (semicolon) | `,` (comma) |
| Decimal separator | `,` (comma) | `.` (period) |
| Encoding | UTF-8 with BOM | UTF-8 with BOM |
| Date format | `DD/MM/YYYY` | `DD/MM/YYYY` |
| Column headers | Localized to device language | Localized to device language |

The file opens directly in Microsoft Excel and LibreOffice Calc without any additional configuration.

---

## 🔒 Privacy

- **No internet connection required.** The app works fully offline.
- **No accounts or sign-up.** No personal data is collected or transmitted.
- **100% local storage.** All data lives in the on-device Room database.
- **No ads** in the current version.

---

## 📋 Roadmap

- [ ] Google Play Store release
- [ ] Home screen widget showing the last refuel
- [ ] Optional automatic backup to Google Drive
- [ ] Electric vehicle support (kWh instead of liters)
- [ ] Multi-vehicle comparison on the same chart
- [ ] Additional language support beyond EN and ES

---

*Built with ❤️ and plenty of fuel.*
