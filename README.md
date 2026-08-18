# Event Roster Formatter

A quick tool to turn raw WhatsApp event booking details into clean, ready-to-use WhatsApp rosters for your team.

## Features
- **Auto-Formatting**: Standardizes dates to `dd/mm/yyyy (Day)` and event times to 12-hour format.
- **Forgiving Input**: Reads the times people actually type — `9.00AM`, `9AM`, `9 a.m.`, `14:30`, and ranges joined by `-`, `–`, or `to`. If the start time has no am/pm, it is inferred from the end time (`10 - 4.30PM` becomes a 6.5 hour morning-to-afternoon session).
- **Call Time**: Calculates 1-hour prep call time automatically and bolds it (`*HH.MMam/pm*`) for WhatsApp. Wraps correctly past midnight.
- **Pay Calculation**: Computes total hours (`Session + 1h prep`) and total pay (`RM15/h`). Sessions are rounded to the nearest half hour, so a 5h30m job is not billed as 6h.
- **Safe Dates**: A date that does not exist (`31/02/2026`) is passed through untouched rather than silently rolled over to a date nobody booked.
- **Copy & Share**: **Copy** puts the roster on the clipboard and tells you honestly if the browser blocked it. On phones a **Share** button opens the native share sheet, so the roster can go straight into a WhatsApp thread.
- **Works Offline**: No fonts, scripts, or requests of any kind are fetched. Open the file and it runs.
- **Privacy First**: Runs 100% client-side in your browser. No data is stored anywhere.

## How to Use
1. Paste raw WhatsApp message blocks into the input panel. Separate multiple bookings with a blank line.
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

A block needs at least a `Tarikh` or a `Tempat` line to be treated as a booking.

## Layout

Two panes side by side on a desktop, stacked with full-width controls on a phone. Inputs use 16px text so iOS Safari does not zoom when you tap into them.

## Design

Shares one design language with the other Micro Apps ([QR Generator](https://github.com/fanbigg/qr-generator) and [Wheel of Fortune](https://github.com/fanbigg/wheel_of_fortune)): a simulated macOS window with a traffic-light title bar, one shared set of light/dark colour tokens that follow the system appearance, and the same button, input, and phone-layout rules. The shared block is marked `shared macOS app shell` in the `<style>` element — edit it in one app and copy it to the others rather than letting them drift.

---

*Built for quick deployments via GitHub Pages.*
