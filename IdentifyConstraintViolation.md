 Task 3 — Identify Constraint Violations

A constraint `P → Q` is **violated** when `P = TRUE` and `Q = FALSE`.

| #   | Constraint | Violation State | What went wrong | How we know it is violated |
|-----|------------|-----------------|-----------------|----------------------------|
| V1  | C1: `Train_Present → ¬Barrier_Open` | `Train_Present = T`, `Barrier_Open = T` | Barrier reopened (or never closed) while the train is on the crossing, so cars can drive onto the tracks. | `T → ¬T` = `T → F` = **FALSE** |
| V2  | C2: `Train_Approaching → Warning_Active` | `Train_Approaching = T`, `Warning_Active = F` | Train detected but lights/alarm did not turn on (e.g. relay failure). Road users get no warning. | `T → F` = **FALSE** |
| V3  | C3: `Barrier_Lowering → Warning_Active` | `Barrier_Lowering = T`, `Warning_Active = F` | Barrier started descending before lights/alarm were on. Vehicles may be trapped. | `T → F` = **FALSE** |
| V4  | C4: `Barrier_Opening → Clear_Confirmed` | `Barrier_Opening = T`, `Clear_Confirmed = F` | Barrier began opening on a timer, without confirmation that the last carriage left. | `T → F` = **FALSE** |
| V5  | C5: `(Train_Approaching ∨ Train_Present) → Signal_Red` | `Train_Present = T`, `Signal_Red = F` | Road signal stayed green while the train occupied the crossing. Drivers are told to proceed. | `(F ∨ T) → F` = `T → F` = **FALSE** |
| V6  | C6: `Sensor_Fault → Failsafe_Mode` | `Sensor_Fault = T`, `Failsafe_Mode = F` | Sensor failed but the system kept normal operation with the barrier open, blind to trains. | `T → F` = **FALSE** |
| V7  | C7: `Barrier_Fault → Control_Alert` | `Barrier_Fault = T`, `Control_Alert = F` | Barrier motor jammed but no alert reached the control center. Operators are unaware. | `T → F` = **FALSE** |
| V8  | C8: `Comm_Loss → Failsafe_Mode` | `Comm_Loss = T`, `Failsafe_Mode = F` | Link dropped but the system kept running on stale data instead of failing safe. | `T → F` = **FALSE** |
| V9  | C9: `Emergency → (Barrier_Closed ∧ Warning_Active)` | `Emergency = T`, `Barrier_Closed = T`, `Warning_Active = F` | Barrier closed but lights/alarm are off during an emergency, so protection is only partial. | `T → (T ∧ F)` = `T → F` = **FALSE** |
| V10 | C10: `Sensor_Conflict → ¬Clear_Confirmed` | `Sensor_Conflict = T`, `Clear_Confirmed = T` | One sensor says "train gone", another says "train present", yet the crossing was declared clear. | `T → ¬T` = `T → F` = **FALSE** |

## Detection Summary

- Each violation is found by **evaluating the formal expression on the current system state**.
- If the premise is TRUE and the conclusion is FALSE, the constraint is violated.
- Expected response: alert the control center, force `Failsafe_Mode`, and log the event.
