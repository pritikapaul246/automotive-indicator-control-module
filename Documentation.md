
## System Architecture Diagram

<img width="2504" height="362" alt="mermaid-diagram (1)" src="https://github.com/user-attachments/assets/71c4a774-4bd6-4877-92a2-ab257ff848bb" />

Shows scheduler-based firmware flow from push-button input through finite state machine logic to LED indicator outputs with hazard arbitration control.


## Hardware Interface Diagram

<img width="998" height="523" alt="mermaid-diagram" src="https://github.com/user-attachments/assets/29dc373c-72d4-4bd6-8b24-5bf63ef23d53" />

Illustrates GPIO connections between ESP8266 NodeMCU, left/right push buttons (D1, D2), and indicator LEDs (D5, D6).


## Scheduler Timing Diagram

<img width="1300" height="1302" alt="mermaid-diagram (2)" src="https://github.com/user-attachments/assets/eba5869b-4825-490f-85c4-f98bdcd4d956" />

Depicts periodic execution of 100 ms input sampling task and 300 ms LED control task in the cooperative scheduler architecture.


## Indicator Control State Machine Diagram

<img width="2099" height="871" alt="mermaid-diagram (3)" src="https://github.com/user-attachments/assets/8f59a44f-82f8-4bff-994c-f0ccdced1bbb" />

Represents FSM transitions between IDLE, LEFT_ACTIVE, RIGHT_ACTIVE, and HAZARD_ACTIVE states triggered by ≥1 second button hold detection.
