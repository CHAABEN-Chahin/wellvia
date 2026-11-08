# HealthTrack Wearable App

![HealthTrack Logo](assets/images/logo.png)

## 📱 About

**HealthTrack Wearable** is an AI-powered health and nutrition companion mobile application developed for the **IEEE CSTAM2.0 Technical Challenge**. The app connects to an ESP32-based wearable device via Bluetooth to monitor real-time health vitals and provide personalized health insights.

**Developer:** CHAABEN-Chahin  
**Date:** November 15, 2025  
**Platform:** Flutter (iOS + Android)  
**Challenge:** IEEE CSTAM2.0 Technical Challenge

---

## ✨ Features

### Core Functionality
- 🔵 **Bluetooth Connectivity** - Seamless connection to ESP32 wearable device
- ❤️ **Real-time Vital Monitoring** - Heart rate, SpO2, temperature tracking
- 🚨 **Intelligent Alert System** - Emergency, critical, and warning health alerts
- 📊 **Advanced Analytics** - Daily, weekly, and monthly health trends
- 🏃 **Workout Tracking** - Session tracking with real-time metrics
- 🍽️ **Nutrition Logging** - AI-powered food recognition (placeholder API)
- 🌙 **Wellness Scoring** - Holistic health assessment
- 💪 **Motivation System** - Context-aware motivational messages

### Health Monitoring
- **Heart Rate Zones** - Resting, Fat Burn, Cardio, Peak
- **SpO2 Tracking** - Oxygen saturation monitoring
- **Temperature Monitoring** - Body temperature with fever detection
- **Activity Detection** - Steps, distance, calories burned
- **Stress Assessment** - HRV-based stress level calculation
- **BMI Calculator** - Body mass index with category interpretation

---

## 🎨 Design System

### Color Palette
- **Dark Theme Base**
  - Primary Dark: `#0F101A`
  - Secondary Dark: `#1A1C2C`
  - Tertiary Dark: `#23243A`

- **Primary Accents (Pink/Red)**
  - Pink Primary: `#FF2E78`
  - Pink Secondary: `#FF4C75`
  - Red Accent: `#FF3344`

- **Secondary Accents (Purple)**
  - Purple Primary: `#8A5AFF`
  - Purple Secondary: `#C047FF`

### Design Features
- ✨ Glassmorphism cards with blur effects
- 🎨 Pink-to-purple gradient accents
- 📈 Smooth animated charts
- 💫 Circular progress indicators
- 🌟 Neumorphic elements with shadows

---

## 🏗️ Architecture

### Tech Stack
- **Framework:** Flutter 3.0+
- **State Management:** Provider
- **Database:** SQLite (sqflite)
- **Bluetooth:** flutter_blue_plus
- **Charts:** fl_chart, syncfusion_flutter_charts
- **Notifications:** flutter_local_notifications

### Project Structure
```
lib/
├── core/
│   ├── theme/          # App theme, colors, text styles
│   ├── constants/      # App-wide constants
│   └── utils/          # Validators, helpers
├── models/             # Data models
├── services/           # Business logic services
├── providers/          # State management
├── screens/            # UI screens
├── widgets/            # Reusable widgets
└── main.dart           # Entry point
```

---

## 🚀 Getting Started

### Prerequisites
- Flutter SDK 3.0 or higher
- Android Studio / VS Code
- Android SDK (for Android development)
- Xcode (for iOS development - macOS only)

### Installation

1. **Clone or Extract the Project**
   ```bash
   cd mobile_app_3
   ```

2. **Install Dependencies**
   ```bash
   flutter pub get
   ```

3. **Note: Font Files Required**
   
   This project uses custom fonts that need to be downloaded separately:
   - Poppins (Regular, Medium, SemiBold, Bold)
   - Inter (Regular, Medium, SemiBold)
   
   Download from [Google Fonts](https://fonts.google.com/) and place in:
   ```
   fonts/
   ├── Poppins-Regular.ttf
   ├── Poppins-Medium.ttf
   ├── Poppins-SemiBold.ttf
   ├── Poppins-Bold.ttf
   ├── Inter-Regular.ttf
   ├── Inter-Medium.ttf
   └── Inter-SemiBold.ttf
   ```

4. **Run the App**
   ```bash
   flutter run
   ```

---

## 🧪 Testing with Mock Data

The app includes a **Mock Data Service** for testing without physical hardware.

### Enable Mock Mode
In `main.dart` or provider initialization, mock data is enabled by default. The app will simulate:
- Realistic heart rate patterns (resting, walking, running, sleeping)
- SpO2 variations
- Temperature readings
- Accelerometer and gyroscope data
- Battery drain simulation

### Test Scenarios
The mock service includes specific test scenarios:
- **Critical Heart Rate** - Triggers emergency alerts
- **Low SpO2** - Simulates low oxygen levels
- **High Fever** - Tests temperature alerts
- **Emergency HR** - Tests emergency protocols

---

## 📊 Database Schema

### Key Tables
- `users` - User authentication data
- `user_profile` - Personal info, health conditions, goals
- `raw_sensor_data` - Real-time vital signs from device
- `wellness_metrics` - Daily aggregated health metrics
- `alerts` - Health alerts and notifications
- `sessions` - Workout session data
- `nutrition_log` - Food intake tracking

---

## 🔐 Authentication

### Test Users
Since this is a demo, create a test account:
1. Tap "Sign Up" on login screen
2. Fill in registration form
3. Complete 3-step onboarding:
   - Personal info (age, gender, weight, height)
   - Health history
   - Goals setting

### Security Features
- SHA-256 password hashing
- Secure storage (flutter_secure_storage)
- Session management
- Database cascade delete on account removal

---

## 📱 Key Screens

### Authentication Flow
1. **Login Screen** - Gradient design with animated entrance
2. **Sign Up Screen** - Registration with validation
3. **Onboarding** - 3-step personalization flow

### Main App
1. **Home Dashboard** - Activity summary, live vitals, quick actions
2. **Vitals Detail** - Historical charts for HR, SpO2, temperature
3. **Daily Activity** - Steps, distance, calories, active minutes
4. **Alerts** - Health notifications with severity levels
5. **Profile** - User info, BMI, goals, settings
6. **Start Session** - Real-time workout tracking
7. **Settings** - App configuration, device pairing

---

## ⚠️ Health Alert System

### Alert Severities

**🚨 EMERGENCY (Red)**
- Heart Rate: >200 or <30 bpm
- SpO2: <80%
- **Action:** Immediate notification + "Call 911" recommendation

**⚠️ CRITICAL (Orange)**
- Heart Rate: >180 or <40 bpm
- SpO2: 80-90%
- Temperature: >39°C
- **Action:** High-priority notification + medical attention recommendation

**⚠️ WARNING (Yellow)**
- Elevated resting HR
- SpO2: 90-95%
- Mild fever: 37.5-39°C
- **Action:** Standard notification + monitoring recommendation

**ℹ️ INFO (Blue)**
- Achievement notifications
- Motivational messages
- Daily tips

---

## 🎯 Wellness Score Calculation

The app calculates a holistic wellness score (0-100) based on:
- **Sleep Quality** (25%) - Hours and patterns
- **Activity Level** (25%) - Steps, active minutes, workouts
- **Vital Signs** (25%) - HR, SpO2, temperature stability
- **Nutrition** (25%) - Calorie intake, macronutrient balance

---

## 🔗 Cloud Integration ✅

The app is fully integrated with Firebase - no backend server needed!

**Services:**
- `FirestoreService` - Direct Firestore database operations
- `FirebaseService` - Wrapper for cloud sync operations
- `AuthService` - Firebase Authentication integration

**Cloud Features:**
- ✅ Firebase Authentication for user management
- ✅ Cloud Firestore for data storage and sync
- ✅ Automatic offline support with local SQLite cache
- ✅ Real-time data synchronization
- ✅ Secure user data isolation

**Future Enhancements:**
- `analyzeFood()` - AI image recognition for nutrition (TODO)
- `getAIInsights()` - Personalized health recommendations (TODO)

**Setup:** See [FIRESTORE_SETUP.md](../docs/FIRESTORE_SETUP.md) for Firebase configuration.

---

## 📦 Package Dependencies

Core packages used:
```yaml
google_fonts: ^6.1.0           # Typography
flutter_blue_plus: ^1.30.0     # Bluetooth
sqflite: ^2.3.0                # Local database
provider: ^6.1.0               # State management
fl_chart: ^0.65.0              # Charts
flutter_local_notifications    # Alerts
flutter_secure_storage         # Secure credentials
uuid: ^4.2.0                   # Unique IDs
```

---

## 🐛 Troubleshooting

### Common Issues

**1. Build Errors**
```bash
flutter clean
flutter pub get
flutter run
```

**2. Font Not Found**
- Download required fonts and place in `fonts/` directory
- Ensure `pubspec.yaml` font paths are correct

**3. Database Errors**
- Delete app and reinstall to reset database
- Or use: `await DatabaseService().clearAllData()`

**4. Bluetooth Not Working**
- Ensure device permissions are granted
- Check if mock mode is enabled (no real device needed)
- Android: Enable location permissions (required for BLE)

---

## 📄 License

This project is developed for the IEEE CSTAM2.0 Technical Challenge.  
**For educational and competition purposes.**

---

## 👨‍💻 Developer

**CHAABEN-Chahin**  
IEEE CSTAM2.0 Technical Challenge Participant  
2025-11-15

---

## 🙏 Acknowledgments

- IEEE CSTAM2.0 Technical Challenge organizers
- Flutter community
- Open-source package contributors

---

## 📞 Support

For issues or questions:
1. Check the troubleshooting section above
2. Review code comments in service files
3. Examine mock data service for testing examples

---

## 🚀 Future Enhancements

Planned features (marked with TODO in code):
- [ ] Cloud synchronization implementation
- [ ] AI-powered food recognition
- [ ] Social features (friends, challenges)
- [ ] Apple Watch & Wear OS support
- [ ] Advanced sleep tracking
- [ ] Medication reminders
- [ ] Doctor appointment scheduling
- [ ] Export health reports (PDF)

---

**Built with ❤️ using Flutter**
