# Project Viva Evaluation — 15 Marks (verbatim extraction)

*(Source: `../sources/viva-preparation-guideline.docx`. Marks per block as printed in the document; the listed blocks total 10 explicit + code walkthrough as the remaining weight.)*

## 1. Name all sensor, actuator, MCU modules — 3 Marks

## 2. Know how the sensors really work and produce data — 3 Marks

Example questions from the guideline:
- How does an IR sensor work? Why are there two LED-like structures?
- What is the full form of PIR? Why is there a fresnel prism?
- How does an MPU measure acceleration and angular speed?
- Difference between DC motor, stepper and servo motors
- How does an encoder in a motor work

## 3. How does the MCU control the actuator based on data? Show how to use/operate it — 4 Marks

Example questions:
- What is PID? How are you measuring motor speed and providing feedback?
- Which filters did you use for denoising sensor data? Which ML/DL models did you use?

## 4. Codes — walkthrough

- Show how you read sensor measurements, filter noise
- How did you calculate intermediate features? How are actuators controlled from this data?
- Example: "Show me the code where you are reading BPM sensor data? How are you calculating BPM? How do you justify the formula? How are you showing it in the dashboard? How do you connect to different WiFi routers?"

## Rules

- You may bring printed connection diagrams, flowcharts and codes to the viva
- But cannot share them with others
