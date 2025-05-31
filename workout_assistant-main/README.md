# AI-Based Workout Assistant and Fitness Guide

**Table of Contents**  
- [Project Overview](#project-overview)  
- [Features](#features)  
- [Architecture & Technologies](#architecture--technologies)  
  - [Frontend](#frontend)  
  - [AI / Computer Vision](#ai--computer-vision)  
  - [Backend (Optional)](#backend-optional)  
- [Getting Started](#getting-started)  
  - [Prerequisites](#prerequisites)  
  - [Installation](#installation)  
  - [Running Locally](#running-locally)  
- [Usage](#usage)  
  - [Real-Time Pose Detection](#real-time-pose-detection)  
  - [Repetition Counting & Corrective Feedback](#repetition-counting--corrective-feedback)  
  - [Personalized Workout & Diet Plans](#personalized-workout--diet-plans)  
  - [Progress Tracking](#progress-tracking)  
- [Project Structure](#project-structure)  
- [Contributing](#contributing)  
- [Future Enhancements](#future-enhancements)  
- [Acknowledgments](#acknowledgments)  
- [License](#license)  
- [Contact](#contact)

---

## Project Overview

Fitness and health are essential to leading a balanced life, yet too many people lack affordable, personalized guidance for effective workouts and progress tracking. Traditional fitness solutions often require expensive gym memberships or personal trainers—barriers that can be prohibitive for students, remote workers, and beginners.

**AI-Based Workout Assistant and Fitness Guide** is a browser-based platform that democratizes expert‐level fitness coaching by leveraging:

- **Computer Vision & Pose Estimation** (MediaPipe BlazePose) to detect user posture in real time.  
- **Joint‐Angle Analysis** for accurate repetition counting and form validation.  
- **Instant Corrective Feedback** to prevent injury and maximize workout effectiveness.  
- **Lightweight AI Inference (TensorFlow.js)** for generating personalized workout and diet plans based on individual goals (e.g., weight loss, muscle gain, flexibility).  
- **On-Device Model Execution** entirely inside the browser—no heavy server infrastructure required.  
- **Motivational Progress Charts & Achievement Badges** to foster long-term adherence.

By combining accurate, on-device pose tracking with dynamic nutritional recommendations and progress visualization, the platform significantly lowers the cost barrier to high-quality fitness coaching. Its modular architecture allows you to extend functionality seamlessly (e.g., yoga pose correction, heart-rate integration, AI chat coaching). Ultimately, the AI-Based Workout Assistant empowers users to exercise safely, stay motivated, and achieve their health goals in a fully accessible, affordable way.

---

## Features

1. **Real-Time Pose Detection**  
   - Uses MediaPipe BlazePose under the hood to track 33 key landmarks on the body.  
   - Displays an overlay of keypoints and skeleton on top of the live webcam feed.

2. **Repetition Counting & Form Validation**  
   - Joint-angle analysis (e.g., knee angle for squats, elbow angle for push-ups) determines when a repetition is completed.  
   - On-screen counter shows reps in real time.  
   - Color-coded feedback (green/red) indicates whether your form is correct or needs adjustment.

3. **Instant Corrective Feedback**  
   - Uses simple heuristics (e.g., “Keep your back straight” or “Lower down more”) to help prevent common mistakes.  
   - Visually highlights which joints or body parts are misaligned.

4. **Personalized Workout Plans**  
   - Users choose a fitness goal (e.g., weight loss, muscle gain, flexibility).  
   - Lightweight AI model (running in the browser via TensorFlow.js) generates a tailored set of exercises (e.g., number of sets, reps, rest times).

5. **Dietary Recommendations**  
   - Based on user’s age, weight, height, and fitness goal, the AI suggests calorie and macronutrient targets.  
   - Example: “Consume 1,800 kcal/day with 40% proteins, 30% carbs, 30% fats for muscle gain.”

6. **Progress Tracking & Motivation**  
   - Displays a weekly/monthly chart of total calories burned, total reps completed, etc.  
   - Unlockable badges (e.g., “First 50 Push-Ups,” “7-Day Workout Streak”) encourage consistency.

7. **Modular & Extensible**  
   - Clear separation between the **`/pose-estimation`** module (real-time webcam + BlazePose) and the **`/ai-recommendations`** module (TensorFlow.js inference).  
   - Easily integrate new features like heart-rate monitoring (via Web Bluetooth API), yoga pose correction, or an AI-powered chat coach.

---

## Architecture & Technologies

### Frontend
- **HTML / CSS / JavaScript**  
  ­– Core web technologies to build the user interface.  
- **MediaPipe BlazePose** (via WebAssembly or JS)  
  ­– Performs landmark detection at ~30 fps in modern browsers.  
- **TensorFlow.js**  
  ­– Runs small neural networks (for workout plan and diet plan inference) directly inside the browser.  
- **Chart.js** (or similar)  
  ­– For rendering progress charts (calories burned, reps, workout streak).  
- **Bootstrap / Tailwind CSS (optional)**  
  ­– For responsive layout and styling.  
- **Web APIs**  
  ­– Webcam access (`getUserMedia`), Local Storage (to cache user profile & progress), and possibly IndexedDB (for storing larger logs).

### AI / Computer Vision
- **MediaPipe BlazePose**  
  ­– High-fidelity, lightweight pose‐estimation model that provides 33 3D landmarks.  
- **Pose-Based Repetition Counting Logic**  
  ­– Custom JavaScript code that computes joint angles (e.g., angle between hip‐knee‐ankle for squats).  
  ­– Thresholds detect “down” and “up” positions to count a completed rep.  
- **Corrective Feedback Rules**  
  ­– If joint angle exceeds/falls below safe thresholds, display a warning (e.g., “Knees shouldn’t extend beyond toes”).  
- **TensorFlow.js Models**  
  ­– A small feedforward network or pretrained “mobile” model that takes user inputs (age, weight, height, goal) and outputs a structured workout plan or macronutrient breakdown.

### Backend (Optional)
> **Note:** The core MVP runs *entirely* in the browser. If you choose to add user accounts or persist data server-side, a minimal backend might include:
- **Node.js + Express.js** (or Python Flask / Django)  
  ­– REST endpoints for saving user profiles, workout logs, and retrieving historical progress.  
- **MongoDB** (or PostgreSQL)  
  ­– Stores user info, workout history, and any additional metadata.  
- **Authentication**  
  ­– JWT or session-based login if you want multi-device syncing.  

---

## Getting Started

Follow these steps to get a local copy of the project up and running on your machine.

### Prerequisites

1. **Node.js & npm** (if you plan to run a local web server or install JS dependencies)  
   - Download and install: https://nodejs.org/  
   - Verify in terminal/command prompt:
     ```bash
     node -v
     npm -v
     ```

2. **Web Browser**  
   - A modern browser (Chrome, Firefox, Edge) with WebGL & WebAssembly support.  
   - Ensure you have a working webcam (built-in or USB).

3. **Git** (for cloning/forking the repo)  
   - If you haven’t already installed Git: https://git-scm.com/downloads  

### Installation

1. **Clone the repository**  
   ```bash
   git clone https://github.com/MurtazaPlumber68/AI-Workout-Assistant.git
   cd AI-Workout-Assistant
