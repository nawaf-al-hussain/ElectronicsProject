# Reference Journal — IoT Environmental Monitoring & Control for Mushroom Cultivation (notes)

*(Source: `../sources/journal-iot-for-agriculture.pdf` — teacher-provided reference under "Journal Articles".)*

**Citation:** Chong, J.L.; Chew, K.W.; Peter, A.P.; Ting, H.Y.; Show, P.L. — "Internet of Things (IoT)-Based Environmental Monitoring and Control System for Home-Based Mushroom Cultivation," *Biosensors* (MDPI).

## What the paper does

- Sensors for temperature, humidity, light intensity, soil moisture connected to a **NodeMCU**; data to a cloud server; remote monitoring **and control** via mobile/web app, including **live video** of growth.
- Control algorithm regulates chamber equipment autonomously from sensor feedback to hold optimum growth conditions.
- Sensor readings validated against manual readings for accuracy.

## Why the teacher supplied it

It is the reference model for **Direction 1** of the curated problems menu (sensor data → storage → cloud → dashboard, closed-loop control). It shows the expected rigour: sense → validate against manual readings → automate on thresholds → visualize remotely.

## Relevance to the CropGuard decision

- Supports the *monitoring/dashboard* half of an agri project, but note: this "sense-and-regulate greenhouse" pattern is exactly what the dossier **rejected as a headline** (soil sensing + precision irrigation = too generic; 10 of 36 teams this season do its variants).
- Where it *does* help CropGuard: its validation discipline (sensor vs manual reading) mirrors the dossier's acceptance tests, and its video/telemetry layer is a plausible **future-work slide** for the platform robot.
