# Auto Harmonic Patterns — MQL4 Script

A MetaTrader 4 script that automatically detects **Gartley, Bat, Butterfly, and Crab** harmonic chart patterns using Fibonacci ratio analysis on pivot points, and fires alerts when a valid pattern is identified.

---

## Overview

Harmonic patterns are price structures defined by precise Fibonacci retracement and extension ratios between five pivot points (X, A, B, C, D). This script scans the most recent bars for pivot highs and lows, extracts the five key points, computes the AB/XA, BC/AB, and CD/XA ratios, and matches them against the known ratio targets for each pattern type within a configurable tolerance.

---

## Features

- **Four pattern types:** Gartley, Bat, Butterfly, and Crab
- **Fibonacci ratio matching** — AB/XA, BC/AB, and CD/XA computed and validated against each pattern's canonical ratios
- **Pivot point detection** — `IsPivotHigh()` / `IsPivotLow()` compare each bar against its immediate neighbors
- **Configurable tolerance** — allows ±`Tolerance` deviation from ideal ratios
- **Three notification channels:** sound alert, email, and mobile push
- **Lightweight loop** — polls once per minute (`Sleep(60000)`)
- Logs detected patterns and all five point values to the MT4 **Experts** tab

---

## How It Works

1. Every minute, `DetectHarmonicPattern()` calls `FindPivotPoints()` to scan `LookbackBars` bars for the five most recent alternating pivot highs/lows
2. From the five points, three ratios are computed: `AB/XA`, `BC/AB`, `CD/XA`
3. `CheckPattern()` compares each ratio against the canonical Fibonacci targets for all four pattern types within `±Tolerance`:

| Pattern   | AB/XA | BC/AB | CD/XA |
|-----------|-------|-------|-------|
| Gartley   | 0.618 | 0.618 | 1.618 |
| Bat       | 0.500 | 0.382 | 1.618 |
| Butterfly | 0.786 | 0.618 | 1.270 |
| Crab      | 0.382 | 0.618 | 2.240 |

4. On a match, `AlertHarmonic()` fires all enabled notification channels with the pattern name, symbol, timeframe, and all five point values

---

## Input Parameters

| Parameter      | Type            | Default     | Description                                        |
|----------------|-----------------|-------------|----------------------------------------------------|
| `TradeSymbol`  | string          | `EURUSD`    | Symbol for analysis                                |
| `Timeframe`    | ENUM_TIMEFRAMES | `PERIOD_H1` | Timeframe for pattern detection                    |
| `LookbackBars` | int             | `300`       | Number of bars to scan for pivot points            |
| `Tolerance`    | double          | `0.05`      | Allowable deviation from ideal Fibonacci ratios    |
| `EnableAlerts` | bool            | `true`      | Fire an on-screen/sound alert                      |
| `EnableEmail`  | bool            | `false`     | Send an email notification                         |
| `EnablePush`   | bool            | `false`     | Send a mobile push notification                    |

---

## Alert Message Format

```
Gartley Pattern detected on EURUSD (Timeframe: PERIOD_H1)
Points: [1.08100, 1.08520, 1.08310, 1.08640, 1.08190]
```

---

## Installation

1. Copy `Auto_Harmonic_Patterns_001.mq4` to `MQL4/Scripts/` in your MT4 data folder
2. Compile in MetaEditor (F7)
3. Drag onto any chart from Navigator → Scripts
4. Configure inputs and click **OK**

---

## Requirements

- MetaTrader 4 (`#property strict` compatible build)
- MQL4 compiler (MetaEditor)

---

## License

MIT License

Copyright (c) 2026

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
