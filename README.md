# OVERCLOCK PRO — QA & Scenario Validation Report
**Tested By:** Member 4 (Testing & Quality Assurance Engineer)  
**Test Environment:** Browser Client Engine (`index.html`)

---

## Test Matrix & Guardrail Verification

| Test ID | Scenario Name | Input Parameters | Expected Architectural Behavior | Actual Result | Status |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-01** | **Factory Stock Baseline** | BCLK: `100 MHz`<br>Multiplier: `36x`<br>VCore: `1.20 V`<br>Cooler: Stock Air (`0.18 °C/W`) | Clock = `3.60 GHz`<br>Power = `62.2 W`<br>Temp = `36.2 °C`<br>Badge = `SYSTEM STABLE` | Clock = `3.60 GHz`<br>Power = `62.2 W`<br>Temp = `36.2 °C`<br>Badge = `SYSTEM STABLE` | **PASS** |
| **TC-02** | **Under-Volting Setup-Time Violation** | BCLK: `100 MHz`<br>Multiplier: `50x` (`5.00 GHz`)<br>VCore: `1.20 V` (Below `V_min`) | Logic gate propagation delay exceeds clock period $\rightarrow$ triggers `CRASH: UNDER-VOLTED (BSOD)` alert | BSOD alert triggered accurately when $V < V_{\text{min}}$ | **PASS** |
| **TC-03** | **Thermal Throttling Protection** | BCLK: `110 MHz`<br>Multiplier: `50x`<br>VCore: `1.55 V`<br>Cooler: Stock Air (`0.18 °C/W`) | $T_j \ge 95.0^\circ\text{C}$ triggers automatic $25\%$ frequency downclock and `THERMAL THROTTLING ACTIVE` warning | Throttled frequency by $25\%$ at $95.0^\circ\text{C}$ ceiling | **PASS** |
| **TC-04** | **Liquid Cooling Efficiency** | BCLK: `105 MHz`<br>Multiplier: `48x` (`5.04 GHz`)<br>VCore: `1.42 V`<br>Cooler: 240mm AIO (`0.04 °C/W`) | Reduced $R_{\text{th}}$ keeps $T_j$ well below $95.0^\circ\text{C}$ under heavy load | Temp stabilized around `30°C–35°C`; zero throttling | **PASS** |
| **TC-05** | **Reset to Stock Baseline** | Click `Reset to Stock Baseline` from an extreme overclocked state | All sliders, dropdowns, telemetry cards, and chart axes reset cleanly to TC-01 defaults | Restored all parameters with zero state leakage | **PASS** |
