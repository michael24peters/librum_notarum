---
tags:
  - fleeting
created: 2024-09-26 13:16
date: 2024-09-26
moc:
  - "[[Codex hardware]]"
  - "[[FEB issues]]"
  - "[[Codex documentation]]"
---
# 202409261316 resolving feb issues

You need to press down on the FEB for each channel and observe the signal on an oscilloscope. It may also help to add a 100 ohm resistance to the pin connector piece. This makes a signal much more prominent so you can diagnose if there is an issue or not.

In the case of m10, phi1, FEB 1, the issue was there was a huge gap between the FEB and the panel. If you press down on the middle, the channels appear alive again. This means that the grounds were not connected, and a short on one ground can cause issues across multiple channels, making it *appear* as if a whole FEB is dead. Removing the entire FEB, cleaning up the solder, and reapplying the FEB again resolved all issues.

As for things to check, you need to make sure that on the RPC itself that you get the following voltages for low voltage:

- V_th: > 1.7 V
- V_amp: 1.3 V
- V_pu: 0.4 V
- V_lvds: 2.4 V
- V_dis: 2.5 V

If one is off by 50 mV, no problem; if one is off by 100 mV, it *may* be an issue; if one is off by 200+ mV, it is definitely an issue.

In the case of m10, it was off by 300 mV. That is indicative of a problem.

In addition to the shorting issue, the LVDS and discriminator voltages needed to be raised to 2.7 V on the power supply in order to provide 2.4 and 2.5 V to the triplet, respectively.

Also keep in mind that, when debugging, you need to change these voltages if you disconnect other singlets. These values only work for a whole triplet plugged in. Draw out the circuit diagram and you'll see why: removing two resistances from a parallel circuit increases the voltage to the remaining line (according to Luca).

**Current check:** For LVDS, you expect a current of around 1.2 A. Maybe it's not exactly this, but you should know what to expect. If you see a current of 1.1 A, this isn't ideal but it's fine; if you see 0.8 A, there is a problem.

---
# References


