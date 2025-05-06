# 📡 Configuration of XBee S2C Modules using XCTU

This guide explains how to configure **two XBee S2C modules** using **XCTU**: one as a **Coordinator** and the other as a **Router**, for point-to-point or mesh communication in ZigBee networks.

---

## 🧰 Requirements

- 2× XBee S2C Modules (ZigBee protocol)
- 2× XBee USB Adapter Boards
- USB Cables
- **XCTU Software** (by Digi International)
- PC with XCTU installed

---

## 🛠️ Step-by-Step Configuration Using XCTU

### 🔽 Step 1: Install XCTU

1. Download XCTU from: [https://www.digi.com/xctu](https://www.digi.com/xctu)
2. Install and launch the software.

---

### 🔌 Step 2: Connect XBee Modules

1. Plug each XBee S2C into a USB adapter board.
2. Connect the first adapter to the PC via USB.

---

### ➕ Step 3: Add Module in XCTU

1. Open XCTU and click the **“Add devices”** (🔍) icon.
2. Select the COM port and **click “Finish”**.
3. The connected XBee will now appear in the left panel.

---

### ⚙️ Step 4: Configure the **Coordinator XBee**

1. Select the XBee device from the left panel.
2. Click **"Read" (eyedropper icon)** to load current settings.
3. Change the following settings:

| Parameter       | Setting         | Description                       |
|----------------|------------------|-----------------------------------|
| **CH (Channel)**        | e.g., `0C`            | Must match with router            |
| **PAN ID (ID)**         | e.g., `1234`          | Same for all devices in the network |
| **DH / DL (Destination)** | Set later or broadcast | Can be left default (`0000`)      |
| **CE (Coordinator Enable)** | `1` (Coordinator)   | Makes it the Coordinator          |
| **BD (Baud Rate)**       | `9600` (or preferred) | Serial speed                      |
| **NI (Node Identifier)** | `COORDINATOR`         | For easy identification           |

4. Click **“Write”** (pencil icon) to save changes.

5. Disconnect and remove this XBee from XCTU.

---

### 🔁 Step 5: Configure the **Router XBee**

1. Connect the second XBee to the PC and repeat **Step 3** to add it.
2. Load current settings (click **Read**).
3. Set these parameters:

| Parameter       | Setting         | Description                       |
|----------------|------------------|-----------------------------------|
| **CH (Channel)**        | Same as Coordinator | e.g., `0C`                        |
| **PAN ID (ID)**         | Same as Coordinator | e.g., `1234`                      |
| **CE (Coordinator Enable)** | `0` (Router)       | Must be set to 0                 |
| **BD (Baud Rate)**       | Same as Coordinator | e.g., `9600`                      |
| **NI (Node Identifier)** | `ROUTER`             | For identification               |

4. Optionally set:
   - **DH / DL** to Coordinator’s serial number (for targeted communication)

5. Click **“Write”** to save settings.

---

## 🔄 Optional: Addressing for Point-to-Point Communication

To make the router send data directly to the coordinator:

1. On **Router**, set:
   - **DH (Destination High)** = Coordinator's **SH (Serial Number High)**
   - **DL (Destination Low)** = Coordinator's **SL (Serial Number Low)**

2. On **Coordinator**, do the same for router’s SH/SL if bidirectional communication is needed.

---

## 💻 Example Code (Serial Communication Test)

No code is needed if you’re just sending serial data. However, for testing via Arduino or another microcontroller, here's an example for sending data from Arduino to XBee:

### Arduino Code to Send Data via Serial
```cpp
void setup() {
  Serial.begin(9600);  // Must match XBee baud rate
}

void loop() {
  Serial.println("Hello from Arduino via XBee!");
  delay(2000);
}

```
### Use Serial Monitor on the other XBee (connected to XCTU) to observe the received data.

## 🧪 Testing the Communication

- Open **XCTU terminal** for the **Coordinator XBee**.
- Send data from the **Router** via XCTU terminal or Arduino.
- You should see data arriving in real time.

---

## 🧘 Troubleshooting Tips

- Make sure both XBees use the **same PAN ID** and **Channel**.
- Ensure one device is set to **Coordinator (CE=1)**.
- Use **matching baud rates** for communication.
- Ensure **DH/DL** are set correctly for directed communication.

---

## 📘 Conclusion

You’ve successfully configured two XBee S2C modules using XCTU:

- One as a **Coordinator**
- One as a **Router**

They can now communicate wirelessly using the **ZigBee protocol**, ideal for **mesh networks** and **IoT systems**.
