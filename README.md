# UAV–GS–BS Secure Authentication Protocol

##  Overview

This project implements and **formally verifies** a **mutual authentication and secure session key establishment protocol** between three entities:

* **UAV (Unmanned Aerial Vehicle)**
* **GS (Ground Station)**
* **BS (Base Station)**

The protocol is modeled and verified using **ProVerif**, ensuring strong guarantees under the **Dolev–Yao adversary model**.

---

##  Protocol Goal

* Enable a UAV to securely communicate with the Ground Station (GS).
* Ensure that GS and BS cooperate to authenticate UAVs and distribute session keys.
* Provide **mutual authentication** and **fresh session keys** for secure communication.

---

##  Roles of the Entities

###  UAV (Unmanned Aerial Vehicle)

* Initiates authentication, generates fresh nonces, and communicates securely via the Base Station to the Ground Station.

###  Ground Station (GS)

* Verifies UAV authenticity, issues session keys, and acts as the central trust authority in coordination with the BS.

###  Base Station (BS)

* Coordinates communication between UAV and GS, ensures secure session key distribution, and maintains session logs.

---

##  Security Properties Verified
The following properties are formally verified using ProVerif:

1. **Authentication**

   * Each entity only completes the protocol if the other has genuinely started.

2. **Mutual Authentication**

   * UAV ↔ GS ↔ BS are strongly authenticated to each other.

3. **Session Key Freshness**

   * Every session uses a newly generated key.

4. **Replay Attack Resistance**

   * Old messages cannot be reused in new sessions.

---

##  Advantages

* **Formally Verified** using ProVerif 
* **Resists replay and man-in-the-middle (MITM) attacks**.
* **Ensures trust continuity** across three entities.
* **Scalable foundation** for multi-UAV systems.
* **Cryptographically sound** under the **Dolev–Yao model**.

---

##  Limitations

* **Forward secrecy not fully proven** (needs additional modeling).
* **Designed for 3 entities only** → multi-UAV scalability not tested.
* **Assumes secure key setup** (long-term keys already shared).

---

##  Tools Used

* [**ProVerif**](https://proverif.inria.fr/) — for formal protocol verification.
* **PlantUML** — to visualize message flows.

---

##  Protocol Diagram

![Protocol Diagram](/uav_system.png/)

---

##  How to Run

1. Install **ProVerif**:

   ```bash
   sudo apt-get install proverif
   ```

2. Run the model:

   ```bash
   proverif uav_gs_bs.pv
   ```

---

##  Conclusion

This protocol showcases the effectiveness of formal verification in enhancing UAV communication security. By ensuring mutual authentication, key freshness, and resilience against replay attacks, it establishes a lightweight and robust framework for secure UAV networks.

