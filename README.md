# EnergyGrid Data Aggregator

## Overview
This project is a client application that fetches real-time telemetry data for **500 solar inverters** from a legacy EnergyGrid API while strictly following server constraints such as **rate limiting**, **batch size**, and **request signing**.

The goal was to reliably collect data from all devices without overwhelming the server or violating security rules.

---

## What This Project Does
- Generates **500 device serial numbers** (`SN-000` to `SN-499`)
- Sends requests in **batches of 10 devices**
- Enforces a **strict rate limit of 1 request per second**
- Signs every request using **MD5(URL + Token + Timestamp)**
- Handles **HTTP 429 (Too Many Requests)** using retry logic
- Aggregates the data for all 500 devices into a single result

---

## Tech Stack
- **Node.js**
- No external libraries for rate limiting or signing
- Express (used only in mock API)

---

## How to Run Locally

### Step 1: Start the Mock API Server
Open a terminal and run:

```bash
cd mock-api
npm install
npm start
You should see:

⚡ EnergyGrid Mock API running on port 3000


Keep this terminal running.

### Step 2: Run the Client Application

Open another terminal and go to the client project root:

npm install
npm start


Expected Output

The client will fetch data batch by batch and display logs like:

🔌 Starting EnergyGrid Data Aggregation...
✅ Fetched batch (10)
⚠️ 429 received, retrying...
...
🎉 Completed! Total devices: 500


A sample of aggregated device data will be printed at the end.

Notes

Seeing {"error":"Missing headers"} in the browser at localhost:3000 is expected.
The API requires signed POST requests and rejects direct browser access.

Total execution time is ~50 seconds due to the 1 request/second limit.
