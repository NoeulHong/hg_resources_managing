# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview
Korean fitness and diet tracking web application built as a single HTML file with embedded CSS and JavaScript. Users can track daily exercise and diet records, calculate personalized calories, and manage fitness goals.

## Architecture
- **Single-page application** in `fitness-tracker.html`
- **Pure client-side**: HTML5, CSS3, JavaScript (ES6+)
- **Data persistence**: Browser localStorage with date-based keys
- **OCR integration**: Tesseract.js CDN for nutrition label scanning
- **Tab-based navigation**: 기록 (Record), 계획 (Plan), 비교 (Compare)

## Development Commands

### Server Management
```bash
# Start local development server
python3 -m http.server 8000

# Kill existing server process
lsof -ti:8000 | xargs kill -9

# Start ngrok tunnel for external access
ngrok http 8000

# Get ngrok public URL
curl -s http://localhost:4040/api/tunnels | grep -o '"public_url":"[^"]*' | head -1 | cut -d'"' -f4
```

### Testing
No automated testing framework - manual testing via browser at:
- Local: `http://localhost:8000`
- External: Via ngrok URL

## Key Features & Implementation

### Core Functionality
- **Personalized calorie calculation** using MET values and user profile (BMR/TDEE)
- **Exercise database** with 20+ exercises and metabolic equivalent values
- **Food database** with nutritional information (calories, carbs, protein, fat)
- **OCR nutrition scanning** via Tesseract.js for automatic label processing
- **Web search integration** for unknown food items
- **Encouragement system** with random motivational messages when goals are met

### Data Structure
- User profile: `userProfile` object with age, gender, height, weight, activity level
- Exercise records: `exercises_${date}` arrays with name, duration, calories, timestamp
- Food records: `foods_${date}` arrays with nutritional breakdown and meal timing
- Exercise plans: `plans_${date}` arrays for goal setting and progress tracking

### Key JavaScript Functions
- `calculatePersonalizedCalories()` - Exercise calorie calculation using MET values
- `calculateBMR()` / `calculateTDEE()` - Metabolic rate calculations (Harris-Benedict formula)
- `checkPlanCompletion()` - Detects when exercise records match plans
- `showEncouragementModal()` - Displays motivational popup messages
- OCR processing functions for nutrition label scanning

## File Structure
```
fitness-tracker.html    # Main application (all HTML/CSS/JS)
server.log             # HTTP server logs
ngrok.log             # Ngrok tunnel logs
ngrok                 # Ngrok binary
CLAUDE.md             # This file
```

## Current Status
- Fully functional fitness tracking application
- Recent addition: Encouragement popup system for goal achievement
- External access via ngrok tunnel
- Korean UI with comprehensive feature set