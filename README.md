# Maintenance Command Center

**Demand-driven maintenance planning: slide demand up, toggle overtime, and watch machine failure risk, boiler and chiller load, shift coverage and units-at-risk respond in real time. Links the shop floor to the S&OP forecast.**

## Overview

Maintenance Command Center is a browser-based dashboard that connects two things most plants manage separately: **production demand** and **equipment health**.

Instead of showing static machine status, it lets a planner ask "what if?" What happens to my equipment if demand rises 20%? What if we run an overtime shift? Which machines become critical, which batches are exposed, do I have the right people on shift, and can I even meet the forecast with the capacity that's left?

Everything updates live from one demand slider and one overtime toggle.

## Dashboard Link: https://ayanvsingh.github.io/torqueline-ops-command-center/

## The Problem

In many manufacturing plants, planning and maintenance work in silos:

- **Planners** commit to demand without knowing how much stress it puts on aging equipment.
- **Maintenance teams** see failures only after they happen, or see machine health with no link to which customer orders are at stake.
- **Spare parts and lead times** are discovered during a breakdown, not before it.
- **Shift coverage** is checked after the alarm goes off, when it's too late to find a technician with the right expertise.
- **S&OP meetings** treat capacity as a fixed number, even though it shrinks every time a critical asset is flagged.

The result is reactive firefighting, missed export orders, expensive external repairs and avoidable overtime.

## The Idea Behind It

> Capacity is not a fixed number. It depends on equipment health, and equipment health depends on demand.

This dashboard closes that loop. It treats demand load as the input and projects its effect on:

1. Equipment failure risk
2. Utility (boiler and chiller) load
3. People and expertise required
4. Production batches exposed
5. Effective capacity versus forecast demand

That gives planners, maintenance leads and operations managers a shared view and a common language for trade-offs, before a failure forces the decision.

## Features

### Global controls and alarm strip
- **Demand slider** sets the demand load as a percentage of baseline.
- **Overtime toggle** adds extra stress to equipment and utilities.
- **Alarm strip** across the top lists every critical machine or utility, with the batch at risk, or confirms that no alarms are active.

### Machines view
- Fleet list with a live failure-risk percentage and a status of **Healthy**, **At risk** or **Critical**.
- Fleet summary showing how many machines are flagged at the current demand.
- **Detail panel** for the selected machine with MTBF, time since last service, failure risk and units at risk.
- **Risk vs. demand chart** showing projected failure risk as demand increases, with a critical-threshold line and a marker for the current setting.
- **Batches at risk** if the machine goes down, with priority (for example export vs. domestic).
- **Repair planning data**: spare in stock or lead time, in-house capability, in-house vs. external repair cost, and the responsible owner.
- **Plan status** per asset: Planned, In progress or Resolved.

### Boilers and Chillers view
- Semicircular gauges showing the load of each utility as a percentage of its safe limit.
- Trend sparkline showing how load builds as demand approaches the current setting.
- Operating temperature and pressure ranges, owner and plan status for each unit.

### Team Coverage view
- Roster of technicians with their expertise and availability: **On shift**, **On call** or **Off**.
- Automatically works out which expertise is needed, based on which machines and utilities are currently flagged.
- Summary of how well the needed skills are covered right now.

### Demand and Forecast view
- Monthly demand chart showing actuals, a **3-month moving-average forecast** and **current production capacity**.
- Capacity degrades as more assets are flagged, so the gap between forecast demand and capacity is always up to date.
- Clear indication of surplus or shortfall in thousands of units.

### S&OP Snapshot
- A one-screen summary for sales and operations planning: projected demand against capacity, and the maintenance risks driving any gap.

## How the Logic Works

The dashboard uses transparent, rule-based models rather than a black box, so every number can be traced and challenged.

**Machine failure risk**

    risk = baseline + (demand load × sensitivity × 55) + overtime bump

- `baseline` is the machine's inherent risk at normal demand (age, condition, service history).
- `sensitivity` is how strongly this machine reacts to extra load.
- `overtime bump` is extra risk when the overtime shift is active.

Risk is capped to a 0-100% range and classified as:

| Risk | Status |
|------|--------|
| Below 40% | Healthy |
| 40% to 64% | At risk |
| 65% and above | Critical |

**Utility load (boilers and chillers)**

    load % = 55 + (demand load × sensitivity × 60) + overtime bump

Load is clamped between 20% and 99%. Status turns **elevated** at 72% and **critical** at 88%.

**Units at risk**

Each machine has batches with a priority. The dashboard weights each batch's units by priority (critical batches count fully, medium ones partially, low-priority buffer stock least) to estimate how much output is exposed if that machine fails.

**Expertise needed**

Any machine or utility that is not "Healthy" adds its required expertise (Molding, Filling, Boilers and so on) to the needed set. The Team Coverage view compares that set against who is on shift or on call.

**Forecast and capacity**

Demand for the next months is forecast with a **3-month moving average** of historical demand. Production capacity is reduced as more assets become flagged, and the difference between projected demand and capacity feeds the S&OP snapshot.

## Where It Can Be Used

The sample data models a packaging plant (molding, filling, sterilization, packaging, plus boilers and chillers), but the concept applies wherever demand stresses equipment:

- **Pharmaceutical and medical packaging** (batch-driven, with export and domestic priorities)
- **Food and beverage plants** (filling lines, sterilizers, boilers, cold chain)
- **FMCG and consumer goods** manufacturing
- **Plastics and injection molding** operations
- **Utilities-heavy facilities** (steam, chilled water, compressed air)
- **Any S&OP process** that needs maintenance risk to be visible to planners

It is also useful as:

- A **teaching tool** for operations management, maintenance engineering and S&OP courses
- A **prototype or UI reference** before building a production system on live plant data
- A **discussion aid** in planning meetings and maintenance reviews


## How to Use It

1. **Set the scenario.** Drag the demand slider and switch overtime on or off. Every view updates immediately.
2. **Read the alarm strip.** It tells you instantly which assets are critical and which batches are at risk.
3. **Go to Machines.** Select a machine to see its risk curve, how close it is to the critical threshold, and what is exposed if it fails.
4. **Check Boilers and Chillers.** Look for utilities approaching their safe limit before they limit production.
5. **Check Team Coverage.** Confirm the expertise you need is on shift or on call, and arrange cover if not.
6. **Open Demand and Forecast.** See whether capacity, after accounting for flagged assets, can meet the forecast.
7. **Use the S&OP Snapshot** to summarize the trade-offs for the planning meeting.
8. **Track actions.** Mark each flagged asset as Planned, In progress or Resolved.


---

*Built to answer one question before it becomes an emergency: what does this demand do to our equipment?*
