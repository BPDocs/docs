# ❓ What colors can PCBs be made with?

The most common PCB color is **green**, but modern manufacturing allows for a wide range of solder‑mask colors—plus some flashy specialty options if you pick the right fab. Here’s what you can expect:

## 🎨 Common Solder‑Mask Colors

| Color       | Notes |
|-------------|-------|
| **Green**   | Industry standard, great contrast for inspection, cheapest. |
| **Black**   | Sleek and professional, but harder to inspect and can trap heat. |
| **Red**     | Popular alternative to green, offers good contrast. |
| **Blue**    | Visually striking, a fan favorite for dev boards. |
| **White**   | Clean look, but can discolor over time and is harder to inspect. |
| **Yellow**  | Rare but bright; decent trace visibility. |
| **Purple**  | Signature OSH Park color; premium look. |
| **Orange**  | Uncommon; may require a premium tier. |
| **Matte Finishes** | Matte black/green/blue/red available from some fabs for a boutique aesthetic. |

## 🧪 Silk & Copper Color Considerations

- **Silkscreen** is usually white, black, or yellow—choose a color that contrasts strongly with your solder mask.
- **ENIG (gold finish)** pairs beautifully with dark masks like black or purple.
- **HASL (silver finish)** is the budget default and works with most colors.

## 🏭 Typical Fab Offerings

| Fab            | Standard Color Set                    |
|----------------|---------------------------------------|
| **JLCPCB**     | Green, Red, Blue, Yellow, Black, White |
| **PCBWay (Standard)** | Same as JLCPCB                  |
| **OSH Park**   | Purple only                           |
| **Seeed Studio** | Same as JLCPCB + occasional matte   |

---

## 🌈 PCBWay **Advanced PCB**: Extra Colors & Full‑Color UV Printing

PCBWay’s *Advanced PCB* service unlocks additional solder‑mask options—**pink, grey, orange, transparent, matte blue, and matte red**—that aren’t available in the standard tier. :contentReference[oaicite:0]{index=0}  

Even more eye‑catching, the Advanced line now supports **full‑color UV printing** on one or both sides of the board. This process lets you print photographs, gradients, or intricate artwork directly onto the PCB:

- **How it works:** Choose a base solder‑mask color (white is recommended for best fidelity) and supply PCBWay with a reference image or multi‑color silkscreen layers.
- **Design limits:** Maximum single‑board size ≈ 270 × 470 mm; avoid placing artwork over exposed pads; provide artwork in PDF/PNG/JPEG/AI, zipped with your Gerbers.
- **Finishes:** Matte and glossy UV inks available; the print survives standard SMT reflow. :contentReference[oaicite:1]{index=1}

*Heads‑up:* Advanced colors and UV prints add cost and 2‑3 days to lead‑time, so factor that into your schedule.

---

### 💡 Tip

For a badge that really *pops*:  
Pair a bold solder mask (e.g., matte black, pink, or transparent) with **ENIG gold plating**, then add full‑color UV artwork on the front side and high‑contrast white silkscreen on the back. Assembly techs can still read the reference designators, and your badge will dominate the swag table!