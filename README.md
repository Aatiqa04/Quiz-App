# Quiz-App

A simple Android quiz application written in Java that presents 30 multiple-choice general-knowledge questions with a 3-minute countdown timer and live scoring.

## Features

- 30 multiple-choice questions covering general knowledge (geography, science, history, literature, etc.)
- Single-select answers via a `RadioGroup` of four options per question
- Live score display
  - Correct answer: **+5 points**
  - Wrong answer: **-1 point**
  - Reveal correct answer: **-1 point** (and auto-selects the right option)
- 3-minute countdown timer that auto-ends the exam when it reaches zero
- Navigation between questions with **Next** and **Previous** buttons
- **End Exam** button to submit early
- Final summary screen showing total score and percentage

## Tech Stack

- **Language:** Java
- **Platform:** Android (`compileSdk` 34, `minSdk` 24, `targetSdk` 34)
- **Build system:** Gradle (Kotlin DSL) with version catalogs (`libs.versions.toml`)
- **Libraries:** AndroidX AppCompat, Material Components, Activity, ConstraintLayout

## Project Structure

```
Quiz-App/
├── app/
│   ├── build.gradle.kts
│   └── src/
│       └── main/
│           ├── AndroidManifest.xml
│           ├── java/com/example/quizapp/MainActivity.java
│           └── res/                  # layouts, drawables, values
├── build.gradle.kts
├── settings.gradle.kts
└── gradle/
```

The core logic lives in `app/src/main/java/com/example/quizapp/MainActivity.java`, which holds the question bank, answer options, correct-answer indices, and the scoring/timer logic.

## Getting Started

### Prerequisites

- Android Studio (Hedgehog or newer recommended)
- JDK 8+
- Android SDK 34

### Build & Run

1. Clone the repository:
   ```bash
   git clone <repo-url>
   cd Quiz-App
   ```
2. Open the project in Android Studio and let Gradle sync.
3. Connect a device or start an emulator (API 24+).
4. Click **Run**, or build from the command line:
   ```bash
   ./gradlew assembleDebug        # macOS/Linux
   gradlew.bat assembleDebug      # Windows
   ```
5. Install the resulting APK from `app/build/outputs/apk/debug/`.

## How It Works

- `MainActivity` initializes the UI, loads the first question, and starts a `CountDownTimer` of 180,000 ms.
- Tapping **Next** calls `checkAnswer()` to update the score, then advances to the next question (or ends the exam on the last one).
- Tapping **Previous** moves back without re-scoring.
- Tapping **Show Answer** highlights the correct option and deducts one point.
- When the timer expires or the user taps **End Exam**, all controls are disabled and the final score and percentage are displayed.

## Scoring

| Action              | Score change |
| ------------------- | ------------ |
| Correct answer      | +5           |
| Wrong answer        | -1           |
| Show correct answer | -1           |

Final percentage is calculated as `(totalScore / (numQuestions * 5)) * 100`.
