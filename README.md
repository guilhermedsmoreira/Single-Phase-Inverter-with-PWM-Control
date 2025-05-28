# ⚡ Single-Phase Inverter with PWM Control
[🔧 Under Load – Handle with Care!]

This project continues the previous study on single-phase inverters. Here, the same H-bridge circuit is analyzed with the addition of Pulse Width Modulation (PWM) control.

---

## 🔧 Circuit Components

The circuit includes:

4 N-channel MOSFETs

A 5 V DC power supply

A 10 kΩ resistive load

PWM control voltage sources

Buffers and operational amplifiers

![Circuito completo]()

---

## 📈 Load Waveform

The simulation was carried out in LTspice. Below, you can see the voltage and current waveforms across the resistive load:

![Forma de onda da carga]()
![Forma de onda da carga]()


Since the load is purely resistive, the voltage and current waveforms have the same shape.

In the previous version (without PWM control), the RMS voltage across the load was approximately 5 V, as expected given the 5 V DC source and direct MOSFET switching.

With the addition of Pulse Width Modulation (PWM) control, the output voltage waveform is no longer constant but composed of periodic pulses. This reduces the average energy delivered to the load, which results in a lower RMS voltage.

In this simulation, the measured RMS voltage across the load is about 4.07 V. This reduction occurs because part of the PWM cycle is spent at low voltage, which decreases the total energy delivered over time.

This behavior is expected and directly tied to the duty cycle of the PWM signal. The shorter the on-time (Ton), the lower the RMS voltage across the load.

In other words, the drop in Vrms is a natural and controlled result of PWM — a key technique for regulating power delivered to the load without changing the DC source voltage.
---

## 🎛️ PWM Control

To implement PWM control in the inverter, we used:

2 comparators

3 voltage sources: Vp1, Vp2, and Vc

Vp1 and Vp2 are the carrier signals (sawtooth), with Vp2 being the inverted version of Vp1

Vc is the control voltage (set at 10 V)

The comparator switches its output high whenever Vc exceeds the instantaneous value of Vp1 or Vp2.

This comparison process is what generates the PWM pulses used to drive the MOSFETs.

---

## 🔁 Inverting Op-Amp (Unity Gain)

To ensure Vp1 and Vp2 have the same RMS value, an inverting operational amplifier with unity gain was used.

Resistors used: R1 = R2 = 10 kΩ

Result: the waveform is inverted without any change in magnitude

![Amp Op inversor]()

---

## ⚖️ Comparator with Op-Amp

PWM generation is based on comparing Vc with the carriers Vp1 and Vp2 using op-amp comparators.

When Vc > Vp1 → comparator output is HIGH

When Vc < Vp1 → comparator output is LOW

The same logic applies to Vp2

This is the fundamental process behind PWM pulse generation for switching the MOSFETs.

![Ondas Vp1, Vp2, Vc]()

---

## 🧱 Buffer Stage

A voltage follower (buffer) was added at the comparator output to ensure proper signal isolation and integrity before reaching the MOSFET gates.

The buffer serves to:

Prevent the control circuit from being affected by the MOSFET gate load

Preserve the PWM signal shape

Provide high input impedance and low output impedance, ensuring efficient coupling between stages

Using a buffer guarantees that PWM signals arrive at the transistors cleanly and without distortion.


## 📌 Key Takeaways

PWM allows control over the RMS voltage across the load by varying the MOSFET conduction time

A higher duty cycle leads to a higher RMS voltage

The circuit was simulated in LTspice using a 50 Hz switching frequency






