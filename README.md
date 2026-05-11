# ESL — Electronic Shelf Label

> *Automated VMI ordering system. Two buttons. Zero manual replenishment.*

---

## What it solves

Manual replenishment on warehouse shelves is slow, error-prone and invisible to the ERP system. Staff forget to order, order too late or order the wrong quantities.

ESL replaces the process with a two-button hardware label mounted directly on the shelf:

- **Button 1** — triggers an order line instantly
- **Button 2** — confirms delivery and resets the order line

No screens. No logins. No manual data entry.

---

## How it works

```
Button press → REST API → Order pooled by site
→ Weekly trigger → CSV/EDI → SAP → Delivery next day
→ Button 2 confirms → Order line reset
```

Orders from all shelf labels on a site are pooled throughout the week. At a predefined day and time, the batch is converted to CSV, transformed to EDI format and pushed to SAP for automatic fulfilment.

Duplicate presses within the same order period are detected — the label display confirms the item is already ordered.

---

## Architecture

| Component | Role |
|---|---|
| ESL Hardware | 2-button label, e-ink display, wireless |
| REST API | Collects and pools order lines per site |
| LM Admin | Configuration portal for items, sites, access points |
| SAP | ERP system — receives EDI, checks availability, fulfils |
| LTE Router | Wireless connectivity, min. 20m range per access point |

---

## Key requirements

- 24/7/365 availability
- Battery life minimum 2 years
- Operating temperature -10°C to +50°C
- Dust, dirt and grease resistant
- Display update within 10 seconds
- CSV/EDI output compatible with SAP

---

## Documentation

- [ESL Use Case — System Architecture](docs/ESL%20UseCase.pdf)
- https://www.lemu.dk/da/services/levering-og-lagerstyring/smartlager/elektronisk-hyldeforkant
---

## Status

Co-architect of the ESL system now commercially deployed as part of Lemvigh-Müller's SmartLager™ solution — serving industrial customers across Denmark.
---

*Part of [NorthLogicLab](https://github.com/NorthLogicLab) · Built by [Jon Bach](https://theenginesbehind.com)*
