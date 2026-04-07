# What is an SAO?

**SAO** stands for **Simple Add-On**. It's a small PCB that plugs into a host badge through a standardized 2x3 pin header, originally created for DEF CON's badge ecosystem and now used at many conferences.

## What an SAO does

An SAO can be as simple as a piece of PCB art with a couple of LEDs, or as complex as a full microcontroller-based mini-badge with sensors, displays, or its own logic. The standard pinout provides:

- **3.3V power**
- **Ground**
- **I²C SDA / SCL** for communication with the host
- **Two general-purpose I/O pins**

## Why people collect them

SAOs are wearable, swappable, and tradeable. At hardware-friendly conferences, you'll see attendees walking around with a host badge full of SAOs from other crews — each one a little piece of someone else's design.

We've designed several SAOs over the years. A few are still available on our [Tindie store](https://www.tindie.com/stores/badgepirates/), and others were one-off runs handed out at specific events.

## SAOs we've made

- **SAO_BadgePirates** — our logo SAO
- **SAO_HankPropane** — a Hank Hill tribute
- **SAO_Holder-Sword** — the 2022 sword totem holder
- **SAO_keanu-homeboy** — well... it's Keanu

A more complete list is in our [GitHub organization](https://github.com/orgs/BadgePiratesLLC/repositories?q=SAO) under any repo starting with `SAO_`.

## Want to make your own?

The [SAO standard](https://hackaday.io/project/175182-simple-add-ons-sao) is open and well documented. Our [Common Library](https://github.com/BadgePiratesLLC/BadgePirates_Common_Library) on GitHub has KiCAD footprints you can drop into your own design.
