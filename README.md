# ESE 123 Lab 2: The Digital Multimeter (DMM)

**Interactive page:** https://cad281.github.io/ese123-lab2/

All labs: [Lab 1: DC Power & Ohm's Law](https://cad281.github.io/ese123-lab1/) · [Lab 2: Digital Multimeter](https://cad281.github.io/ese123-lab2/) · [Lab 3: SPICE & Soldering](https://cad281.github.io/ese123-lab3/) · [Lab 4: Function Generator & Scope](https://cad281.github.io/ese123-lab4/) · [Lab 5: Capacitors & Scope](https://cad281.github.io/ese123-lab5/) · [Lab 6: Operational Amplifiers](https://cad281.github.io/ese123-lab6/) · [Lab 7: Assembly Language & Buzzer](https://cad281.github.io/ese123-lab7/)

A TA-written guide for ESE 123 students. It explains **what** you do in Lab 2, **why** it matters and **how** to do each step on the bench. The interactive page animates the DMM hookups, KVL, 2-wire vs 4-wire measurement and meter loading.

---

## What this lab is about

| You will… | Using… |
|---|---|
| Measure DC voltage, DC current, resistance and continuity | Keysight 34461A 6½-digit DMM |
| Verify **Kirchhoff's voltage law** with two supplies in series | E36312A channels stacked, 300 Ω resistor |
| Measure resistors alone, in **series** and in **parallel** | 100 Ω and 200 Ω resistors |
| Compare **2-wire and 4-wire** resistance measurement | 1 Ω resistor |
| See how the meter's own **10 MΩ input** changes a circuit | Two 10 MΩ resistors on 5 V |
| Build the **voltage divider** you designed in the pre-lab | Your chosen resistors |

## Why it matters

- The DMM is the most accurate instrument you have (better than 0.0035% on DC volts). Whenever a number has to be right, you use it.
- The **voltage and current inputs are completely different**. The voltage input is ~10 MΩ (barely touches the circuit). The current input is ~1 Ω (behaves like a wire). Using the wrong one can destroy a circuit; the fuse only protects the meter.
- **KVL** and **series/parallel rules** are the basic tools for analysing every circuit in this course.
- **No meter is perfect.** Its input resistance and the test leads' resistance can change the reading. Knowing when that matters is a key engineering skill.

## How to do it, step by step

### Part 1: voltage sources in series (steps 1–11)
1. Build Figure 4: channel A set to **1 V** stacked on channel B set to **2 V**, both + up, driving a **300 Ω** resistor (orange-black-brown-gold). Outputs off for now.
2. Set **both current limits to 100 mA**. The circuit needs only 10 mA; the limit protects against wiring mistakes.
3. On the 34461A press **DCV**. Leads in **Input VΩ HI** (red) and **LO** (black).
4. HI to the resistor end connected to the 1 V supply's +, LO to the end connected to the 2 V supply's −. Enable outputs. **Expect ≈ 3.000 V.**
5. **Swap the leads.** Expect ≈ **−3.000 V** (same voltage, opposite reference).
6. Outputs off. Move the red lead to the **I** input (lower right). **Break the circuit** and insert the meter: I toward the 1 V supply's +, LO toward the resistor. Press **Shift → DCI** and check the display shows µADC/mADC.
7. Outputs on. **Expect ≈ 10 mA.** Outputs off, take it apart.

### Part 2: continuity (steps 12–13)
Leads back in VΩ/LO, press **Cont**, touch the probes together: it beeps. Use this to check wires and solder joints for the rest of the semester.

### Part 3: resistance (steps 14–23)
1. **Ω2W**: measure 100 Ω, 200 Ω, then the two in **series** (≈ 300 Ω) and in **parallel** (≈ 66.7 Ω).
2. Hold one bare lead in each hand: **your body resistance** (typically hundreds of kΩ to a few MΩ; a firmer grip lowers it).
3. Measure a **10 MΩ** resistor with clips, without touching. Then hold both ends: the reading **drops**, because your body is now in parallel with it.
4. Measure the **1 Ω** resistor in 2-wire mode (reads high, ~1.1 Ω), then add the two **Sense Ω4W** leads to the same resistor legs and press **Shift → Ω4W** (reads ≈ 1.00 Ω).

### Part 4: powered circuits (steps 24–26)
1. Two 10 MΩ in series across 5 V. Try measuring one with **Ω2W while powered**, then swap the leads. The readings are nonsense and change with lead order.
2. Switch to **DCV**. Measure V_S and the voltage across each resistor. **Expect ≈ 1.67 V each, not 2.5 V**, and they don't add up to 5 V.

### Part 5: voltage divider (step 27)
Build your pre-lab divider and measure V_out. If a value isn't available, combine two resistors in series or parallel.

## What you should observe, and why

| Observation | Why it happens |
|---|---|
| 3.000 V, then −3.000 V when leads swap | The DMM displays V(HI) − V(LO). |
| ≈ 10 mA in series | I = 3 V / 300 Ω. The meter's ~1 Ω barely changes it. |
| Parallel R is smaller than either resistor | Two paths share the current, so it's easier for current to flow. |
| 10 MΩ reads lower when you hold it | Your body (~0.2–3 MΩ) is in parallel with it. |
| 1 Ω reads ~1.1 Ω in 2-wire, ~1.00 Ω in 4-wire | 2-wire includes both leads' resistance; 4-wire senses voltage right at the part with leads carrying ~0 A. |
| Ω readings in a powered circuit are garbage | The ohmmeter assumes the only voltage present comes from its own test current. |
| 1.67 V + 1.67 V ≠ 5 V | The meter's 10 MΩ in parallel with a 10 MΩ resistor makes 5 MΩ, changing the divider during each reading. |

## Formula sheet (what, when, example)

### Kirchhoff’s voltage law (KVL)

```
Σ V around any closed loop = 0
```

**Use it when:** Finding an unknown voltage in a loop: add rises (− to + through a source), subtract drops (+ to − across a resistor carrying current).

- `Σ V`: sum of voltages, with signs, going once around

**Example:** Figure 4: +1 V + 2 V − Vout = 0 → Vout = 3 V.

### Sources in series

```
Vtotal = V1 + V2  (same orientation)
Vtotal = V1 − V2  (opposing)
```

**Use it when:** Stacking power supply channels to get a bigger voltage.

**Example:** 1 V on top of 2 V, both + up → 3 V.

### Ohm’s law

```
I = V / R
```

**Use it when:** Predicting the current the ammeter should read.

**Example:** 3 V / 300 Ω = 10 mA.

### Tolerance → current range

```
Imin = V / Rmax,  Imax = V / Rmin
```

**Use it when:** Checking if a measured current is plausible given a ±5% resistor.

**Example:** 300 Ω ±5% = 285–315 Ω → 9.52–10.53 mA at 3 V.

### Series resistors

```
Rs = Ra + Rb + …
```

**Use it when:** Parts connected end to end with one path for current. Use measured values for the best prediction.

**Example:** 99.6 Ω + 200.9 Ω = 300.5 Ω.

### Parallel resistors

```
Rp = RaRb / (Ra + Rb)
1/Rp = 1/Ra + 1/Rb + …
```

**Use it when:** Parts connected across the same two nodes. The result is always smaller than the smallest resistor.

**Example:** 100 Ω ∥ 200 Ω = 20000/300 = 66.7 Ω.

### Power absorbed by a meter

```
P = V² / Rin
```

**Use it when:** Seeing why the voltage input is safe and the current input across a source is not.

- `Rin`: 10 MΩ for the voltage input, ~1 Ω for the current input

**Example:** 25 V: 25²/10⁷ = 63 µW (safe) vs 25²/1 = 625 W (fuse blows).

### 2-wire resistance reading

```
Rread = R + 2Rwire
```

**Use it when:** Understanding why small resistors read high in Ω2W mode.

**Example:** 1 Ω + 2 × 0.06 Ω = 1.12 Ω (12% high).

### Lead resistance from 2W and 4W

```
Rwire = (R2W − R4W) / 2
```

**Use it when:** Question 11: the 4-wire reading removes the leads, so the difference is the two leads.

**Example:** (1.118 − 1.002)/2 = 0.058 Ω per lead.

### Voltage divider

```
Vout = Vin · Rbottom / (Rtop + Rbottom)
```

**Use it when:** Designing or checking a divider, and seeing how a meter’s Rin in parallel with Rbottom lowers the reading.

**Example:** 5 V, two 10 MΩ: 2.5 V ideal; with the 10 MΩ meter across one: 5 × 5M/15M = 1.667 V.

### Designing Rtop

```
Rtop = Rbottom · (Vin − Vout) / Vout
```

**Use it when:** Pre-lab divider design: pick Rbottom, compute Rtop, round to the nearest standard value.

**Example:** 5 V → 3.3 V with 10 kΩ bottom: 5.15 kΩ → use 5.1 kΩ (gives 3.31 V).

### Percent difference / error

```
(measured − expected) / expected × 100%
```

**Use it when:** Every comparison question in the report.

**Example:** Measured 2.998 V vs 3 V → −0.07%.


## Practice questions

Same concepts and formulas as the Brightspace quiz, with new numbers (not the real quiz questions). Try each one before opening the answer.

**Q1.** Find the series and parallel resistance of 150 Ω and 330 Ω.

<details><summary>Show answer</summary>

**480 Ω and 103 Ω**. Series: 150 + 330 = 480 Ω. Parallel: 150 × 330 / 480 = 103.1 Ω (smaller than 150 Ω, as it must be).

</details>

**Q2.** Find the equivalent of 1 kΩ, 2.2 kΩ and 4.7 kΩ all in parallel.

<details><summary>Show answer</summary>

**≈ 600 Ω**. 1/R = 1/1000 + 1/2200 + 1/4700 = 0.001 + 0.000455 + 0.000213 = 0.001667 S → R = 600 Ω.

</details>

**Q3.** A 5 V and a 2 V source are in series but opposing (+ to +) across a 1 kΩ resistor. Find the resistor voltage and current.

<details><summary>Show answer</summary>

**3 V, 3 mA**. Opposing sources subtract: 5 − 2 = 3 V. I = 3 V / 1 kΩ = 3 mA.

</details>

**Q4.** A 9 V source drives R1 and R2 in series. R1 drops 4.2 V. What is across R2? What does the DMM show if HI is on the bottom of R2 and LO on the top?

<details><summary>Show answer</summary>

**4.8 V, then −4.8 V**. KVL: 9 − 4.2 − VR2 = 0 → VR2 = 4.8 V. Swapping HI/LO flips the sign: −4.8 V.

</details>

**Q5.** A 12 V supply drives a 330 Ω ±5% resistor. What current range should you expect?

<details><summary>Show answer</summary>

**34.6 mA to 38.3 mA**. R ranges 313.5–346.5 Ω. Imin = 12/346.5 = 34.6 mA, Imax = 12/313.5 = 38.3 mA.

</details>

**Q6.** A divider has Rtop = 6.8 kΩ and Rbottom = 3.3 kΩ on 9 V. Find Vout.

<details><summary>Show answer</summary>

**2.94 V**. Vout = 9 × 3.3/(6.8 + 3.3) = 9 × 0.3267 = 2.94 V.

</details>

**Q7.** Design a divider from 12 V to 5 V with Rbottom = 10 kΩ. What Rtop, and which standard value would you use?

<details><summary>Show answer</summary>

**14 kΩ exact; 15 kΩ → 4.80 V or 13 kΩ → 5.22 V**. Rtop = Rb(Vin − Vout)/Vout = 10k × 7/5 = 14 kΩ. Not an E24 value, so pick 15 kΩ or 13 kΩ, or put two resistors in series (e.g. 12k + 2k).

</details>

**Q8.** The 2-wire reading of a small resistor is 2.236 Ω and the 4-wire reading is 2.118 Ω. What is the resistance of one test lead?

<details><summary>Show answer</summary>

**0.059 Ω**. Two leads = 2.236 − 2.118 = 0.118 Ω, so one lead = 0.059 Ω.

</details>

**Q9.** Two 1 MΩ resistors in series on 10 V. A DMM with 10 MΩ input is put across the bottom one. What does it read?

<details><summary>Show answer</summary>

**4.76 V (not 5 V)**. Bottom becomes 1M ∥ 10M = 0.909 MΩ. V = 10 × 0.909/(1 + 0.909) = 4.76 V. The error is smaller than with 10 MΩ resistors because 1 MΩ ≪ 10 MΩ.

</details>


## Report guide

1. KVL for Figure 4: +1 + 2 − V_out = 0 → V_out = 3 V.
2. % error vs your step-7 reading.
3. Redraw Figure 4 with V_out's polarity as measured in step 8.
4. Current range with ±5%: 3/315 to 3/285 A. Is your step-10 value inside?
5. Expected series R from measured parts; % difference vs step 17.
6. Expected parallel R from measured parts.
7. V = 10 mA × body resistance (a big number; skin breaks down earlier, and never touch > 42 V).
8. Difference between steps 20 and 21 and what caused it.
9–10. % difference of the 1 Ω readings (2-wire, 4-wire) vs nominal.
11. Lead resistance = (2W − 4W)/2.
12. Were powered Ω readings believable? Why not?
13. KVL with V_S, V_R1, V_R2 and the role of the meter's 10 MΩ.
14. Divider schematic with values, target and measured V_out.

---
*Made for ESE 123 students by a TA. Simulated values are typical; your bench readings will differ slightly.*
