Critical Architecture Questions for Phase 1:
1. Signal Technology Choice (Most Important)
You mentioned both Bluetooth and SDR options. Which would you prefer to start with for Phase 1?
What specific Bluetooth hardware do you have available?
What SDR device do you have (RTL-SDR, HackRF, etc.) and what frequency ranges can it handle?
2. Cat Tracker Hardware Approach
Are you planning to start with a commercial tracker (like Tile, AirTag, or Tabcat) to "hijack" signals, or build a custom beacon?
If commercial, which specific device were you considering?
Do you already have a test device, or do we need to factor in procurement time?
3. Software Stack Preferences
What programming language do you prefer for the core tracking system? (Python seems like a natural fit for rapid prototyping)
For the UI, are you leaning toward a web interface, desktop app, or command-line for Phase 1?
Any preference for frameworks? (Flask/FastAPI for web, tkinter for desktop, etc.)
4. Development Environment
What OS will you be developing on? (Windows, Linux, macOS)
Do you have any constraints on development tools or libraries?
5. Data Storage & Logging
For Phase 1, are you okay with simple file-based logging, or do you want to set up a proper database from the start?
How much historical data do you want to retain? (signal logs, status changes, etc.)
6. Testing Strategy
Do you have access to your cat for testing, or should we build in simulation capabilities?
What's your property layout like for testing range/signal strength?
These decisions will significantly impact the Phase 1 architecture and implementation approach. Which of these areas would you like to tackle first?