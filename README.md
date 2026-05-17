# VMI Systems — Vendor Managed Inventory

> *From manual replenishment to automated inventory intelligence — built across two of Denmark's largest industrial distributors.*

---

## Impact

Designed, implemented and optimised VMI solutions across **Lemvigh-Müller** and **Sanistål** — two of Denmark's largest industrial distributors and direct competitors.

Four different technologies. Four separate implementations. One consistent outcome: warehouse staff stop managing replenishment manually, and the business gains real-time visibility into consumption patterns.

---

## Implementations

### 🔵 ESL — Electronic Shelf Label
**Client:** Lemvigh-Müller · **Hardware & embedded software:** [PDI Digital](https://www.pdi-digital.com/)

Two-button label mounted directly on the shelf. Button 1 triggers an order line. Button 2 confirms delivery and resets. Orders pool by site via REST API, convert to CSV/EDI and push to SAP automatically.

Replenishment: 1x weekly via mercher who refills stock and handles signal loss, unit issues and demand changes on-site.

→ [See use case documentation](docs/ESL%20UseCase.pdf)
→ [Live on lemu.dk](https://www.lemu.dk/da/services/levering-og-lagerstyring/smartlager/elektronisk-hyldeforkant)

---

### ⚖️ SmartVægte™ — Weight-based VMI
**Client:** Lemvigh-Müller · **Hardware:** [DigiSens](https://digisens.ch/en/)

Shelf sensors monitor stock continuously. Order triggered automatically when stock falls below a pre-set minimum weight — based on min/max interval logic. No human action required. Range: 4kg to 1000kg per sensor.

Replenishment: 1x weekly via mercher.

→ [Live on lemu.dk](https://www.lemu.dk/da/services/levering-og-lagerstyring/smartlager/smartvaegte)

---

### 🤖 Vending Automater — Controlled Issue
**Clients:** Lemvigh-Müller · Sanistål · **Hardware:** [IVM Micro Solutions](https://www.ivmsolutions.com/) · [AutoCrib](https://www.autocrib.com/)

Locked dispensing units with RFID access control. Employees access items using existing access cards or PIN. System logs who takes what and when. Order triggered automatically based on min/max interval logic.

RFID readers programmed per installation: card type, frequency, output format (hex vs decimal).

Replenishment: 1x weekly via mercher.

---

### 📦 StockMaster
**Client:** Sanistål (now Ahlsell) · **Platform:** [CribMaster / Stanley Black & Decker](https://storage.stanleyblackanddecker.com/cribmaster)

VMI concept built on CribMaster technology. Order triggered based on min/max interval logic — generated as XML files from the CribMaster database. Sanistål won International Partner of the Year 2017 for this implementation — a proven, successful concept still live under the Ahlsell brand.

RFID access control programmed via [ELATEC](https://www.elatec-rfid.com/int/).

Replenishment: 1x weekly via mercher.

---

## Integration Patterns

| Solution | Integration | Order trigger | Replenishment |
|---|---|---|---|
| ESL | REST API → CSV/EDI → SAP | Button press | 1x weekly, mercher |
| SmartVægte™ | Weight sensor → site controller | Min/max interval | 1x weekly, mercher |
| Vending automater | RFID access log → ERP | Min/max interval | 1x weekly, mercher |
| StockMaster | CribMaster DB → XML files | Min/max interval | 1x weekly, mercher |

---

## The Decision Logic Behind It

The technology is the easy part. The hard part is knowing what goes in the machine.

### ABC Categorisation
Every customer implementation started with their item list and an ABC classification:

- **A** — must always be available
- **B** — include if capacity allows
- **C** — remove if space is needed

This forced customers to think about criticality — not just what they used, but what they could not afford to run out of.

### Capacity Calculation
Originally featured within CribMaster templates for StockMaster implementations at Sanistål — then re-invented and rebuilt to fit the AutoCrib solution at Lemvigh-Müller.

Built a dedicated Excel model that automatically calculated capacity fill rate per customer — room by room. Each room configured individually: some rooms hold 12 pairs, others 6. Almost entirely customer-specific.

### Item Database
Built a master item database mapping each physical room in each machine to a specific item — with max capacity defined per room. Enabled rapid configuration of new installations and consistent management of existing ones.

### Asset Management — Rental and Calibration
VMI infrastructure extended beyond consumable replenishment:

**Rental items** — tools and equipment lent to employees or contractors tracked by who has what, since when, and when due back. Automatic reminders. No lost assets or disputes.

**Calibrated instruments** — measuring instruments tracked by serial number, last calibration date, next due date, and certificate status. Implemented and live. All data captured and utilised.

This transforms VMI from a replenishment system into a **complete asset lifecycle platform** — covering acquisition, usage, maintenance, and return.

---

## The Business Case — Hidden Costs VMI Eliminates

Most organisations evaluate VMI on purchase price alone. That is the wrong number.

The real question is: what does the current process actually cost?

### Invoice Cost — DKK 1,000 per order

In a high-wage country like Denmark, the fully loaded cost of processing a single purchase order and its associated invoice is typically **DKK 1,000** — when all steps are included:

- Order creation and approval
- Goods receipt confirmation
- Invoice receipt and validation
- 3-way matching (PO / delivery / invoice)
- Bookkeeping and archiving
- Error correction and follow-up

With VMI, this entire process is replaced by a single consolidated weekly invoice per site. A customer with 200 individual order lines per week goes from 200 invoices to 1.

**200 order lines × DKK 1,000 = DKK 200,000 hidden cost per week — eliminated.**

### Walk & Wait Time

Every minute a skilled employee spends walking to find stock, waiting for a delivery, or searching for a missing item is a direct productivity loss. In industrial environments — production lines, workshops, offshore facilities — hourly rates of DKK 400–600 are not unusual for the people affected.

VMI ensures the right item is in the right place at the right time.

### Consumption Reduction — typically 15–25%

When items are freely accessible without control, overconsumption follows. Controlled access via RFID changes behaviour immediately and measurably.

Experience from implementations at Lemvigh-Müller and Sanistål/Ahlsell shows consistent consumption reductions of **15–25%** from access control and visibility alone. No process change required. Just accountability.

### Supplier Consolidation

VMI concentrates purchasing with one supplier across multiple categories — consumables, PPE, tools, spare parts, safety equipment. The effect: fewer suppliers to manage, higher volume per supplier, stronger negotiating position, and reduced procurement overhead across the entire indirect spend portfolio.

### The ROI Summary

| Cost driver | Manual process | With VMI |
|---|---|---|
| Invoice processing | DKK 1,000 per order | 1 consolidated invoice per site per week |
| Walk & wait time | Untracked, uncontrolled | Eliminated |
| Consumption | Baseline | 15–25% reduction |
| Supplier complexity | Multiple vendors, high overhead | Consolidated, lower cost to serve |
| Asset tracking | Manual or absent | Automated, documented, auditable |

The business case does not require optimistic assumptions. It requires honest accounting of what the current process actually costs.

→ [Full business case documentation](docs/BusinessCase.md)

---

## What This Actually Is

This is not just VMI implementation. It is the same pattern that appears across all NorthLogicLab work:

- Understand the domain deeply
- Build decision support that makes the complex manageable
- Document it so others can maintain and extend it
- Make the invisible visible

The same thinking that built these VMI solutions now drives [PTDE](https://github.com/jonbach2012-design/PackagingTenderDecisionEngine) and [Regulus](https://github.com/NorthLogicLab/Regulus).

---

## Documentation

**Lemvigh-Müller SmartLager™**
- [ESL — Elektronisk hyldeforkant](https://www.lemu.dk/da/services/levering-og-lagerstyring/smartlager/elektronisk-hyldeforkant)
- [SmartVægte™](https://www.lemu.dk/da/services/levering-og-lagerstyring/smartlager/smartvaegte)
- [Vending automater](https://www.lemu.dk/da/services/levering-og-lagerstyring/smartlager/smartautomater)

**Ahlsell / Sanistål**
- [StockMaster — Lagerstyring](https://www.ahlsell.dk/da/services/ahlsell-services/lagerstyring/stockmaster)

**Hardware & software partners**
- [PDI Digital](https://www.pdi-digital.com/) — ESL hardware & embedded software
- [DigiSens](https://digisens.ch/en/) — weight-based VMI hardware
- [AutoCrib](https://www.autocrib.com/) · [IVM Micro Solutions](https://www.ivmsolutions.com/) — vending automater
- [ELATEC](https://www.elatec-rfid.com/int/) — RFID reader software
- [CribMaster / Stanley Black & Decker](https://storage.stanleyblackanddecker.com/cribmaster) — StockMaster platform

**Project documentation**
- [ESL Use Case — System Architecture](docs/ESL%20UseCase.pdf)
- [Business Case — Hidden Costs VMI Eliminates](docs/BusinessCase.md)

---

## Status

All four solutions live in production — across Lemvigh-Müller's SmartLager™ network and Sanistål/Ahlsell's StockMaster programme, serving industrial customers across Denmark and abroad.

**From push to pull — in the market, not just the warehouse.**

In the early phase, VMI was a concept we had to explain and sell. Customers didn't know they needed it. We pushed the idea into the market.

Over time, the concept became expected. Industrial customers started requesting VMI solutions proactively — and eventually writing it directly into tender requirements. The market had shifted from us pushing a concept to customers pulling it as a standard.

That is the measure of a successful concept.

---

*Part of [NorthLogicLab](https://github.com/NorthLogicLab) · Built by [Jon Bach](https://theenginesbehind.com)*
