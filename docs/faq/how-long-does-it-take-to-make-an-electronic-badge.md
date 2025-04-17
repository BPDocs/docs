# ❓ Question: How long does it take to make an electronic badge?

The time it takes to create an electronic badge depends heavily on complexity, feature set, and whether you're working solo or with a team. Here's a general breakdown:

## 🧠 Planning & Design (2–4 weeks)
- Define functionality: LED patterns, screens, games, sensors, etc.
- Select microcontroller, power source, and peripherals
- Draft the schematic and physical layout

## 🛠️ PCB Layout & Prototyping (2–4 weeks)
- Design the PCB (routing, art, test points)
- Order boards and parts from suppliers
- Optional: Use a PCB assembly service for surface-mount components

## 🔧 Assembly & Testing (2–4 weeks)
- Hand-solder or reflow boards
- Flash firmware and test hardware functionality
- Fix hardware bugs and prepare for production

## 👾 Firmware Development (4–8+ weeks)
- Write code for UI, animations, games, OTA updates, etc.
- Test performance, power management, and user input
- Iterate as needed

## 📦 Final Production (4–8+ weeks, if mass-producing)
- Refine design for manufacturing
- Assemble, test, and package units

---

## ⏱️ Estimated Total Time (Based on Complexity)

| **Badge Type**                 | **Estimated Timeline** |
|-------------------------------|------------------------|
| Basic LED-only badge          | 6–8 weeks             |
| ESP32 badge with screen       | 3–4 months            |
| Feature-rich con badge        | 6–12+ months          |
| Mass production (100+ units)  | 6–14+ months          |

---

Most delays happen due to **PCB revisions**, **component shortages**, or extended **firmware debugging**. Starting with a solid plan and reusing proven modules (like SAO headers, boot circuits, or LVGL code) can help, but complex projects require significant time investment for quality results.

!!! warning "Planning Ahead"
    Start your badge project well in advance of your target event date. Component shortages and manufacturing delays can significantly impact timelines.

**Need help planning your badge project timeline? Join our [Discord](https://discord.gg/BfsYbHY8m7) for personalized advice!**
