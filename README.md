# Business Insights

A single-file dashboard that turns a **RingCentral call log export** into clear, actionable insight on your recruiting team: who is calling, when candidates pick up, where the idle time goes, and who needs a check-in.

Open it in a browser, drop in the export, done. No server, no install, no account. Your data never leaves your computer.

![Overview](docs/screenshots/overview.png)

## Features

- **Nine focused pages**: Overview, Recruiters, Profile, When to call, Where to call, Work rhythm, Attendance, Call quality and Inbound.
- **Plain-language summaries**: every page opens with a one-line summary written from your data, and every chart carries a one-line takeaway.
- **Chart or table, your choice**: flip any card between a chart and a table, or switch the whole dashboard at once.
- **Copy to Excel**: every card and table has a **Copy** button that places the data on your clipboard as cells, ready to paste into Excel or Google Sheets. Large tables also export to CSV.
- **Period comparison**: pick *Last 5 days* or *Last 20 days* and the headline numbers show the change against the previous period of the same length.
- **Coaching profile per recruiter**: score breakdown, best hours to call, weekday pick-up, call length versus the team, and a day-by-day history.
- **Remembers your data**: loaded files are kept in the browser (IndexedDB), so a refresh does not lose anything.
- **Live file sync** (Chrome and Edge on desktop): link an export on your computer and the dashboard re-reads it on a schedule.

| Recruiters | Profile |
|---|---|
| ![Recruiters](docs/screenshots/recruiters.png) | ![Profile](docs/screenshots/profile.png) |

| When to call | Table view |
|---|---|
| ![When to call](docs/screenshots/when-to-call.png) | ![Table view](docs/screenshots/table-view.png) |

## Getting started

### Option 1: open the file

1. Download `index.html`.
2. Open it in Chrome, Edge, Firefox or Safari.
3. Drop your RingCentral export onto the page, or click **Choose file(s)**.

### Option 2: host it with GitHub Pages

1. In this repository go to **Settings → Pages**.
2. Under **Build and deployment**, choose **Deploy from a branch**, select `main` and `/ (root)`, then **Save**.
3. After a minute the dashboard is live at `https://<your-username>.github.io/<repository-name>/`.

The hosted page only serves the dashboard. Call logs you load are processed in your own browser and are not uploaded to GitHub or anywhere else.

### Try it with sample data

`sample/sample-call-log.xlsx` contains about 16,000 **made-up** calls (fictional names and 555-01xx numbers) so you can explore every page before loading real data.

## Getting the export from RingCentral

Export the call log to Excel (`.xlsx`) or CSV. The sheet needs these columns (names are matched case-insensitively):

| Column | Used for |
|---|---|
| `From Name`, `From Number` | Recruiter and caller ID on outbound calls |
| `To Name`, `To Number` | Candidate on outbound calls, recruiter on inbound |
| `Result` | Connected, Not Connected, Answered, Missed, Voicemail |
| `Call Length` | Talk time (`h:mm:ss`) |
| `Call Start Time` | Date and time, read as Eastern Time |
| `Call Direction` | Outbound, Inbound, Internal |
| `Session Id` *(optional)* | Groups inbound legs and removes duplicates |

If the workbook also has a **Filters** sheet listing users, the dashboard uses it to spot people on the roster who made no calls. You can load several files at once; overlapping calls are de-duplicated.

## Settings

Click **Settings** to match your team's working day. Everything recalculates on save.

- Shift start and end, break times and break length (Eastern Time)
- Daily targets for calls and talk minutes
- What counts as an idle gap, an absent day, a real conversation, an instant hang-up, and more (under **Advanced**)

## Keyboard shortcuts

| Key | Action |
|---|---|
| `1`–`9` | Jump to a page |
| `T` | Switch every card between charts and tables |
| `Esc` | Close menus, the data panel and settings |

## Privacy

- All parsing and analysis happen in the browser. Nothing is sent to a server.
- Data is stored only in your browser's IndexedDB. Use **Your data → Remove all data** to clear it.
- `.gitignore` blocks `.xlsx` and `.csv` files (except the sample) so real call logs, which contain phone numbers, are not committed by accident.

## How it is built

- One self-contained HTML file: plain JavaScript, inline SVG charts, no build step and no framework.
- Excel parsing by [SheetJS](https://sheetjs.com/) Community Edition 0.18.5, embedded in the file (Apache License 2.0).
- UI font: [Manrope](https://fonts.google.com/specimen/Manrope) from Google Fonts, falling back to system fonts when offline.

## Project structure

```
.
├── index.html                 # the dashboard (open this)
├── sample/
│   └── sample-call-log.xlsx   # fictional demo data
├── docs/
│   └── screenshots/           # images used in this README
├── CHANGELOG.md
├── README.md
└── .gitignore
```

## Author

Built by JK.
