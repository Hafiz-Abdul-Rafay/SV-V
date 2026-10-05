# Task 2 — Formalize Constraints

## Notation

| Symbol | Meaning |
|--------|---------|
| ∧ | AND |
| ∨ | OR |
| ¬ | NOT |
| → | implies / if-then |

## Propositions

| Symbol | Meaning |
|--------|---------|
| `Train_Present` | Train is inside the crossing |
| `Train_Approaching` | Train detected approaching |
| `Barrier_Open` | Barrier fully open |
| `Barrier_Closed` | Barrier fully closed |
| `Barrier_Lowering` | Barrier has started to lower |
| `Barrier_Opening` | Barrier has started to open |
| `Warning_Active` | Lights and alarm are on |
| `Signal_Red` | Road traffic signal is red |
| `Clear_Confirmed` | System confirmed the train has fully cleared |
| `Sensor_Fault` | Train-detection sensor failed |
| `Barrier_Fault` | Barrier mechanism failed |
| `Comm_Loss` | Communication lost |
| `Emergency` | Emergency condition active |
| `Sensor_Conflict` | Sensor readings disagree |
| `Failsafe_Mode` | Barrier closed, warning on, signal red |
| `Control_Alert` | Alert sent to control center |

## Formal Constraints

| ID  | Formal Expression |
|-----|-------------------|
| C1  | `Train_Present → ¬Barrier_Open` |
| C2  | `Train_Approaching → Warning_Active` |
| C3  | `Barrier_Lowering → Warning_Active` |
| C4  | `Barrier_Opening → Clear_Confirmed` |
| C5  | `(Train_Approaching ∨ Train_Present) → Signal_Red` |
| C6  | `Sensor_Fault → Failsafe_Mode` |
| C7  | `Barrier_Fault → Control_Alert` |
| C8  | `Comm_Loss → Failsafe_Mode` |
| C9  | `Emergency → (Barrier_Closed ∧ Warning_Active)` |
| C10 | `Sensor_Conflict → ¬Clear_Confirmed` |

**Definition:** `Failsafe_Mode ≡ Barrier_Closed ∧ Warning_Active ∧ Signal_Red`
