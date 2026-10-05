# Task 1 — Identify Constraints

**System:** Automated Railway Level-Crossing Control System (ARLCCS)

| ID  | Constraint (simple English) | Why it is necessary |
|-----|-----------------------------|---------------------|
| C1  | The barrier must not be open while a train is in the crossing. | Road vehicles could enter the crossing while the train passes, causing a collision. |
| C2  | If a train is approaching, warning lights and alarm must be active. | Drivers and pedestrians must be warned before the barrier moves. |
| C3  | The barrier may only start lowering when the warning is already active. | Gives road users time to clear the crossing before the barrier descends. |
| C4  | The barrier may only open after the system confirms the train has fully cleared the crossing. | Prevents opening while the tail of the train is still on the crossing. |
| C5  | The road traffic signal must be red while a train is approaching or present. | Stops new vehicles from entering the danger zone. |
| C6  | If a train-detection sensor fails, the system must enter fail-safe mode (barrier closed, warning on). | A blind system must assume a train may be present. |
| C7  | If a barrier fault is detected, the control center must be alerted. | Operators must send manual protection or maintenance immediately. |
| C8  | If communication is lost, the system must enter fail-safe mode. | Without communication, train status cannot be trusted. |
| C9  | In an emergency, the barrier must be closed and the warning active. | Maximum protection for road users during abnormal conditions. |
| C10 | If sensor readings conflict, "crossing clear" must not be confirmed. | Contradictory data is unsafe to act on; assume the train is still there. |
| C11 | The barrier cannot be both open and closed at the same time. | A contradictory state indicates a sensing or logic error. |
| C12 | The warning must stay active whenever the barrier is not fully open. | Prevents silent or unlit barriers while still lowered or moving. |
