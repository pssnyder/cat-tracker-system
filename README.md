# **Project Documentation: Home-Centered Cat Tracker**

## **Project Idea**

The goal is to design and build a minimally invasive, long-range cat tracking system for a 3-acre property. This system will combine the compactness and local findability of radio frequency (RF) devices with the data-rich, networked insights of modern connected apps. The system will not rely on public data channels, ensuring privacy and reliability.

## **Project Goals**

* **Create a Compact Tracker:** Develop a tracking unit small enough to be worn comfortably on a cat's collar for extended periods without irritation.  
* **Achieve Long Battery Life:** Design a low-power system where the tracker's battery can last for several weeks on a single charge.  
* **Ensure Reliable Signal:** Utilize a robust communication protocol that provides reliable signal strength and does not rely on public or crowd-sourced networks.  
* **Enable Triangulation:** Implement a system of three or more ground-based beacons that can triangulate the location of the cat's tracker, providing precise spatial data.  
* **Establish Location Zones:** Define and programmatically identify the cat's location within distinct zones: "at home," "on the property," and "near home."  
* **Provide Findability:** Ensure the tracker can be located using traditional radio frequency direction finding methods (e.g., a handheld Yagi antenna).

## **System Architecture Overview**

The system consists of two primary components:

1. **The Tracker:** A miniature, battery-powered unit on the cat's collar with a low-power transmitter/beacon.  
2. **The Base Station:** A central home-based hub and a network of three (or more) ground beacons strategically placed around the property.

The base station and beacons will perform the following functions:

* **Self-Triangulation:** The ground beacons will use GPS and inter-beacon communication to establish their precise locations relative to the home base.  
* **Tracker Pinging:** The beacons will periodically ping for the cat's tracker.  
* **Spatial Calculation:** Using the received signal strength (RSS) and the known positions of the beacons, the system will calculate the cat's location.  
* **Status Update:** The home base hub will process the location data and update the cat's status (e.g., via a connected app) to reflect its current zone.

## **Key Features & Requirements**

* **Wireless Communication:** The system should use a license-free frequency band for data transmission between the tracker, beacons, and base station, or a licensed band that aligns with your amateur radio license.  
* **GPS Integration:** The ground beacons will require GPS modules for self-calibration and precise location establishment.  
* **Location Zones:** The application or interface must visually represent the three predefined zones, updating the cat's status in real time.  
  * **Near Home:** Tracker is within range of at least one beacon (\>150ft from home base).  
  * **On the Property:** Tracker is triangulated by at least three beacons within the 150ft x 300ft area.  
  * **At Home:** Tracker is within a few feet of the home base hub.

## **User Stories**

* **Idea:** As a cat owner, I want to know my cat is safe and nearby without relying on a public network.  
* **Goal:** The system alerts me when my cat is within the "near home" zone (1+ acre) or outside of it.  
* **Benefit:** I can quickly confirm my cat is in a safe area and gain peace of mind without worrying about data privacy or network reliance.  
* **Priority:** High  
* **Idea:** As a developer, I want to use my RF knowledge to locate my cat in the event the tracker is out of range of the beacons.  
* **Goal:** The tracker can be located using a handheld RF-seeking device.  
* **Benefit:** I can manually locate my cat using a trusted method if they wander beyond the automated system's range.  
* **Priority:** High  
* **Idea:** As a cat owner, I want to know when my cat has left the main inhabited area of the property.  
* **Goal:** The application dashboard provides a clear status update when the cat is "on the property" (within the 150ft x 300ft zone).  
* **Benefit:** This provides an accurate, granular location status for the cat's typical roaming area.  
* **Priority:** High  
* **Idea:** As a user, I want a tracker unit that is comfortable and unobtrusive for my cat.  
* **Goal:** The tracker is significantly smaller than commercial options like the Tractive Mini and has a long-lasting, rechargeable battery.  
* **Benefit:** My cat will be comfortable wearing the device, increasing the system's effectiveness and usability.  
* **Priority:** Urgent

## **Initial Tasks**

1. **Hardware Prototyping (Tracker):** Research and select a low-power microcontroller (e.g., ESP32, nRF52), a compact RF module, and a small-capacity, high-efficiency battery.  
2. **Hardware Prototyping (Beacons):** Research and select microcontrollers with built-in GPS and Wi-Fi/RF communication capabilities.  
3. **Software Development (Firmware):** Write firmware for the tracker to broadcast its RF beacon.  
4. **Software Development (Beacon Network):** Develop the logic for beacons to self-triangulate, ping for the tracker, and transmit data to the home base.  
5. **Software Development (Home Base):** Build the data processing and API layer to calculate the cat's location based on beacon data.  
6. **User Interface Development:** Design and build a simple user interface to display the cat's location status and zones.

## **ROAM Tracker**

| Risk | Status | “Con” | Resolution/Mitigation |
| :---- | :---- | :---- | :---- |
| Commercial trackers offering comprehensive capability are too bulky for a 13lb cat, causing discomfort and potential for the device to get caught or fall off. | Owned | Pat | The project's core hypothesis is that the system can be re-designed from the ground up, focusing on a minimal form factor for the cat, with small, energy-efficient remote components performing the heavy lifting and triangulation. |
| Reliance on public, crowd-sourced networks leads to privacy concerns and data inaccuracies. | Resolved | Pat | The system's architecture is designed to be fully self-contained on the property, using a private network of beacons and a home-based hub to ensure data is secure and location is accurate. |
| Signal degradation, loss, and inaccuracy due to environmental factors (woods, steel building, etc.) | Mitigated | Pat | The approach will be to reuse what we can, literally and conceptually, then interject our own better solutions. One idea is to construct repeater devices to amplify the RF signal or inject private signals to ensure more accurate data points from devices like Tabcat or Tile. |
| Size and capability limitations of a compact, cat-wearable device. | Mitigated | Commercial Products | This issue will be resolved by using commercially available trackers and "hijacking" their signals for our own use, allowing us to focus on the more comprehensive network of receiving and processing devices. |

## **Final Review**

* **Task Cohesion:** Ensure that tasks are logically grouped and lead to a clear, testable outcome.  
* **Low Coupling:** Maintain modularity between the tracker, beacons, and base station software to allow for independent development and future improvements.  
* **Documentation:** Maintain a log of component selections, circuit diagrams, and code comments throughout the development process.

## **Roadmap**

### **Phase 1: Home Base Tracker POC (Proof of Concept)**

* **Objective:** To validate the fundamental technology stack and the concept of signal reception and analysis in our specific environment.  
* **Scope:**  
  * **Components:** 1 tracker (commercial or custom), 1 receiver/data processor (the "home base").  
  * **Location:** The home base will be centrally located in the house.  
  * **Core Functionality:** Proximity tracking.  
    * The system will provide a binary value: "in range" or "out of range."  
    * A simple visual indicator (e.g., an LED) will illuminate if the tracker is in range.  
    * A counter will log how many times the cat passes in and out of range.  
  * **Stretch Goal:**  
    * Attempt to collect and analyze signal strength (RSSI) data.  
    * Use RSSI to create a proxy value for distance (assuming ideal signal conditions).  
    * Enhance the user experience with a "red, yellow, green" status based on signal strength:  
      * Green: Upper 50% of signal strength (close to home).  
      * Yellow: Lower 50% of signal strength (in range, but further out).  
      * Red: No signal (out of range).

### **Proposed Solution:**

The initial approach can leverage just a home computer as the base station. I have either bluetooth cards I can use in isolation just for this project or I also have an SDR device for radio frequency reception, all which would be PC compatible, allowing us to technically do most of the initial work and experimentation on a PC in a contained environment. Bluetooth requires the least additional hardware, so we can start broad using basic concepts to code out what our system should do, making it agnostic to the technology or signal used, whether RF or BLE. We can design the tracking system to be a core tracking processor with a signal API, so as I explore additional signal methods or devices, I can just construct new mappings the system can use. This may even open up the opportunity for redundant signal use and parallel processing for even more reliability.

#### **Key Tasks for Phase 1:**

* **Build a Signal Generator and API:** Develop a software-based signal generator and a signal API to simulate data reception from tracking devices. This will allow for initial functional tests in a controlled environment, isolating the core logic from hardware complications and enabling rapid, repeatable testing.  
* **Create the Tracking Framework:** Design and build a hierarchical status engine. This system will be responsible for processing signal data, calculating the cat's current location, and determining its status details. The hierarchy will allow us to easily add more granular location information in future phases.  
* **Implement Proximity-Based Tracking:** Code the core logic for Phase 1's MVP. This includes the ability to detect a relevant signal, determine the frequency of signal checks, and process the results to deliver a simple "in range" or "out of range" status.  
* **Develop the Initial Human Interface:** Create a user interface (UI) to display the cat's current status. At a minimum, this can be a simple command-line interface or a basic web page that shows whether the cat is in or out of range and logs a running count.  
* **Implement Signal Strength Enhancement:** Integrate the ability to collect signal strength (RSSI) data into the tracking framework.  
* **Update the UI for Signal Data:** Enhance the human interface to visually represent the signal/proximity details, transitioning from the simple binary "in/out of range" to a "red, yellow, green" status based on RSSI values.  
* **Value:** This phase will be a proof of concept to determine if the team is equipped to work with the chosen technologies and if the core hypothesis holds. It will produce a usable, albeit basic, product that provides immediate value.

## AI Agent Expertise Reference

This section outlines the recommended GitHub Copilot AI models for various tasks within this project. Selecting the appropriate model for a given task can improve the quality and relevance of the assistance provided.

| Task / Domain                   | Recommended Copilot Model | Strengths & Rationale                                                                                                                            |
| ------------------------------- | ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Project Planning & Design**   | **Gemini 2.5 Pro**        | Best for brainstorming, ideation, creating project plans, defining system architecture, and generating documentation like this README.              |
| **Hardware & Firmware (C++)**   | **Claude 3 Sonnet**       | Excellent for complex coding tasks and low-level languages. Its large context window is ideal for working with hardware datasheets and libraries.    |
| **Backend Services (Python)**   | **Claude 3 Sonnet**       | Particularly strong with Python and handling large, complex codebases. Ideal for developing the API, database logic, and server-side components. |
| **Frontend Web App (JS/HTML/CSS)** | **GPT-4 Turbo**           | Highly proficient with modern web frameworks and languages. Excels at generating component code, styling, and client-side application logic.      |
| **Code Review & Refactoring**   | **Claude 3 Sonnet**       | The large context window allows it to understand the entire scope of the code, making it superior for identifying deep-seated issues and refactoring. |
| **Unit Testing & Debugging**    | **GPT-4 Turbo**           | Strong logical reasoning and problem-solving capabilities make it well-suited for generating comprehensive test cases and proposing targeted fixes.  |