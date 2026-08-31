# Origo — Client Interview Kiosk

A touch-first client intake and interview application for an advocate's office.
Ask the client only the questions that matter, tick off the documents they brought,
and walk away with a CSV, PDF and JSON record ready for drafting.

**One HTML file. No installation. No internet. No server. No account.**

---

## Quick start

### Option 1 — just open it
Download `origo-app.html` and double-click it. That's the whole application.

### Option 2 — publish it on GitHub Pages
1. Push this repository to GitHub.
2. Go to **Settings → Pages**.
3. Under *Source*, choose **Deploy from a branch** → branch `main`, folder `/ (root)`.
4. Wait a minute. Your app is live at `https://<your-username>.github.io/<repo-name>/`

`index.html` is an identical copy of `origo-app.html`, so GitHub Pages serves the
app automatically at the root URL.

### Option 3 — use it offline on a tablet or phone
Open the Pages URL once in Chrome or Safari, then use the browser's
**Add to Home Screen**. It launches full-screen like a native app and keeps
working with the internet switched off.

---

## The PIN

The app opens on a lock screen.

**Default PIN: `2244`**

Change it from **Backup → Security → Change PIN**. The screen also locks itself
after 10 minutes of inactivity, and there is a 🔒 button in the top bar to lock
it instantly when a client walks up to the desk.

> **What the PIN is for:** stopping a client from reading the previous client's
> matter while the tablet sits on the desk. It is **not** encryption. Anyone with
> access to the device's browser storage can still read the data. Keep the device
> itself locked with the operating system PIN as well.
>
> There is **no PIN recovery**. If you change it and forget it, clear the browser's
> site data — which also erases every saved matter, so **take a JSON backup first**.

---

## How the interview works

Tap **Start New Interview** and the app walks through numbered steps:

| Step | What it asks |
|---|---|
| Case Category | Civil, Family, Cheque, Revenue, Criminal, Consumer, Drafting, Other |
| Case Type | The exact matter — this decides everything that follows |
| Client Details | Name, mobile, role, address, ID brought |
| Other Side | Opposite party, forum, case number, stage |
| Case Questions | Questions written specifically for that case type |
| Facts & Relief | The story in the client's own words, timeline, limitation |
| Documents | Tap **Got it** for every paper handed over |
| Fee & Follow-up | Fee, advance, balance, next date, next action |
| Review & Save | Check everything, then save and export |

### Questions appear only when they are relevant

This is the core idea. A few examples:

- Answer **"Notice sent: Yes"** → the notice date, mode of sending, and
  service-status questions appear. Answer **No** → they never show.
- Answer **"Children: No"** → custody and child-details questions stay hidden.
- Answer **"Fee not discussed"** → the amount fields don't exist.
- Answer **"Part payment received: Yes"** → the amount box appears.

The intern never scrolls past a field that doesn't apply.

### It stops mistakes before they happen

- Questions marked `*` block the **Next** button, with a plain-language message
  that scrolls to the offending question.
- Entering a mobile number that already exists warns you and links to the
  existing matter.
- Limitation reminders are printed inside the relevant questions — for example
  the cheque-return date carries *"notice must be sent within 30 days of THIS date."*
- Work is auto-saved as a draft continuously. Close the tab by accident and
  **Resume Draft** picks it up.

---

## Exports

From the review screen, or the buttons on any saved matter:

| Export | What it is | Use it for |
|---|---|---|
| **CSV** | Excel-ready, one column per question | Mail-merge into notice and plaint templates |
| **Full PDF (print)** | Complete record via the browser's print dialog | Marathi renders perfectly here |
| **PDF file download** | A real `.pdf` file, no dialog | English fields only — see the note below |
| **JSON** | Structured data, per matter or whole device | Restore, or feed into your own drafting tools |
| **Client Slip** | Signed requisition of pending documents | Hand to the client — excludes your private notes |
| **Drafting Brief** | Parties → jurisdiction → facts → relief → evidence | Advocate-mode print for actually drafting |

**Why two PDF buttons.** The direct `.pdf` download uses the PDF format's built-in
fonts, which cannot draw Devanagari — Marathi text would come out blank. So any
record containing Marathi should use **Full PDF (print)** and then *Save as PDF*
in the print dialog, which renders it correctly. The direct download is there for
English-only records where you want a file with no dialog at all.

### Privacy in printed output

Two fields — **Weak points / risks** and **Note for the advocate** — are marked
private. They appear in your internal Full PDF and Drafting Brief, and are
deliberately **excluded from the Client Slip** you hand across the desk.

---

## Two modes

Switch with the 👤 button in the top bar.

- **Intern** — the kiosk only. Home, Interview, Matters, Case Types, Backup.
- **Advocate** — adds the **Advocate Desk**: a full grid of every matter, fee
  quoted / received / outstanding totals, and the Drafting Brief export.

The 🌐 button cycles the language: **English + Marathi** → **English** → **Marathi**.

---

## Editing the case types

**Case Types** tab. Every category and case type can be renamed, deleted, or added
to, and each one's document checklist is editable. Changes apply to all future
interviews; already-saved matters are untouched. **Restore defaults** brings back
the shipped library without touching your saved matters.

The eight shipped categories cover Civil/Property, Family/Matrimonial,
Cheque/Recovery, Revenue/Land Records, Criminal, Consumer, Documentation/Drafting,
and General Consultation — with over 100 case-specific questions between them.

---

## Where the data lives

In this browser's `localStorage`, on this device. Nothing is uploaded anywhere —
the file contains no external scripts, no fonts, no trackers, no network calls
of any kind. You can confirm this by opening it with the Wi-Fi off.

**This means:**

- Use the **same browser on the same device**, every time.
- Clearing "browsing data / cookies and site data" **erases everything**.
- Private/Incognito windows lose everything on close.
- The app nags you for a backup after 7 days. Listen to it.

**Backup routine:** open **Backup → Backup Everything Now**. That writes a JSON
(everything, restorable) plus two CSVs (all matters, and a document-status sheet).
Keep them somewhere that isn't the tablet.

To restore on a new device: **Backup → Restore from JSON**, then choose *Merge*
(keeps both sets) or *Replace* (wipes and loads the file).

---

## Repository contents

```
index.html       Copy of the app, so GitHub Pages serves it at the root URL
origo-app.html   The application — this is the file that matters
README.md        This document
LICENSE          MIT
.gitignore       Keeps OS and editor clutter out of the repository
```

There is no build step, no dependency, and nothing to install. `origo-app.html`
is the entire program.

---

## Updating the app later

Because the data lives in the browser and not in the file, you can replace
`origo-app.html` with a newer version and **your saved matters survive** — the
storage keys stay the same. Still, take a JSON backup before you update.

---

## Disclaimer

Origo is an office record-keeping tool. The questions, checklists and limitation
reminders are drafting aids for the advocate's own use — they are not legal advice
and are not a substitute for the advocate's judgment on any matter.

## License

MIT — see [LICENSE](LICENSE).
