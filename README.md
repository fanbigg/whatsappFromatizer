# Event Roster Formatter

A quick tool to turn raw WhatsApp event booking details into clean, ready-to-use WhatsApp rosters for your team.

## Features
- **Auto-Formatting**: Standardizes dates to `dd/mm/yyyy (Day)` and event times to 12-hour format.
- **Reads Dates However They Arrive**: `08/08/2026`, `3/3/24`, `8.8.2026`, `2026-08-08`, `3 feb 2027`, `Feb 3, 2027`, `3 Ogos 2026`, `15 Disember 2026`. Malay and English month names both work, long or shortened. A date with no year (`3 Feb`) is read as the coming one, never one already past.
- **Reads Malay Times**: `11 pagi`, `12 tghari` / `tengahari`, `1 ptg` / `petang`, `8 malam`, `12 tengah malam`, and `pukul 10`. `12 malam` is midnight, `12 tghari` is noon.
- **8-Hour Rule**: No booking runs longer than 8 hours, so an unmarked time is read the way that fits a real working day — `11-1ptg` is 11.00am - 1.00pm, never 11.00pm - 1.00pm, and a bare `2 - 6` is the afternoon, not two in the morning.
- **Flags Conflicts Instead Of Guessing**: If `Masa Event` and `Session Hour` disagree (`11-4PM` marked as `4 Hours`), or the session works out longer than 8 hours, or the time cannot be read at all, the block comes out with a `⚠️ CHECK` line and **everything blanked except the event time and the two hour figures** — stated and calculated, side by side. Nothing is priced, and the half-empty block cannot be forwarded by accident, so it gets confirmed with the client first.
- **Many Bookings At Once**: Paste as many forms as you like in one go. A new booking is detected from a blank line, a line of dashes, or simply a key repeating (the next `Nama:` or `Tarikh:`) — so back-to-back WhatsApp forms with nothing between them still come out as separate rosters, joined by a dashed separator. Bolded keys (`*Tarikh:*`), bullets, and `1.` numbering are all read.
- **Forgiving Input**: Reads the times people actually type — `9.00AM`, `9AM`, `9 a.m.`, `14:30`, and ranges joined by `-`, `–`, or `to`. If the start time has no am/pm, it is inferred from the end time (`10 - 4.30PM` becomes a 6.5 hour morning-to-afternoon session).
- **Call Time**: Calculates 1-hour prep call time automatically and bolds it (`*HH.MMam/pm*`) for WhatsApp. Wraps correctly past midnight.
- **Pay Calculation**: Computes total hours (`Session + 1h prep`) and total pay (`RM15/h`). Sessions are rounded to the nearest half hour, so a 5h30m job is not billed as 6h. The clock is the source of truth when it can be read; a stated `Session Hour` is used only when there is no readable time. Nothing is billed at `RM 0` — with no hours to go on, the totals stay blank.
- **Safe Dates**: A date that does not exist (`31/02/2026`) is passed through untouched rather than silently rolled over to a date nobody booked.
- **Copy & Share**: **Copy** puts the roster on the clipboard and tells you honestly if the browser blocked it. On phones a **Share** button opens the native share sheet, so the roster can go straight into a WhatsApp thread.
- **Works Offline**: No fonts, scripts, or requests of any kind are fetched. Open the file and it runs.
- **Privacy First**: Runs 100% client-side in your browser. No data is stored anywhere.

## How to Use
1. Paste raw WhatsApp message blocks into the input panel. Multiple bookings can follow one another directly; a blank line or a line of dashes between them is optional.
2. The formatted roster appears instantly in the output panel.
3. Tap **Copy** (or **Share** on a phone) and paste it into your WhatsApp group.

## Input Format

Any `Key: value` lines are read; unrecognised keys (like `Nama` or `No phone`) are ignored.

```
Nama: Ms Lim
No phone: 016-2282102
Tarikh: 08/08/2026
Tempat: Kuantan Parade
Type of event: Conference
Masa Event: 9.00AM - 3.00PM
Session Hour: 6 Hours
```

`Masa Event` ranges can be joined by `-`, `–`, `~`, `to`, `hingga`, or `sampai`.

A block needs at least a `Tarikh` or a `Tempat` line to be treated as a booking. Paste several such blocks one after another and each becomes its own roster; the app's own output can be pasted back in and re-formatted without change.

## Layout

Two panes side by side on a desktop, stacked with full-width controls on a phone. Inputs use 16px text so iOS Safari does not zoom when you tap into them.

## Design

Shares one design language with the other Micro Apps ([QR Generator](https://github.com/fanbigg/qr-generator) and [Wheel of Fortune](https://github.com/fanbigg/wheel_of_fortune)): a simulated macOS window with a traffic-light title bar, one shared set of light/dark colour tokens that follow the system appearance, and the same button, input, and phone-layout rules. The shared block is marked `shared macOS app shell` in the `<style>` element — edit it in one app and copy it to the others rather than letting them drift.

---

*Built for quick deployments via GitHub Pages.*
