# ⚡ Small Craft (e.g. ClassGlobe 5.80) — 12 V DC Electrical System

Welcome aboard! This is your boat’s **electrical brain** — drawn so you (builder, sailor, tinkerer) can read it, understand it, and even talk to it using AI. The file [`scdcs.svg`](scdcs.svg) isn’t just a picture; it’s your **living wiring plan**. Every device, cable, switch, and fuse includes embedded data — wire sizes, allowable lengths, ratings, and more. You can open it in a browser, share it, or hand it to a technician.

And yes — you can also let AI help you check it.

---

## Design Philosophy — Simple, Minimal, Complete

This system is intentionally **small and tidy**:

* The fewest possible parts to meet offshore needs
* Short cable runs
* Device-integrated switching where feasible
* *Clear fusing* everywhere

The **selector and combiner** logic remains intuitive, the **reserve battery** can operate independently, and essential gear (bilge, navigation lights, VHF/AIS, GPS) is covered — without “gadget creep.”

---

## Why This Matters for You (the Builder–Sailor)

You’re building a boat, not wiring a factory.

You need:

* **Clarity** — no hidden pathways
* **Safety** — know what’s protected, redundant, or critical
* **Flexibility** — upgrade, repair, or tweak without guesswork
* **Trust** — when you head offshore, you know the system will behave

This SVG is your single source of truth.

---

## System at a Glance

| Subsystem         | What It Does                                        | Notes for Builders                                      |
| ----------------- | --------------------------------------------------- | ------------------------------------------------------- |
| **Batteries**     | House + Reserve (LiFePO₄ 12.8 V)                    | Each is fused and cross-linked via the combiner         |
| **Selector**      | Blue Sea 6008 selector switch                       | Enables selecting between House, Reserve, or OFF        |
| **Auto-Combiner** | Victron Cyrix Li-ct                                 | Joins batteries when voltage is high; isolates when low |
| **Distribution**  | Switched + Always-On blocks                         | Separates essential and non-essential loads             |
| **Loads**         | Nav lights, VHF, AIS, GPS, bilge, tiller, USB, etc. | Each load has its own fuse and wire size                |
| **Solar**         | SunWare panels with Victron MPPTs                   | Feeds House, Reserve, and emergency circuits            |
| **Network**       | NMEA 2000 backbone                                  | AIS, GPS, VHF, depth sensor spurs                       |
| **RF / Antenna**  | VHF + AIS antenna feed                              | RG-8X cable, safe routing, and splitter logic           |

---

## Operations Cheat Sheet

| Action             | What You Do                       | What Happens                                                       |
| ------------------ | --------------------------------- | ------------------------------------------------------------------ |
| Normal cruising    | Selector → **1**                  | House battery powers all systems                                   |
| Use reserve        | Selector → **2**                  | Reserve battery powers the loads                                   |
| Automatic parallel | Leave the Cyrix wired             | Batteries merge at ≥ 13.4 V; stay separate under 13.2 V            |
| Bilge override     | Flip the bilge switch **UP**      | Pump runs even if automatic control fails                          |
| Changing nav mode  | Use the Mast and Deck switches    | Configures correct COLREG lighting                                 |
| Emergency solar    | Plug in the red emergency PV lead | Feeds **Always-On** circuits                                       |
| Tiller autopilot   | Use the cockpit power socket      | The tiller draws from the Reserve; it’s unaffected by the selector |

### Lighting Modes

| Mode                     | Switch Positions                                      | Output                     | Power (W) |
| ------------------------ | ----------------------------------------------------- | -------------------------- | --------: |
| **Sail (Mast)**          | `switch.mast = UP (TRI)` · `switch.deck = CTR`        | Mast tricolor only         |       1.9 |
| **Off**                  | `switch.mast = CTR` · `switch.deck = CTR`             | All nav lights off         |       0.0 |
| **Anchor**               | `switch.mast = DN (ARW)` · `switch.deck = CTR`        | Mast all-round white (ARW) |       1.0 |
| **Engine (< 12 m)**      | `switch.mast = DN (ARW)` · `switch.deck = DN (Side)`  | Mast ARW + sidelights      |       3.3 |
| **Sail (Deck / Emerg.)** | `switch.deck = UP (Side+Stern)` · `switch.mast = CTR` | Deck sidelights + stern    |       3.3 |

### NAV/COM Switching

| Device                         | Switch Type | Selector Behavior                  | After Power Loss            |
| ------------------------------ | ----------- | ---------------------------------- | --------------------------- |
| Actisense A2K-SBN-1 N2K Hub    | Hard-wired  | Always ON when supplied            | Resumes ON                  |
| Echomax Active-XS RTE          | Hard switch | ON → becomes active immediately    | Resumes ON                  |
| Raymarine Axiom (chartplotter) | Soft switch | Remembers last ON/OFF state        | Recovers last state         |
| Standard Horizon GX2410GPS VHF | Soft switch | Always OFF after power loss        | **OFF** (must be turned on) |
| Raymarine i50 Depth            | Soft switch | Remembers last state               | Recovers last state         |
| em-trak B923 AIS               | Hard switch | ON → device powers; OFF → no power | Resumes ON                  |

---

## Let AI Help You (with [`scdcs.svg`](scdcs.svg))

You can ask **ChatGPT** — your electrician-in-a-box — to explain, check, or troubleshoot the wiring diagram in plain sailor’s language.

### Quick Start (~1 minute)

1. **Download** `scdcs.svg` → [Download `scdcs.svg`](./scdcs.svg)
2. Go to `https://chat.openai.com` or open the ChatGPT app
3. Start a new chat
4. **Upload** your `scdcs.svg` (drag it into the window)
5. Paste this message:

```
Here is my boat’s wiring diagram, scdcs.svg. Read it and confirm you can see components, fuses, cables, and notes. Then give me a simple overview.
```

ChatGPT will read wire sizes, fuse ratings, switch logic, voltage-drop limits, and part details — and walk you through how your system works.

### What You Can Ask

**Basics**

> Which battery powers the boat right now?
> What happens when I switch from 1 to 2?
> Explain how power flows from the battery to the lights.

**Charging**

> How do the solar panels charge both batteries?
> Which systems keep running if solar stops?

**Safety & Checks**

> List every fuse and what it protects.
> Are all wires within safe voltage-drop limits?

**Troubleshooting**

> My VHF won’t power up — which fuse or switch should I check first?
> If the bilge pump doesn’t run, where do I start?

**Passage Prep**

> Summarize the three most important electrical checks before a long trip.
> If the House battery fails, what still works?

### Tips for Better Results

* Use exact identifiers (e.g., `selector.house`, `fuse.sw.navcom.vhf`, `load.gps`)
* Ask for **tables**, **summaries**, or **step-by-step explanations**
* If it’s too technical, say: *“Explain this as though I’m building my own 5.80, not an engineer.”*

---

## Customizing Your System — Prompt Ideas

**Adding gear**

> I want to add a small cockpit light or a stereo. Where should I connect it, and what fuse sizes should I use?
> Where should I take power for a cabin fan so it doesn’t drain the batteries while at anchor?

**Changing components**

> Replace the Victron MPPT with a different brand — what wiring changes are needed?
> If I switch from LiFePO₄ to AGM batteries, which fuse or wire sizes need adjustment?

**Simplifying layout**

> Show me a simpler version that only powers lights, bilge, and VHF.
> Remove solar circuits and give me a minimal coastal setup.

**Planning upgrades**

> Add a second solar panel + MPPT for the Reserve battery — what wire gauge and fuse ratings would that require?
> Suggest where to place a 12 V USB socket near the chart table and how to fuse it.

---

## ⚓ Sailor-Style (Fun) Prompts

> Would **Don McIntyre** be impressed if he toured my 5.80?
> What might **Nigel Calder** think of this electrical layout?
> Explain my wiring like you’re talking to a shipwright over a beer in Les Sables d’Olonne.
> Translate this setup into the language of an old-school electrician who hates computers.
> Make a fun checklist to explain this system during a boat tour.
> Pretend you’re a surveyor inspecting my 5.80 before launch — what would you praise, and what would you question?
> What’s elegant about this system from a designer’s view?
> How would you describe this to a kid who wants to circumnavigate one day?

---

## Getting Started — Beginner Prompts

| Goal                | Try Asking                                                                                                         |
| ------------------- | ------------------------------------------------------------------------------------------------------------------ |
| Basic understanding | “What does this diagram show in simple terms?” • “Explain how power flows on my boat.”                             |
| Identify key parts  | “Which parts are the batteries?” • “Where is the main switch?”                                                     |
| Normal operation    | “Which battery is used when the selector is on 1?” • “How do I switch to the reserve battery?”                     |
| Safety checks       | “Which fuses protect the lights and radio?” • “What should I check if the lights stop working?”                    |
| Troubleshooting     | “Why might the bilge pump not run?” • “Which fuse should I check if VHF fails?”                                    |
| Charging            | “How do the solar panels charge the batteries?” • “Can both batteries charge at once?”                             |
| Learning mode       | “Explain this as though I’m a new sailor.” • “What are the three most important things to check before a passage?” |

---

## Intermediate / Technical Prompts

* List all loads and how each is powered
* Show every component connected to the **Always-On** bus
* What’s protected by `fuse.sw.navcom.gps`?
* If the selector is **2**, which circuits remain active?
* Estimate how long the House battery will power lights + navigation gear

---

## Advanced / Power-User Prompts

* Extract all `` elements with `data-entity="cable"` and check each against its `data-vdrop-pct-target`
* Create a wiring table: cable ID, size (ABYC/ISO), maximum length, fuse rating
* Validate every fuse’s `data-rating` vs. upstream conductor ampacity
* Trace the power path from `batt.house` to `load.vhf`

---

## Quick AI Prompt Card

**System Basics**

> Explain this electrical system simply.
> Which battery runs the boat now?
> Show me the path from battery to lights.

**Power & Charging**

> How do solar panels charge the batteries?
> Can both charge at once?
> Which circuits stay alive when the selector is off?
> Should there be a fuse between the panels and the batteries?

**Troubleshooting**

> Why might nav lights stop working?
> Which fuse should I check if VHF fails?
> If the bilge pump doesn’t run, what could cause that?
> What if the combiner relay fails?

**Maintenance & Checks**

> List every fuse and its protected circuit.
> Which cable is closest to its max length?
> What is the smallest wire, and which load does it power?
> Are all circuits within voltage-drop limits?

**Passage Prep**

> Explain this system to a skipper before departure.
> Which circuits absolutely must stay powered offshore?
> If the **House** battery dies, what still works?
> What should I do to keep the bilge and nav lights alive in an emergency?

---

## Working with the File

* Open `scdcs.svg` in your browser to see tooltips, embedded links, and metadata
* Print it large (A3/A2) and keep a copy on board
* Use it when reviewing with electricians or ordering parts
* Feed it to AI or engineering tools for checks, upgrades, or audits

---

## License & Caveats

* © 2025 Olaf Koepke — MIT License (see metadata in the SVG)
* Intended for builders; not for direct installation without review
* Always cross-check with **ABYC E-11**, **ISO 13297**, and manufacturer data before final wiring

---

## Designer’s Note: What Makes It Elegant

From a designer’s perspective, the beauty lies in **clarity and restraint**. Nothing is hidden, nothing is extra — every part earns its place. It’s a complete offshore-capable system built from the minimum necessary components: selector, combiner, clear fusing, short runs, and visible logic you can trace at a glance. The balance between *House* and *Reserve*, the automatic yet understandable charge sharing, and the assurance that essential circuits remain live even under failure — that’s real design discipline.

It’s a system that trusts the sailor, not one that tries to outsmart them. That’s why it feels simple, reliable, and elegant all at once.

---

## For the Builder–Sailor

You’re building something real — something that will carry you across oceans. This diagram is your reference, your inspector, your safety check. Use it with pride, and use it with care.

---

## Details

### Primary

#### BOM

* `combiner` — [Victron Energy Cyrix-Li-ct 12/24-120](https://www.victronenergy.com/battery-isolators-and-combiners/cyrix-battery-combiners)
* `selector.house` — [Blue Sea 6008 Selector Switch](https://www.bluesea.com/products/6008/m-Series_Selector_3_Position_Battery_Switch_-_Red)

#### Wiring

* Common negative bridge — ISO 6 mm² / ABYC 10 AWG

  * `neg-bridge-reserve-house.1` — `dist.ao.reserve.term.neg` → `dist.sw.lights.term.neg`
  * `neg-bridge-reserve-house.2` — `dist.sw.lights.term.neg` → `dist.sw.navcom.term.neg`
  * `neg-bridge-reserve-house.3` — `dist.sw.navcom.term.neg` → `dist.ao.house.term.neg`
* → `dist.ao.house` — ISO 6 mm² / ABYC 10 AWG

  * `cable.subfeed.combiner.87` — `dist.ao.house.term.pos` → `combiner.term.87`
* → `dist.ao.reserve` — ISO 6 mm² / ABYC 10 AWG

  * `cable.subfeed.combiner.30` — `dist.ao.reserve.term.pos` → `combiner.term.30`
* → `dist.sw.lights` — ISO 6 mm² / ABYC 10 AWG

  * `cable.subfeed.lights.pos` — `selector.house.term.output` → `dist.sw.lights.term.pos`
* → `dist.sw.navcom` — ISO 6 mm² / ABYC 10 AWG

  * `cable.subfeed.navcom.pos` — `selector.house.term.output` → `dist.sw.navcom.term.pos`

---

### `dist.batt.house` — MRBF House

#### Currents & Fuses

* `dist.ao.house`

  * I 6.8 / 0.5 / 0
  * `fuse.batt.house`
* `dist.sw.lights` *Selector = 1*

  * I 0.8 / 0.3 / 0.3
  * `fuse.batt.house`
* `dist.sw.navcom` *Selector = 1*

  * I 8.2 / 0.9 / 0.7
  * `fuse.batt.house`

#### BOM

* `batt.house` — [Victron Energy Lithium SuperPack 12,8/100](https://www.victronenergy.com/batteries/12,8v-lithium-superpack)

  * `dist.batt.house` — [Blue Sea 5191](https://www.bluesea.com/products/5191/MRBF_Terminal_Fuse_Block_-_30_to_300A)

    * `fuse.batt.house` — [Blue Sea 5178](https://www.bluesea.com/products/5178/MRBF_Terminal_Fuse_-_60A)
    * `fuse.batt.house.lights` — [Blue Sea 5175](https://www.bluesea.com/products/5175/MRBF_Terminal_Fuse_-_30A)
    * `fuse.batt.house.navcom` — [Blue Sea 5175](https://www.bluesea.com/products/5175/MRBF_Terminal_Fuse_-_30A)

#### Wiring

* → `dist.ao.house` — ISO 6 mm² / ABYC 10 AWG; Lmax ISO 3.3 m / ABYC 3.3 m

  * `cable.main.house.neg` — `batt.house.term.neg` → `dist.ao.house.term.neg`
  * `cable.main.house.pos` — `dist.batt.house.term.load` → `dist.ao.house.term.pos`

---

### `dist.ao.house` — Always-on House

#### Currents & Fuses

* `load.bilge`

  * I 4.3 / – / –
  * `fuse.ao.house.bilge.auto` — 5 A [Blue Sea 5239](https://www.bluesea.com/products/5239/ATO___ATC_Fuse_-_5_Amp)
  * `fuse.ao.house.bilge.manual` — 5 A [Blue Sea 5239](https://www.bluesea.com/products/5239/ATO___ATC_Fuse_-_5_Amp)
* `load.usb.h`

  * I 2.5 / 0.5 / –
  * `fuse.ao.house.usb` — 3 A [Blue Sea 5237](https://www.bluesea.com/products/5237/ATO___ATC_Fuse_-_3_Amp)
* `pv.ctrl.emergency`

  * I 5 / – / –
  * `fuse.ao.house.pv-emergency` — 10 A [Blue Sea 5241](https://www.bluesea.com/products/5241/ATO___ATC_Fuse_-_10_Amp)
* `pv.ctrl.house`

  * I 5.7 / – / –
  * `fuse.ao.house.pv-house` — 10 A [Blue Sea 5241](https://www.bluesea.com/products/5241/ATO___ATC_Fuse_-_10_Amp)

#### BOM

* `dist.ao.house` — [Blue Sea 5025](https://www.bluesea.com/products/5025/ST_Blade_Fuse_Block_-_6_Circuits_with_Negative_Bus_and_Cover)

  * `load.usb.h` — [Blue Sea 1045](https://www.bluesea.com/products/1045/12_24V_DC_Dual_USB_Charger_4.8A_with_Intelligent_Device_Recognition)
  * `pv.ctrl.emergency` — [Victron SCC075010060R](https://www.victronenergy.com/solar-charge-controllers/smartsolar-mppt-75-10-75-15-100-15-100-20)

    * `pv.panel.emergency` — [SunWare RX-21052](https://en.sunware.solar/products/solarpanel/45)

      * `pv.panel.emergency.adapter` — [SunWare 30003111](https://en.sunware.solar/products/item_details/30003111)
  * `pv.ctrl.house` — [Victron SCC075010060R](https://www.victronenergy.com/solar-charge-controllers/smartsolar-mppt-75-10-75-15-100-15-100-20)

    * `pv.panel.house` — [SunWare SW-40183](https://en.sunware.solar/produkte/solarmodul/197)
  * `switch.bilge` — [Blue Sea 4150](https://www.bluesea.com/products/4150/WeatherDeck_Toggle_Switch_SPST_-_ON-OFF)

    * `load.bilge` — [Whale SS1212](https://docs.navico.com/view/177634415/8)

#### Wiring

* `cable.subfeed.house.pos` — `dist.ao.house.term.pos` → `selector.house.term.1` — ISO 6 mm² / ABYC 10 AWG
* → `load.bilge` — ISO 1.5 mm² / ABYC 16 AWG; Lmax ISO 3.6 m / ABYC 3.1 m

  * `cable.bilge.auto.pos` — `dist.ao.house.term.pos.bilge.auto` → `load.bilge.term.auto.pos`
  * `cable.bilge.manual.pos` — `switch.bilge.pin-2` → `load.bilge.term.manual.pos`
  * `cable.bilge.neg` — `dist.ao.house.term.neg.bilge` → `load.bilge.term.neg`
* → `load.usb.h` — ISO 0.75 mm² / ABYC 18 AWG

  * `cable.usb.h.neg` — `dist.ao.house.term.neg.usb` → `load.usb.h.term.neg`
  * `cable.usb.h.pos` — `dist.ao.house.term.pos.usb` → `load.usb.h.term.pos`
* ← `pv.ctrl.emergency` — ISO 1.5 mm² / ABYC 16 AWG; Lmax ABYC 1 m

  * `cable.pv.ctrl.emergency.neg` — `pv.ctrl.emergency.term.out.neg` → `dist.ao.house.term.neg.pv-emergency`
  * `cable.pv.ctrl.emergency.pos` — `pv.ctrl.emergency.term.out.pos` → `dist.ao.house.term.pos.pv-emergency`
  * ← `cable.pv.panel.emergency.adapter` — captive

    * `cable.pv.panel.emergency.adapter.neg` — `connector.pv.emergency.neg` → `pv.ctrl.emergency.term.in.neg`
    * `cable.pv.panel.emergency.adapter.pos` — `connector.pv.emergency.pos` → `pv.ctrl.emergency.term.in.pos`
  * ← `cable.pv.panel.emergency.pv` — captive

    * `cable.pv.panel.emergency.neg` — `pv.panel.emergency.term.neg` → `connector.pv.emergency.neg`
    * `cable.pv.panel.emergency.pos` — `pv.panel.emergency.term.pos` → `connector.pv.emergency.pos`
* ← `pv.ctrl.house` — ISO 1.5 mm² / ABYC 16 AWG; Lmax ABYC 1 m

  * `cable.pv.ctrl.house.neg` — `pv.ctrl.house.term.out.neg` → `dist.ao.house.term.neg.pv-house`
  * `cable.pv.ctrl.house.pos` — `pv.ctrl.house.term.out.pos` → `dist.ao.house.term.pos.pv-house`
  * ← `pv.panel.house` — ISO 1.5 mm² / ABYC 16 AWG; Lmax ISO 4.8 m / ABYC 4.2 m

    * `cable.pv.panel.house.neg` — `pv.panel.house.term.neg` → `pv.ctrl.house.term.in.neg`
    * `cable.pv.panel.house.pos` — `pv.panel.house.term.pos` → `pv.ctrl.house.term.in.pos`
* → `switch.bilge` — ISO 1.5 mm² / ABYC 16 AWG

  * `cable.feed.bilge.manual.pos` — `dist.ao.house.term.pos.bilge.manual` → `switch.bilge.pin-2`

---

### `dist.sw.lights` — LIGHTS

#### Currents & Fuses

* `load.chart`

  * I 0.2 / – / 0.1
  * `fuse.sw.lights.chart` — 1 A [Blue Sea 5235](https://www.bluesea.com/products/5235/ATO___ATC_Fuse_-_1_Amp)
* `load.down`

  * I 0.3 / – / 0.1
  * `fuse.sw.lights.down` — 1 A [Blue Sea 5235](https://www.bluesea.com/products/5235/ATO___ATC_Fuse_-_1_Amp)
* `load.mast` (TRI / ARW)

  * P 1.9 / 1.0
  * `fuse.sw.lights.arw` — 1 A [Blue Sea 5235](https://www.bluesea.com/products/5235/ATO___ATC_Fuse_-_1_Amp)
  * `fuse.sw.lights.tri` — 1 A [Blue Sea 5235](https://www.bluesea.com/products/5235/ATO___ATC_Fuse_-_1_Amp)
* `load.side`

  * P 2.3
  * `fuse.sw.lights.side` — 1 A [Blue Sea 5235](https://www.bluesea.com/products/5235/ATO___ATC_Fuse_-_1_Amp)
* `load.stern`

  * P 1.0
  * `fuse.sw.lights.stern` — 1 A [Blue Sea 5235](https://www.bluesea.com/products/5235/ATO___ATC_Fuse_-_1_Amp)

#### BOM

* `dist.sw.lights` — [Blue Sea 5025](https://www.bluesea.com/products/5025/ST_Blade_Fuse_Block_-_6_Circuits_with_Negative_Bus_and_Cover)

  * `load.chart` — [Hella marine 2JA 343 720-622](https://www.hellamarine.com/shop/interior-exterior-lamps/reading-lamps/flexi-spot-led-chart-table-lamp)
  * `load.down` — [Hella marine 2JA 959 950-121](https://www.hellamarine.com/shop/interior-exterior-lamps/downlights/euroled130-surface-mount-round-downlights)
  * `switch.deck` — [Blue Sea 4155](https://www.bluesea.com/products/4155/WeatherDeck_Toggle_Switch_DPDT_-_ON-OFF-ON)

    * `load.side` — [AquaSignal 3853001000](https://www.glamox.com/global-marine/products/outdoor/navigation-lights-and-control-panels/3853001000)
    * `load.stern` — [AquaSignal 3852001000](https://www.glamox.com/global-marine/products/outdoor/navigation-lights-and-control-panels/3852001000)
  * `switch.mast` — [Blue Sea 4155](https://www.bluesea.com/products/4155/WeatherDeck_Toggle_Switch_DPDT_-_ON-OFF-ON)

    * `load.mast` — [AquaSignal 3857001000](https://www.glamox.com/global-marine/products/outdoor/navigation-lights-and-control-panels/3857001000)

#### Wiring

* → `load.chart` — captive

  * `cable.cabin.chart.neg` — `dist.sw.lights.term.neg.chart` → `load.chart.term.neg`
  * `cable.cabin.chart.pos` — `dist.sw.lights.term.pos.chart` → `load.chart.term.pos`
* → `load.down` — captive

  * `cable.cabin.down.neg` — `dist.sw.lights.term.neg.down` → `load.down.term.neg`
  * `cable.cabin.down.pos` — `dist.sw.lights.term.pos.down` → `load.down.term.pos`
* → `load.mast` — ISO 0.75 mm² / ABYC 18 AWG

  * `cable.mast.arw.pos` — `switch.mast.pin-5` → `load.mast.term.pos.arw`
  * `cable.mast.neg` — `dist.sw.lights.term.neg.mast` → `load.mast.term.neg`
  * `cable.mast.tri.pos` — `switch.mast.pin-2` → `load.mast.term.pos.tri`
* → `load.side` — ISO 0.75 mm² / ABYC 18 AWG

  * `cable.side.neg` — `dist.sw.lights.term.neg.side` → `load.side.term.neg`
  * `cable.side.pos` — `switch.deck.pin-2` → `load.side.term.pos`
* → `load.stern` — ISO 0.75 mm² / ABYC 18 AWG

  * `cable.stern.neg` — `dist.sw.lights.term.neg.stern` → `load.stern.term.neg`
  * `cable.stern.pos` — `switch.deck.pin-5` → `load.stern.term.pos`
* → `switch.deck` — ISO 0.75 mm² / ABYC 18 AWG

  * `cable.deck.feed.side.1` — `dist.sw.lights.term.pos.side` → `switch.deck.pin-4`
  * `cable.deck.feed.side.3` — `dist.sw.lights.term.pos.side` → `switch.deck.pin-6`
  * `cable.deck.feed.stern` — `dist.sw.lights.term.pos.stern` → `switch.deck.pin-1`
* → `switch.mast` — ISO 0.75 mm² / ABYC 18 AWG

  * `cable.mast.feed.arw` — `dist.sw.lights.term.pos.arw` → `switch.mast.pin-6`
  * `cable.mast.feed.tri` — `dist.sw.lights.term.pos.tri` → `switch.mast.pin-1`

---

### `dist.sw.navcom` — NAV/COM

#### Currents & Fuses

* `load.ais`

  * I 2.0 / 0.2 / –
  * `fuse.sw.navcom.ais` — 3 A [Blue Sea 5237](https://www.bluesea.com/products/5237/ATO___ATC_Fuse_-_3_Amp)
* `load.gps`

  * P 7.3 / 5.0 / –
  * `fuse.sw.navcom.gps` — 7.5 A [Blue Sea 5240](https://www.bluesea.com/products/5240/ATO___ATC_Fuse_-_7.5_Amp)
* `load.n2k`

  * I 0.4 / 0.1 / 0.1
  * `fuse.sw.navcom.n2k` — 1 A [Blue Sea 5235](https://www.bluesea.com/products/5235/ATO___ATC_Fuse_-_1_Amp)
* `load.rte`

  * I 0.1 / – / 0
  * `fuse.sw.navcom.rte` — 1 A [Blue Sea 5235](https://www.bluesea.com/products/5235/ATO___ATC_Fuse_-_1_Amp)
* `load.vhf`

  * I 5.0 / 0.9 / 0.6
  * `fuse.sw.navcom.vhf` — 7.5 A [Blue Sea 5240](https://www.bluesea.com/products/5240/ATO___ATC_Fuse_-_7.5_Amp)

#### BOM

* `dist.sw.navcom` — [Blue Sea 5025](https://www.bluesea.com/products/5025/ST_Blade_Fuse_Block_-_6_Circuits_with_Negative_Bus_and_Cover)

  * `load.depth` — [Raymarine E70148](https://www.raymarine.com/en-us/our-products/marine-instruments/i50-and-i60-series/i50-depth)
  * `load.gps` — [Raymarine E70634](https://www.raymarine.com/en-us/our-products/Chartplotters/axiom/axiom-plus)
  * `load.n2k` — [Actisense A2K-SBN-1](https://actisense.com/products/a2k-sbn-1)
  * `load.rte` — [Echomax Active-XS](https://www.echomax.co.uk/active-xs)
  * `load.vhf` — [Standard Horizon GX2410GPS](https://standardhorizon.com/product-detail.aspx?Model=GX2410GPS&CatName=Fixed%20Mount%20VHF)

    * `cable.rf.vhf-to-ais` — [em-trak B900/S100/S300 VHF Accessory Cable](https://em-trak.com/accessory-b900-s100-s300-vhf-accessory-cable)
  * `switch.ais` — [Blue Sea 4150](https://www.bluesea.com/products/4150/WeatherDeck_Toggle_Switch_SPST_-_ON-OFF)

    * `load.ais` — [em-trak B923](https://em-trak.com/b900-series)

      * `antenna.vhf` — [Shakespeare 5215](https://shakespeare-marine.com/product/classic-vhf-antennas)

#### Wiring

* `cable.rf`

  * `cable.rf.ais-antenna` — RG-8X; Lmax CG-580 15 m — `load.ais.term.rf.out` → `antenna.vhf.term.rf`
  * `cable.rf.vhf-to-ais` — [em-trak accessory cable](https://em-trak.com/accessory-b900-s100-s300-vhf-accessory-cable) — `load.vhf.term.rf` → `load.ais.term.rf.in`
* → `load.ais` — captive

  * `cable.ais.neg` — `dist.sw.navcom.term.neg.ais` → `load.ais.term.neg`
  * `cable.ais.pos` — `switch.ais.pin-3` → `load.ais.term.pos`
* → `load.gps` — captive; Lmax ISO 25.2 m / MFR 8 m

  * `cable.gps.neg` — `dist.sw.navcom.term.neg.gps` → `load.gps.term.neg`
  * `cable.gps.pos` — `dist.sw.navcom.term.pos.gps` → `load.gps.term.pos`
* → `load.n2k` — captive

  * `cable.n2k.neg` — `dist.sw.navcom.term.neg.n2k` → `load.n2k.term.neg`
  * `cable.n2k.pos` — `dist.sw.navcom.term.pos.n2k` → `load.n2k.term.pos`
  * `cable.n2k.drop`

    * `cable.n2k.drop.ais` — [Actisense A2K-TDC-0M25](https://actisense.com/products/a2k-tdc)
    * `cable.n2k.drop.depth` — [Raymarine A06045 adaptor](https://www.raymarine.com/en-us/our-products/networking-and-accessories/seatalk-ng-and-nmea-2000/nmea-2000-devicenet-female-to-seatalk-ng-spur-female-adaptor-cables)
    * `cable.n2k.drop.gps` — [Raymarine A06045 adaptor](https://www.raymarine.com/en-us/our-products/networking-and-accessories/seatalk-ng-and-nmea-2000/nmea-2000-devicenet-female-to-seatalk-ng-spur-female-adaptor-cables)
    * `cable.n2k.drop.vhf` — [Actisense A2K-TDC-0M25](https://actisense.com/products/a2k-tdc)
* → `load.rte` — ISO 0.75 mm² / ABYC 18 AWG

  * `cable.rte.neg` — `dist.sw.navcom.term.neg.rte` → `load.rte.term.neg`
  * `cable.rte.pos` — `dist.sw.navcom.term.pos.rte` → `load.rte.term.pos`
* → `load.vhf` — ISO 0.75 mm² / ABYC 18 AWG

  * `cable.vhf.neg` — `dist.sw.navcom.term.neg.vhf` → `load.vhf.term.neg`
  * `cable.vhf.pos` — `dist.sw.navcom.term.pos.vhf` → `load.vhf.term.pos`
* → `switch.ais` — ISO 0.75 mm² / ABYC 18 AWG

  * `cable.feed.ais` — `dist.sw.navcom.term.pos.ais` → `switch.ais.pin-2`

---

### `dist.batt.reserve` — MRBF Reserve

#### Currents & Fuses

* `dist.ao.reserve`

  * I 12.8 / 0.5 / 0
  * `fuse.batt.reserve`
* `dist.sw.lights` *Selector = 2*

  * I 0.8 / 0.3 / 0.3
  * `fuse.batt.reserve`
* `dist.sw.navcom` *Selector = 2*

  * I 8.2 / 0.9 / 0.7
  * `fuse.batt.reserve`

#### BOM

* `batt.reserve` — [Victron Energy Lithium SuperPack 12,8/100](https://www.victronenergy.com/batteries/12,8v-lithium-superpack)

  * `dist.batt.reserve` — [Blue Sea 5191](https://www.bluesea.com/products/5191/MRBF_Terminal_Fuse_Block_-_30_to_300A)

    * `fuse.batt.reserve` — [Blue Sea 5178](https://www.bluesea.com/products/5178/MRBF_Terminal_Fuse_-_60A)
    * `fuse.batt.reserve.lights` — [Blue Sea 5175](https://www.bluesea.com/products/5175/MRBF_Terminal_Fuse_-_30A)
    * `fuse.batt.reserve.navcom` — [Blue Sea 5175](https://www.bluesea.com/products/5175/MRBF_Terminal_Fuse_-_30A)

#### Wiring

* → `dist.ao.reserve` — ISO 6 mm² / ABYC 10 AWG; Lmax ISO 2.4 m / ABYC 2.5 m

  * `cable.main.reserve.neg` — `batt.reserve.term.neg` → `dist.ao.reserve.term.neg`
  * `cable.main.reserve.pos` — `dist.batt.reserve.term.load` → `dist.ao.reserve.term.pos`

---

### `dist.ao.reserve` — Always-on Reserve

#### Currents & Fuses

* `combiner` (control)

  * I 0.3 / 0.2 / –
  * `fuse.ao.reserve.combiner` — 1 A [Blue Sea 5235](https://www.bluesea.com/products/5235/ATO___ATC_Fuse_-_1_Amp)
* `load.tiller`

  * I 5 / 2 / 0.1
  * `fuse.ao.reserve.tiller` — 10 A [Blue Sea 5241](https://www.bluesea.com/products/5241/ATO___ATC_Fuse_-_10_Amp)
* `load.usb.r`

  * I 2.5 / 0.5 / –
  * `fuse.ao.reserve.usb` — 3 A [Blue Sea 5237](https://www.bluesea.com/products/5237/ATO___ATC_Fuse_-_3_Amp)
* `pv.ctrl.reserve`

  * I 5.7 / – / –
  * `fuse.ao.reserve.pv` — 10 A [Blue Sea 5241](https://www.bluesea.com/products/5241/ATO___ATC_Fuse_-_10_Amp)
* `socket.12v.reserve`

  * I 5 / – / –
  * `fuse.ao.reserve.socket` — 5 A [Blue Sea 5239](https://www.bluesea.com/products/5239/ATO___ATC_Fuse_-_5_Amp)

#### BOM

* `dist.ao.reserve` — [Blue Sea 5025](https://www.bluesea.com/products/5025/ST_Blade_Fuse_Block_-_6_Circuits_with_Negative_Bus_and_Cover)

  * `combiner` — [Victron Cyrix-Li-ct 12/24-120](https://www.victronenergy.com/battery-isolators-and-combiners/cyrix-battery-combiners)
  * `load.tiller` — [Raymarine A12004](https://www.raymarine.com/en-us/our-products/boat-autopilots/autopilot-packs/st1000-st2000)

    * `socket.tiller` — [Raymarine D338](https://www.raymarine.com)
  * `load.usb.r` — [Blue Sea 1045](https://www.bluesea.com/products/1045/12_24V_DC_Dual_USB_Charger_4.8A_with_Intelligent_Device_Recognition)
  * `pv.ctrl.reserve` — [Victron SCC075010060R](https://www.victronenergy.com/solar-charge-controllers/smartsolar-mppt-75-10-75-15-100-15-100-20)

    * `pv.panel.reserve` — [SunWare SW-40183](https://en.sunware.solar/produkte/solarmodul/197)
  * `socket.12v.reserve` — [Blue Sea 1011](https://www.bluesea.com/products/1011/Dash_Socket_12V_DC_with_Watertight_Cap)

#### Wiring

* `cable.subfeed.reserve.pos` — `dist.ao.reserve.term.pos` → `selector.house.term.2` — ISO 6 mm² / ABYC 10 AWG
* → `combiner` (control) — ISO 0.75 mm² / ABYC 18 AWG

  * `cable.combiner.85` — `dist.ao.reserve.term.pos.combiner` → `combiner.term.85`
  * `cable.combiner.86` — `dist.ao.reserve.term.neg` → `combiner.term.86`
* → `load.tiller` — ISO 2.5 mm² / ABYC 14 AWG; Lmax ISO 4.9 m / ABYC 4.3 m / MFR 4 m

  * `cable.tiller.neg` — `dist.ao.reserve.term.neg.tiller` → `socket.tiller.term.pin2`
  * `cable.tiller.pos` — `dist.ao.reserve.term.pos.tiller` → `socket.tiller.term.pin1`
* → `load.usb.r` — ISO 0.75 mm² / ABYC 18 AWG

  * `cable.usb.r.neg` — `dist.ao.reserve.term.neg.usb` → `load.usb.r.term.neg`
  * `cable.usb.r.pos` — `dist.ao.reserve.term.pos.usb` → `load.usb.r.term.pos`
* ← `pv.ctrl.reserve` — ISO 1.5 mm² / ABYC 16 AWG; Lmax ABYC 1 m

  * `cable.pv.ctrl.reserve.neg` — `pv.ctrl.reserve.term.out.neg` → `dist.ao.reserve.term.neg.pv-reserve`
  * `cable.pv.ctrl.reserve.pos` — `pv.ctrl.reserve.term.out.pos` → `dist.ao.reserve.term.pos.pv-reserve`
  * ← `pv.panel.reserve` — ISO 1.5 mm² / ABYC 16 AWG; Lmax ISO 4.8 m / ABYC 4.2 m

    * `cable.pv.panel.reserve.neg` — `pv.panel.reserve.term.neg` → `pv.ctrl.reserve.term.in.neg`
    * `cable.pv.panel.reserve.pos` — `pv.panel.reserve.term.pos` → `pv.ctrl.reserve.term.in.pos`
* → `socket.12v.reserve` — ISO 0.75 mm² / ABYC 18 AWG

  * `cable.socket.r.neg` — `dist.ao.reserve.term.neg.socket` → `socket.12v.reserve.term.neg`
  * `cable.socket.r.pos` — `dist.ao.reserve.term.pos.socket` → `socket.12v.reserve.term.pos`
---

## Details

### Primary

#### BOM

* `combiner` — [Victron Energy Cyrix-Li-ct 12/24-120](https://www.victronenergy.com/battery-isolators-and-combiners/cyrix-battery-combiners)
* `selector.house` — [Blue Sea 6008 Selector Switch](https://www.bluesea.com/products/6008/m-Series_Selector_3_Position_Battery_Switch_-_Red)

#### Wiring

* Common negative bridge — ISO 6 mm² / ABYC 10 AWG

  * `neg-bridge-reserve-house.1` — `dist.ao.reserve.term.neg` → `dist.sw.lights.term.neg`
  * `neg-bridge-reserve-house.2` — `dist.sw.lights.term.neg` → `dist.sw.navcom.term.neg`
  * `neg-bridge-reserve-house.3` — `dist.sw.navcom.term.neg` → `dist.ao.house.term.neg`
* → `dist.ao.house` — ISO 6 mm² / ABYC 10 AWG

  * `cable.subfeed.combiner.87` — `dist.ao.house.term.pos` → `combiner.term.87`
* → `dist.ao.reserve` — ISO 6 mm² / ABYC 10 AWG

  * `cable.subfeed.combiner.30` — `dist.ao.reserve.term.pos` → `combiner.term.30`
* → `dist.sw.lights` — ISO 6 mm² / ABYC 10 AWG

  * `cable.subfeed.lights.pos` — `selector.house.term.output` → `dist.sw.lights.term.pos`
* → `dist.sw.navcom` — ISO 6 mm² / ABYC 10 AWG

  * `cable.subfeed.navcom.pos` — `selector.house.term.output` → `dist.sw.navcom.term.pos`

---

### `dist.batt.house` — MRBF House

#### Currents & Fuses

* `dist.ao.house`

  * I 6.8 / 0.5 / 0
  * `fuse.batt.house`
* `dist.sw.lights` *Selector = 1*

  * I 0.8 / 0.3 / 0.3
  * `fuse.batt.house`
* `dist.sw.navcom` *Selector = 1*

  * I 8.2 / 0.9 / 0.7
  * `fuse.batt.house`

#### BOM

* `batt.house` — [Victron Energy Lithium SuperPack 12,8/100](https://www.victronenergy.com/batteries/12,8v-lithium-superpack)

  * `dist.batt.house` — [Blue Sea 5191](https://www.bluesea.com/products/5191/MRBF_Terminal_Fuse_Block_-_30_to_300A)

    * `fuse.batt.house` — [Blue Sea 5178](https://www.bluesea.com/products/5178/MRBF_Terminal_Fuse_-_60A)
    * `fuse.batt.house.lights` — [Blue Sea 5175](https://www.bluesea.com/products/5175/MRBF_Terminal_Fuse_-_30A)
    * `fuse.batt.house.navcom` — [Blue Sea 5175](https://www.bluesea.com/products/5175/MRBF_Terminal_Fuse_-_30A)

#### Wiring

* → `dist.ao.house` — ISO 6 mm² / ABYC 10 AWG; Lmax ISO 3.3 m / ABYC 3.3 m

  * `cable.main.house.neg` — `batt.house.term.neg` → `dist.ao.house.term.neg`
  * `cable.main.house.pos` — `dist.batt.house.term.load` → `dist.ao.house.term.pos`

---

### `dist.ao.house` — Always-on House

#### Currents & Fuses

* `load.bilge`

  * I 4.3 / – / –
  * `fuse.ao.house.bilge.auto` — 5 A [Blue Sea 5239](https://www.bluesea.com/products/5239/ATO___ATC_Fuse_-_5_Amp)
  * `fuse.ao.house.bilge.manual` — 5 A [Blue Sea 5239](https://www.bluesea.com/products/5239/ATO___ATC_Fuse_-_5_Amp)
* `load.usb.h`

  * I 2.5 / 0.5 / –
  * `fuse.ao.house.usb` — 3 A [Blue Sea 5237](https://www.bluesea.com/products/5237/ATO___ATC_Fuse_-_3_Amp)
* `pv.ctrl.emergency`

  * I 5 / – / –
  * `fuse.ao.house.pv-emergency` — 10 A [Blue Sea 5241](https://www.bluesea.com/products/5241/ATO___ATC_Fuse_-_10_Amp)
* `pv.ctrl.house`

  * I 5.7 / – / –
  * `fuse.ao.house.pv-house` — 10 A [Blue Sea 5241](https://www.bluesea.com/products/5241/ATO___ATC_Fuse_-_10_Amp)

#### BOM

* `dist.ao.house` — [Blue Sea 5025](https://www.bluesea.com/products/5025/ST_Blade_Fuse_Block_-_6_Circuits_with_Negative_Bus_and_Cover)

  * `load.usb.h` — [Blue Sea 1045](https://www.bluesea.com/products/1045/12_24V_DC_Dual_USB_Charger_4.8A_with_Intelligent_Device_Recognition)
  * `pv.ctrl.emergency` — [Victron SCC075010060R](https://www.victronenergy.com/solar-charge-controllers/smartsolar-mppt-75-10-75-15-100-15-100-20)

    * `pv.panel.emergency` — [SunWare RX-21052](https://en.sunware.solar/products/solarpanel/45)

      * `pv.panel.emergency.adapter` — [SunWare 30003111](https://en.sunware.solar/products/item_details/30003111)
  * `pv.ctrl.house` — [Victron SCC075010060R](https://www.victronenergy.com/solar-charge-controllers/smartsolar-mppt-75-10-75-15-100-15-100-20)

    * `pv.panel.house` — [SunWare SW-40183](https://en.sunware.solar/produkte/solarmodul/197)
  * `switch.bilge` — [Blue Sea 4150](https://www.bluesea.com/products/4150/WeatherDeck_Toggle_Switch_SPST_-_ON-OFF)

    * `load.bilge` — [Whale SS1212](https://docs.navico.com/view/177634415/8)

#### Wiring

* `cable.subfeed.house.pos` — `dist.ao.house.term.pos` → `selector.house.term.1` — ISO 6 mm² / ABYC 10 AWG
* → `load.bilge` — ISO 1.5 mm² / ABYC 16 AWG; Lmax ISO 3.6 m / ABYC 3.1 m

  * `cable.bilge.auto.pos` — `dist.ao.house.term.pos.bilge.auto` → `load.bilge.term.auto.pos`
  * `cable.bilge.manual.pos` — `switch.bilge.pin-2` → `load.bilge.term.manual.pos`
  * `cable.bilge.neg` — `dist.ao.house.term.neg.bilge` → `load.bilge.term.neg`
* → `load.usb.h` — ISO 0.75 mm² / ABYC 18 AWG

  * `cable.usb.h.neg` — `dist.ao.house.term.neg.usb` → `load.usb.h.term.neg`
  * `cable.usb.h.pos` — `dist.ao.house.term.pos.usb` → `load.usb.h.term.pos`
* ← `pv.ctrl.emergency` — ISO 1.5 mm² / ABYC 16 AWG; Lmax ABYC 1 m

  * `cable.pv.ctrl.emergency.neg` — `pv.ctrl.emergency.term.out.neg` → `dist.ao.house.term.neg.pv-emergency`
  * `cable.pv.ctrl.emergency.pos` — `pv.ctrl.emergency.term.out.pos` → `dist.ao.house.term.pos.pv-emergency`
  * ← `cable.pv.panel.emergency.adapter` — captive

    * `cable.pv.panel.emergency.adapter.neg` — `connector.pv.emergency.neg` → `pv.ctrl.emergency.term.in.neg`
    * `cable.pv.panel.emergency.adapter.pos` — `connector.pv.emergency.pos` → `pv.ctrl.emergency.term.in.pos`
  * ← `cable.pv.panel.emergency.pv` — captive

    * `cable.pv.panel.emergency.neg` — `pv.panel.emergency.term.neg` → `connector.pv.emergency.neg`
    * `cable.pv.panel.emergency.pos` — `pv.panel.emergency.term.pos` → `connector.pv.emergency.pos`
* ← `pv.ctrl.house` — ISO 1.5 mm² / ABYC 16 AWG; Lmax ABYC 1 m

  * `cable.pv.ctrl.house.neg` — `pv.ctrl.house.term.out.neg` → `dist.ao.house.term.neg.pv-house`
  * `cable.pv.ctrl.house.pos` — `pv.ctrl.house.term.out.pos` → `dist.ao.house.term.pos.pv-house`
  * ← `pv.panel.house` — ISO 1.5 mm² / ABYC 16 AWG; Lmax ISO 4.8 m / ABYC 4.2 m

    * `cable.pv.panel.house.neg` — `pv.panel.house.term.neg` → `pv.ctrl.house.term.in.neg`
    * `cable.pv.panel.house.pos` — `pv.panel.house.term.pos` → `pv.ctrl.house.term.in.pos`
* → `switch.bilge` — ISO 1.5 mm² / ABYC 16 AWG

  * `cable.feed.bilge.manual.pos` — `dist.ao.house.term.pos.bilge.manual` → `switch.bilge.pin-2`

---

### `dist.sw.lights` — LIGHTS

#### Currents & Fuses

* `load.chart`

  * I 0.2 / – / 0.1
  * `fuse.sw.lights.chart` — 1 A [Blue Sea 5235](https://www.bluesea.com/products/5235/ATO___ATC_Fuse_-_1_Amp)
* `load.down`

  * I 0.3 / – / 0.1
  * `fuse.sw.lights.down` — 1 A [Blue Sea 5235](https://www.bluesea.com/products/5235/ATO___ATC_Fuse_-_1_Amp)
* `load.mast` (TRI / ARW)

  * P 1.9 / 1.0
  * `fuse.sw.lights.arw` — 1 A [Blue Sea 5235](https://www.bluesea.com/products/5235/ATO___ATC_Fuse_-_1_Amp)
  * `fuse.sw.lights.tri` — 1 A [Blue Sea 5235](https://www.bluesea.com/products/5235/ATO___ATC_Fuse_-_1_Amp)
* `load.side`

  * P 2.3
  * `fuse.sw.lights.side` — 1 A [Blue Sea 5235](https://www.bluesea.com/products/5235/ATO___ATC_Fuse_-_1_Amp)
* `load.stern`

  * P 1.0
  * `fuse.sw.lights.stern` — 1 A [Blue Sea 5235](https://www.bluesea.com/products/5235/ATO___ATC_Fuse_-_1_Amp)

#### BOM

* `dist.sw.lights` — [Blue Sea 5025](https://www.bluesea.com/products/5025/ST_Blade_Fuse_Block_-_6_Circuits_with_Negative_Bus_and_Cover)

  * `load.chart` — [Hella marine 2JA 343 720-622](https://www.hellamarine.com/shop/interior-exterior-lamps/reading-lamps/flexi-spot-led-chart-table-lamp)
  * `load.down` — [Hella marine 2JA 959 950-121](https://www.hellamarine.com/shop/interior-exterior-lamps/downlights/euroled130-surface-mount-round-downlights)
  * `switch.deck` — [Blue Sea 4155](https://www.bluesea.com/products/4155/WeatherDeck_Toggle_Switch_DPDT_-_ON-OFF-ON)

    * `load.side` — [AquaSignal 3853001000](https://www.glamox.com/global-marine/products/outdoor/navigation-lights-and-control-panels/3853001000)
    * `load.stern` — [AquaSignal 3852001000](https://www.glamox.com/global-marine/products/outdoor/navigation-lights-and-control-panels/3852001000)
  * `switch.mast` — [Blue Sea 4155](https://www.bluesea.com/products/4155/WeatherDeck_Toggle_Switch_DPDT_-_ON-OFF-ON)

    * `load.mast` — [AquaSignal 3857001000](https://www.glamox.com/global-marine/products/outdoor/navigation-lights-and-control-panels/3857001000)

#### Wiring

* → `load.chart` — captive

  * `cable.cabin.chart.neg` — `dist.sw.lights.term.neg.chart` → `load.chart.term.neg`
  * `cable.cabin.chart.pos` — `dist.sw.lights.term.pos.chart` → `load.chart.term.pos`
* → `load.down` — captive

  * `cable.cabin.down.neg` — `dist.sw.lights.term.neg.down` → `load.down.term.neg`
  * `cable.cabin.down.pos` — `dist.sw.lights.term.pos.down` → `load.down.term.pos`
* → `load.mast` — ISO 0.75 mm² / ABYC 18 AWG

  * `cable.mast.arw.pos` — `switch.mast.pin-5` → `load.mast.term.pos.arw`
  * `cable.mast.neg` — `dist.sw.lights.term.neg.mast` → `load.mast.term.neg`
  * `cable.mast.tri.pos` — `switch.mast.pin-2` → `load.mast.term.pos.tri`
* → `load.side` — ISO 0.75 mm² / ABYC 18 AWG

  * `cable.side.neg` — `dist.sw.lights.term.neg.side` → `load.side.term.neg`
  * `cable.side.pos` — `switch.deck.pin-2` → `load.side.term.pos`
* → `load.stern` — ISO 0.75 mm² / ABYC 18 AWG

  * `cable.stern.neg` — `dist.sw.lights.term.neg.stern` → `load.stern.term.neg`
  * `cable.stern.pos` — `switch.deck.pin-5` → `load.stern.term.pos`
* → `switch.deck` — ISO 0.75 mm² / ABYC 18 AWG

  * `cable.deck.feed.side.1` — `dist.sw.lights.term.pos.side` → `switch.deck.pin-4`
  * `cable.deck.feed.side.3` — `dist.sw.lights.term.pos.side` → `switch.deck.pin-6`
  * `cable.deck.feed.stern` — `dist.sw.lights.term.pos.stern` → `switch.deck.pin-1`
* → `switch.mast` — ISO 0.75 mm² / ABYC 18 AWG

  * `cable.mast.feed.arw` — `dist.sw.lights.term.pos.arw` → `switch.mast.pin-6`
  * `cable.mast.feed.tri` — `dist.sw.lights.term.pos.tri` → `switch.mast.pin-1`

---

### `dist.sw.navcom` — NAV/COM

#### Currents & Fuses

* `load.ais`

  * I 2.0 / 0.2 / –
  * `fuse.sw.navcom.ais` — 3 A [Blue Sea 5237](https://www.bluesea.com/products/5237/ATO___ATC_Fuse_-_3_Amp)
* `load.gps`

  * P 7.3 / 5.0 / –
  * `fuse.sw.navcom.gps` — 7.5 A [Blue Sea 5240](https://www.bluesea.com/products/5240/ATO___ATC_Fuse_-_7.5_Amp)
* `load.n2k`

  * I 0.4 / 0.1 / 0.1
  * `fuse.sw.navcom.n2k` — 1 A [Blue Sea 5235](https://www.bluesea.com/products/5235/ATO___ATC_Fuse_-_1_Amp)
* `load.rte`

  * I 0.1 / – / 0
  * `fuse.sw.navcom.rte` — 1 A [Blue Sea 5235](https://www.bluesea.com/products/5235/ATO___ATC_Fuse_-_1_Amp)
* `load.vhf`

  * I 5.0 / 0.9 / 0.6
  * `fuse.sw.navcom.vhf` — 7.5 A [Blue Sea 5240](https://www.bluesea.com/products/5240/ATO___ATC_Fuse_-_7.5_Amp)

#### BOM

* `dist.sw.navcom` — [Blue Sea 5025](https://www.bluesea.com/products/5025/ST_Blade_Fuse_Block_-_6_Circuits_with_Negative_Bus_and_Cover)

  * `load.depth` — [Raymarine E70148](https://www.raymarine.com/en-us/our-products/marine-instruments/i50-and-i60-series/i50-depth)
  * `load.gps` — [Raymarine E70634](https://www.raymarine.com/en-us/our-products/Chartplotters/axiom/axiom-plus)
  * `load.n2k` — [Actisense A2K-SBN-1](https://actisense.com/products/a2k-sbn-1)
  * `load.rte` — [Echomax Active-XS](https://www.echomax.co.uk/active-xs)
  * `load.vhf` — [Standard Horizon GX2410GPS](https://standardhorizon.com/product-detail.aspx?Model=GX2410GPS&CatName=Fixed%20Mount%20VHF)

    * `cable.rf.vhf-to-ais` — [em-trak B900/S100/S300 VHF Accessory Cable](https://em-trak.com/accessory-b900-s100-s300-vhf-accessory-cable)
  * `switch.ais` — [Blue Sea 4150](https://www.bluesea.com/products/4150/WeatherDeck_Toggle_Switch_SPST_-_ON-OFF)

    * `load.ais` — [em-trak B923](https://em-trak.com/b900-series)

      * `antenna.vhf` — [Shakespeare 5215](https://shakespeare-marine.com/product/classic-vhf-antennas)

#### Wiring

* `cable.rf`

  * `cable.rf.ais-antenna` — RG-8X; Lmax CG-580 15 m — `load.ais.term.rf.out` → `antenna.vhf.term.rf`
  * `cable.rf.vhf-to-ais` — [em-trak accessory cable](https://em-trak.com/accessory-b900-s100-s300-vhf-accessory-cable) — `load.vhf.term.rf` → `load.ais.term.rf.in`
* → `load.ais` — captive

  * `cable.ais.neg` — `dist.sw.navcom.term.neg.ais` → `load.ais.term.neg`
  * `cable.ais.pos` — `switch.ais.pin-3` → `load.ais.term.pos`
* → `load.gps` — captive; Lmax ISO 25.2 m / MFR 8 m

  * `cable.gps.neg` — `dist.sw.navcom.term.neg.gps` → `load.gps.term.neg`
  * `cable.gps.pos` — `dist.sw.navcom.term.pos.gps` → `load.gps.term.pos`
* → `load.n2k` — captive

  * `cable.n2k.neg` — `dist.sw.navcom.term.neg.n2k` → `load.n2k.term.neg`
  * `cable.n2k.pos` — `dist.sw.navcom.term.pos.n2k` → `load.n2k.term.pos`
  * `cable.n2k.drop`

    * `cable.n2k.drop.ais` — [Actisense A2K-TDC-0M25](https://actisense.com/products/a2k-tdc)
    * `cable.n2k.drop.depth` — [Raymarine A06045 adaptor](https://www.raymarine.com/en-us/our-products/networking-and-accessories/seatalk-ng-and-nmea-2000/nmea-2000-devicenet-female-to-seatalk-ng-spur-female-adaptor-cables)
    * `cable.n2k.drop.gps` — [Raymarine A06045 adaptor](https://www.raymarine.com/en-us/our-products/networking-and-accessories/seatalk-ng-and-nmea-2000/nmea-2000-devicenet-female-to-seatalk-ng-spur-female-adaptor-cables)
    * `cable.n2k.drop.vhf` — [Actisense A2K-TDC-0M25](https://actisense.com/products/a2k-tdc)
* → `load.rte` — ISO 0.75 mm² / ABYC 18 AWG

  * `cable.rte.neg` — `dist.sw.navcom.term.neg.rte` → `load.rte.term.neg`
  * `cable.rte.pos` — `dist.sw.navcom.term.pos.rte` → `load.rte.term.pos`
* → `load.vhf` — ISO 0.75 mm² / ABYC 18 AWG

  * `cable.vhf.neg` — `dist.sw.navcom.term.neg.vhf` → `load.vhf.term.neg`
  * `cable.vhf.pos` — `dist.sw.navcom.term.pos.vhf` → `load.vhf.term.pos`
* → `switch.ais` — ISO 0.75 mm² / ABYC 18 AWG

  * `cable.feed.ais` — `dist.sw.navcom.term.pos.ais` → `switch.ais.pin-2`

---

### `dist.batt.reserve` — MRBF Reserve

#### Currents & Fuses

* `dist.ao.reserve`

  * I 12.8 / 0.5 / 0
  * `fuse.batt.reserve`
* `dist.sw.lights` *Selector = 2*

  * I 0.8 / 0.3 / 0.3
  * `fuse.batt.reserve`
* `dist.sw.navcom` *Selector = 2*

  * I 8.2 / 0.9 / 0.7
  * `fuse.batt.reserve`

#### BOM

* `batt.reserve` — [Victron Energy Lithium SuperPack 12,8/100](https://www.victronenergy.com/batteries/12,8v-lithium-superpack)

  * `dist.batt.reserve` — [Blue Sea 5191](https://www.bluesea.com/products/5191/MRBF_Terminal_Fuse_Block_-_30_to_300A)

    * `fuse.batt.reserve` — [Blue Sea 5178](https://www.bluesea.com/products/5178/MRBF_Terminal_Fuse_-_60A)
    * `fuse.batt.reserve.lights` — [Blue Sea 5175](https://www.bluesea.com/products/5175/MRBF_Terminal_Fuse_-_30A)
    * `fuse.batt.reserve.navcom` — [Blue Sea 5175](https://www.bluesea.com/products/5175/MRBF_Terminal_Fuse_-_30A)

#### Wiring

* → `dist.ao.reserve` — ISO 6 mm² / ABYC 10 AWG; Lmax ISO 2.4 m / ABYC 2.5 m

  * `cable.main.reserve.neg` — `batt.reserve.term.neg` → `dist.ao.reserve.term.neg`
  * `cable.main.reserve.pos` — `dist.batt.reserve.term.load` → `dist.ao.reserve.term.pos`

---

### `dist.ao.reserve` — Always-on Reserve

#### Currents & Fuses

* `combiner` (control)

  * I 0.3 / 0.2 / –
  * `fuse.ao.reserve.combiner` — 1 A [Blue Sea 5235](https://www.bluesea.com/products/5235/ATO___ATC_Fuse_-_1_Amp)
* `load.tiller`

  * I 5 / 2 / 0.1
  * `fuse.ao.reserve.tiller` — 10 A [Blue Sea 5241](https://www.bluesea.com/products/5241/ATO___ATC_Fuse_-_10_Amp)
* `load.usb.r`

  * I 2.5 / 0.5 / –
  * `fuse.ao.reserve.usb` — 3 A [Blue Sea 5237](https://www.bluesea.com/products/5237/ATO___ATC_Fuse_-_3_Amp)
* `pv.ctrl.reserve`

  * I 5.7 / – / –
  * `fuse.ao.reserve.pv` — 10 A [Blue Sea 5241](https://www.bluesea.com/products/5241/ATO___ATC_Fuse_-_10_Amp)
* `socket.12v.reserve`

  * I 5 / – / –
  * `fuse.ao.reserve.socket` — 5 A [Blue Sea 5239](https://www.bluesea.com/products/5239/ATO___ATC_Fuse_-_5_Amp)

#### BOM

* `dist.ao.reserve` — [Blue Sea 5025](https://www.bluesea.com/products/5025/ST_Blade_Fuse_Block_-_6_Circuits_with_Negative_Bus_and_Cover)

  * `combiner` — [Victron Cyrix-Li-ct 12/24-120](https://www.victronenergy.com/battery-isolators-and-combiners/cyrix-battery-combiners)
  * `load.tiller` — [Raymarine A12004](https://www.raymarine.com/en-us/our-products/boat-autopilots/autopilot-packs/st1000-st2000)

    * `socket.tiller` — [Raymarine D338](https://www.raymarine.com)
  * `load.usb.r` — [Blue Sea 1045](https://www.bluesea.com/products/1045/12_24V_DC_Dual_USB_Charger_4.8A_with_Intelligent_Device_Recognition)
  * `pv.ctrl.reserve` — [Victron SCC075010060R](https://www.victronenergy.com/solar-charge-controllers/smartsolar-mppt-75-10-75-15-100-15-100-20)

    * `pv.panel.reserve` — [SunWare SW-40183](https://en.sunware.solar/produkte/solarmodul/197)
  * `socket.12v.reserve` — [Blue Sea 1011](https://www.bluesea.com/products/1011/Dash_Socket_12V_DC_with_Watertight_Cap)

#### Wiring

* `cable.subfeed.reserve.pos` — `dist.ao.reserve.term.pos` → `selector.house.term.2` — ISO 6 mm² / ABYC 10 AWG
* → `combiner` (control) — ISO 0.75 mm² / ABYC 18 AWG

  * `cable.combiner.85` — `dist.ao.reserve.term.pos.combiner` → `combiner.term.85`
  * `cable.combiner.86` — `dist.ao.reserve.term.neg` → `combiner.term.86`
* → `load.tiller` — ISO 2.5 mm² / ABYC 14 AWG; Lmax ISO 4.9 m / ABYC 4.3 m / MFR 4 m

  * `cable.tiller.neg` — `dist.ao.reserve.term.neg.tiller` → `socket.tiller.term.pin2`
  * `cable.tiller.pos` — `dist.ao.reserve.term.pos.tiller` → `socket.tiller.term.pin1`
* → `load.usb.r` — ISO 0.75 mm² / ABYC 18 AWG

  * `cable.usb.r.neg` — `dist.ao.reserve.term.neg.usb` → `load.usb.r.term.neg`
  * `cable.usb.r.pos` — `dist.ao.reserve.term.pos.usb` → `load.usb.r.term.pos`
* ← `pv.ctrl.reserve` — ISO 1.5 mm² / ABYC 16 AWG; Lmax ABYC 1 m

  * `cable.pv.ctrl.reserve.neg` — `pv.ctrl.reserve.term.out.neg` → `dist.ao.reserve.term.neg.pv-reserve`
  * `cable.pv.ctrl.reserve.pos` — `pv.ctrl.reserve.term.out.pos` → `dist.ao.reserve.term.pos.pv-reserve`
  * ← `pv.panel.reserve` — ISO 1.5 mm² / ABYC 16 AWG; Lmax ISO 4.8 m / ABYC 4.2 m

    * `cable.pv.panel.reserve.neg` — `pv.panel.reserve.term.neg` → `pv.ctrl.reserve.term.in.neg`
    * `cable.pv.panel.reserve.pos` — `pv.panel.reserve.term.pos` → `pv.ctrl.reserve.term.in.pos`
* → `socket.12v.reserve` — ISO 0.75 mm² / ABYC 18 AWG

  * `cable.socket.r.neg` — `dist.ao.reserve.term.neg.socket` → `socket.12v.reserve.term.neg`
  * `cable.socket.r.pos` — `dist.ao.reserve.term.pos.socket` → `socket.12v.reserve.term.pos`
