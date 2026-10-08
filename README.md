# 🎸 Voron Belt Tuner

A lightweight, browser-based calibration tool to measure and tune the belt tension of your Voron (and other CoreXY) 3D printers. It uses your device's microphone and the Web Audio API to detect the fundamental frequency of a plucked belt, functioning like a digital guitar tuner specifically designed for 3D printer kinematics.

Hosted entirely on **GitHub Pages**, it requires no backend, no installation, and works directly on your mobile phone's browser with a sticky, mobile-first UI.

**→ [Open the app](https://dnshlpmn.github.io/Voron-Belt-Tuner/)**

![Voron Belt Tuner Preview](https://img.shields.io/badge/Voron-2.4-red)
![License](https://img.shields.io/badge/license-GPL--3.0-blue)
![No install](https://img.shields.io/badge/no%20install-required-green)

---

![App Screenshot](app.png)

---

## ✨ Key Features

- **Harmonic Rejection Algorithm**: Automatically detects and corrects 2nd/3rd harmonics, ensuring you are measuring the true fundamental frequency of the belt.
- **Pluck Detection Filter**: Uses an RMS amplitude threshold to ignore background noise and only register a reading when the belt is actually plucked.
- **Live Updates**: Values update instantly on every pluck—no waiting for stability timers.
- **Belt Spread Analysis**: Compares all measured belts (e.g., Z0-Z3) and calculates the Hz spread to tell you if your belts are balanced (✓ BALANCED) or need adjustment (✗ RE-TENSION).
- **Custom Configuration**: Fully customizable Target Hz, Range Min/Max, and Gauge Min/Max for non-Voron printers or custom setups.
- **Mobile-Optimized UI**: Sticky bottom action button, real-time signal strength indicator, and live spectrum analyzer.

## ⚠️ Crucial: The 150mm Pluck Length

The official Voron documentation specifies that the target frequencies are based on plucking exactly a **150mm section** of the belt. Because the frequency of a vibrating string depends on its length, **if you pluck a longer or shorter section, these target values will not apply!**

- **For A/B Belts:** Move your X extrusion forwards until the X/Y idler centers are **150mm** from the front idler centers.
- **For Z Belts:** Move the gantry upwards until the fixed side of the belt is **150mm** from the Z idler centers.

## 🎯 Official Voron Tension Targets

Based on the [official Voron documentation](https://docs.vorondesign.com/tuning/secondary_printer_tuning.html), the recommended tension frequencies are:

| Belt Type | Target Frequency | Acceptable Range |
| :--- | :---: | :---: |
| **Z Belts (Z0-Z3)** | 140 Hz | 130 - 150 Hz |
| **A/B Belts (CoreXY)** | 110 Hz | 100 - 120 Hz |

*Note: Proper tension ensures dimensional accuracy, prevents ghosting/skipped steps, and reduces wear on the printer's kinematics.*

## 🚀 How to Use

1. **Select Belt Type**: Tap the **Z Belts**, **A/B Belts**, or **Custom** tab at the top.
2. **Select Channel**: Tap the specific belt you are measuring (e.g., Z0, Z1, A, B).
3. **Position the Belt**: Move your gantry/extruder so the free span of the belt you are about to pluck is exactly **150mm** long.
4. **Start Measuring**: Tap the sticky **◎ MEASURE** button at the bottom of the screen and allow microphone access.
5. **Pluck the Belt**: Firmly pluck the 150mm section of the belt with your fingernail. 
   - *Watch the **Signal Indicator** bars above the frequency display to ensure your pluck is strong enough to pass the filter.*
6. **Live Feedback**: The main display, channel badges, and comparison chart will update instantly on every pluck.
7. **Check Spread**: After measuring all belts, check the **SPREAD** value in the Comparison section to ensure they are balanced.

## 🛠️ Technical Details

- **Pitch Detection**: Uses the `Web Audio API` (`AnalyserNode`) combined with a time-domain **autocorrelation algorithm** and parabolic interpolation.
- **Harmonic Rejection**: Calculates the ratio of the detected frequency to the target frequency. If it closely matches an integer multiple (e.g., 3.0x), it divides the frequency to find the true fundamental.
- **Pluck Filter**: Calculates the Root Mean Square (RMS) of the audio buffer. Pitch detection is only processed if the RMS exceeds the `PLUCK_THRESHOLD` constant.
- **Deployment**: Static HTML/JS/CSS, deployable to any static host (GitHub Pages, Cloudflare Pages, Netlify, Vercel).

## ⚠️ Disclaimer

This tool is provided as-is for community convenience. Always double-check your belt tension using the official manufacturer guidelines. The creator is not responsible for any hardware damage resulting from over-tensioning or under-tensioning.

## 🙌 Credits & Inspiration

- **Voron Design**: For the amazing open-source 3D printer ecosystem and official tuning documentation.
- **Web Audio API Community**: For the foundational pitch-detection algorithms (inspired by Chris Wilson's [Pitch Detect](https://github.com/cwilso/PitchDetect)).

---
*Made with ❤️ for the 3D Printing Community.*
