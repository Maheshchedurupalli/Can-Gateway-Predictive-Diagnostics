# Learning Log

A short daily record of what I learn while building the CAN gateway project.

## 16 Nov 2026

**Topic:** CAN database (DBC) files

**What I learned**
- A DBC file defines each CAN message: its ID, length and signals.
- A signal line has the form `name : start bit | length @ byte order and sign (scale, offset) [min|max] "unit"`.
- Physical value = raw value × scale + offset. For example, CoolantTemp uses scale 1 and offset -40, so a raw value of 0 means -40 °C.
- `@1+` means little-endian and unsigned.

**What I did**
- Added `dbc/gateway.dbc` with two example messages: ENGINE_STATUS (0x100) and DIAG_FLAGS (0x200).
- Updated the message map in the README to match.

**Next**
- Plan the STM32 CAN initialisation and the FreeRTOS TX task.

---

## 15 Nov 2026

**Topic:** Git and GitHub basics

**What I learned**
- Git saves versions of my files, and GitHub stores them online so others can see my work.
- A commit is a saved snapshot with a short message.
- A good repo has a README, a LICENSE, a `.gitignore` and a clear folder structure.

**What I did**
- Set up this repository with docs, firmware and dbc folders.
- Wrote the README, hardware notes and project plan.

**Next**
- Plan the STM32 CAN initialisation and the FreeRTOS tasks.

---

## Entry format for future days

**Topic:**
**What I learned:**
**What I did:**
**Next:**
