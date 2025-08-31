Perfect 🚀 — here’s a **ready-to-use `README.md` draft** for your GitHub repo. You can directly copy-paste and adapt it.

---

# UAV–GS–BS Secure Authentication Protocol

## 📌 Overview

This project implements and **formally verifies** a **mutual authentication and secure session key establishment protocol** between three entities:

* **UAV (Unmanned Aerial Vehicle)**
* **GS (Ground Station)**
* **BS (Base Station)**

The protocol is modeled and verified using **ProVerif**, ensuring strong guarantees under the **Dolev–Yao adversary model**.

---

## 🎯 Protocol Goal

* Enable a UAV to securely communicate with the Ground Station (GS).
* Ensure that GS and BS cooperate to authenticate UAVs and distribute session keys.
* Provide **mutual authentication** and **fresh session keys** for secure communication.

---

## 🏗️ Roles of the Entities

### ✈️ UAV (Unmanned Aerial Vehicle)

* Initiates authentication with the Ground Station.
* Verifies both GS and BS participation.
* Establishes a **fresh session key** for secure communication.

### 🛰️ Ground Station (GS)

* Acts as an **intermediary** between UAV and BS.
* Verifies UAV’s authenticity.
* Collaborates with BS to generate and forward session keys.

### 🏢 Base Station (BS)

* Central trusted authority in the network.
* Authenticates both UAV and GS.
* Generates a **new symmetric session key (ks)** for each session.
* Ensures **secure distribution** of session keys.

---

## 🔑 Security Properties Verified

1. **Authentication**

   * Each entity only completes the protocol if the other has genuinely started.

2. **Mutual Authentication**

   * UAV ↔ GS ↔ BS are strongly authenticated to each other.

3. **Session Key Freshness**

   * Every session uses a newly generated key.

4. **Replay Attack Resistance**

   * Old messages cannot be reused in new sessions.

5. **Confidentiality (optional)**

   * Session key `ks` can be proven secret by querying:

     ```proverif
     query attacker(ks).
     ```

---

## ✅ Advantages

* **Formally Verified** using ProVerif (stronger than just proposing).
* **Resists replay and man-in-the-middle (MITM) attacks**.
* **Ensures trust continuity** across three entities.
* **Scalable foundation** for multi-UAV systems.
* **Cryptographically sound** under the **Dolev–Yao model**.

---

## ⚠️ Limitations

* **No performance modeling** → UAV resource constraints (battery/CPU) not considered.
* **Forward secrecy not fully proven** (needs additional modeling).
* **Designed for 3 entities only** → multi-UAV scalability not tested.
* **Assumes secure key setup** (long-term keys already shared).

---

## 🧪 Tools Used

* [**ProVerif**](https://proverif.inria.fr/) — for formal protocol verification.
* **Graphviz** — to visualize message flows.

---

## 📜 Protocol Diagram

![Protocol Diagram](uav_gs_protocol_diagram.png)

---

## 📂 Repository Structure

```
.
├── uav_gs_bs.pv             # ProVerif model for UAV–GS–BS protocol
├── uav_gs_protocol_diagram.png  # Protocol message flow diagram
├── README.md                # Documentation (this file)
```

---

## 📖 How to Run

1. Install **ProVerif**:

   ```bash
   sudo apt-get install proverif
   ```

2. Run the model:

   ```bash
   proverif uav_gs_bs.pv
   ```

3. Check results for **Authentication, Secrecy, and Freshness**.

---

## 📌 Conclusion

This protocol demonstrates how **formal verification** strengthens the security of UAV communication systems. By verifying authentication, key freshness, and resistance to replay attacks, it provides a **solid foundation for secure UAV networks**.


